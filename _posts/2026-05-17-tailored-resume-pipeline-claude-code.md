---
layout: post
title: "Building a tailored-resume pipeline with Claude Code in two weekends"
date: 2026-05-17
lane: agentic
description: A case study on the experience-store-as-source-of-truth pattern, and what it would look like for scientific workflows.
---

## TL;DR

I built a personal job-application system over two weekends that produces a tailored resume and cover letter from a pasted job description in about ten minutes — and crucially, **the LLM cannot invent claims**. Every bullet on every generated resume traces back to an atomic experience unit in a YAML store. The same compose-from-IDs discipline, plus a denylist + LLM-judge confidentiality guard, makes this pattern reusable for any scientific workflow where you need an LLM to write polished prose without leaking information or making things up.

The system itself runs on [Claude Code](https://claude.com/claude-code) and a small Python core. Around 2000 lines of Python, four slash commands, one experience store. It replaces an hour of manual editing per application with about five minutes of curation.

This post walks through what the pipeline does, the three design decisions that made it work, and what the same approach buys you when the artifact is a target-review brief or a regulatory submission instead of a resume.

## The problem with generic LLM resume tools

The standard pitch for an LLM-based resume tool is "paste your CV, paste a job description, get a tailored resume." It works for entry-level applicants and people whose work is easy to describe. It falls apart for anyone whose actual job is technical, current, or contains material that should not appear in a public document.

Three failure modes show up immediately:

**Invention.** The model rephrases your resume to match the job description. Some of those rephrasings are plausible but wrong — the model decides that because you used `scanpy` and the job mentions `Seurat`, you must know both. You catch the obvious ones on review and miss the subtle ones. A hiring manager catches the rest, on a phone screen, after you've made it through two rounds. The downstream cost of a single fabricated bullet is enormous; the upstream cost of preventing it should be enormous in return, and yet most tools simply do not.

**Leakage.** Anything specific to your current employer is now in a third-party LLM context window. Internal target codenames, indication names, proprietary method names — all of it. Most companies have policies against this; many people violate them daily without thinking. The standard advice ("redact before pasting") is the kind of advice that survives until the first deadline and then quietly dies.

**Voice collapse.** The output sounds like the LLM's idea of a resume, not yours. You spend half your editing time un-flattening the prose. After three or four passes the tone is roughly yours, but you've lost the time you were trying to save.

The first two failure modes are not editing problems. They are *architectural* problems. They cannot be fixed by writing a better prompt or by being a more careful user.

## The store as source of truth

The core design move is to **separate the substance of what you can claim from the surface of how you say it**. Substance lives in a structured YAML store. Surface lives in templates and a small amount of LLM-mediated narrative writing. The two never get confused because they are mechanically different artifacts.

The store has four sections: roles, units, education, publications. The unit is the atom of the whole system. Every claim about what you have done lives in a unit. A unit looks like this:

```yaml
- id: u_eclipsebio_riboseq_pipeline
  role_id: r_eclipsebio_ds2
  action: Built a Ribo-Seq data retrieval and processing pipeline supporting training of RNA-focused large language models.
  outcome: Enabled fine-tuning and deployment of models for therapeutic RNA design, structural and regulatory feature prediction, and multi-omic integration.
  metric: null
  skills:
    - Python
    - Ribosome profiling
    - Bioinformatics pipelines
    - RNA foundation models
  tags:
    - lane:methods
    - confidentiality:safe
```

A few properties are worth dwelling on. The `id` is stable and humanly memorable. The `action` is a complete sentence that can stand alone in a resume bullet — no rewriting needed when it gets surfaced. The `outcome` describes what the work *enabled*, in the same standalone style. The `metric` slot exists for the units that have a number to report, and is `null` for those that do not. The `skills` and `tags` arrays are *retrieval keys*, not claims — they help the tailor surface the right units for the right job, but never appear verbatim in output.

The store is the only place where you maintain biographical truth. Everything downstream is regenerated from it. When you finish a project, you add a unit. When a project ends or shifts, you mark it. You never edit a generated resume — you edit the store and re-render.

The validator enforces some structural invariants: no duplicate IDs, every unit points at a known role, every package and external post that claims a `paper_id` points at a known publication. The integrity check is not optional — it runs every time the store is loaded. If it fails, nothing else runs.

## Compose-from-IDs: making invention mechanically impossible

Once the store exists, the next question is how the tailor picks which units appear on a given resume. The naive answer is "let the LLM look at the store and write the resume." That answer reintroduces all three failure modes from the previous section.

The actual answer is what I call **compose-from-IDs**: the LLM looks at the store and at the job description, and produces a structured plan that says which unit IDs to surface, in which order, under which role, with which optional drop-outs. The plan is a JSON file. It contains only IDs and ordering hints.

```json
{
  "selected_units_by_role": {
    "r_mirador_aiscientist": ["u_target_nomination", "u_perturb_seq_pipeline", "u_companion_dx_model"],
    "r_sanford_postdoc": ["u_rna_foundation_finetune"],
    "r_eclipsebio_ds2": ["u_riboseq_pipeline"]
  },
  "skills_emphasis": ["Python", "scRNA-seq", "Multi-omic integration"],
  "gaps": ["No direct experience with X mentioned in the JD; consider mentioning related Y"]
}
```

A pure-Jinja template then takes the plan and the store and produces the resume. The template knows nothing about the job description. It cannot rewrite an `action` field, paraphrase an `outcome`, or invent a metric. Its job is to lay out what the plan selected, formatted to match the reference resume layout.

This is the structural guarantee. The LLM never writes resume prose. It only chooses which existing prose to surface. The template renders deterministically from the store, which means **a tailored resume is a function of `(store, plan)`** — and given the same inputs, you get the same output. You can diff two applications and see exactly which units differ. You can replay an application from six months ago and reconstruct it bit-for-bit.

The cover letter is harder. A cover letter must connect units narratively, in paragraphs, with voice — and that does need LLM-mediated writing. The same architecture still applies, but with a tighter constraint: each paragraph is written by a per-paragraph LLM call that is given **only the units it is allowed to cite**, plus the relevant slice of the job description, plus a voice profile. The output is then run through a claim-extraction verifier that pulls out every factual statement in the paragraph and confirms each one is supported by the units it was allowed to use. Unsupported claims fail the build.

Voice is handled through a separate channel: a `voice_profile.md` file that the system maintains, plus two to four hand-curated past cover letters used as per-call exemplars. The voice profile is generated once from a corpus of the author's writing and then **hand-edited** — stylometric extraction is a starting point, not an authority.

## The confidentiality guard

The third design move is to assume that confidentiality protection cannot rely on human discipline alone. People who have signed NDAs leak things every day, accidentally, while doing their jobs. The system needs to be conservative on their behalf.

This works in three layers.

**At ingestion**, a redaction pipeline runs over every input artifact — every PDF, every past resume, every weekly update, every chat export — before any of it lands in the store. The pipeline has two stages: a deterministic denylist (regex word boundaries on a curated list of program codenames, indication names, target gene symbols, internal method names) and an LLM judge that does a semantic pass to catch what the denylist missed. Both stages produce a redacted copy; the original never enters the pipeline.

**At storage time**, the store itself is structured to avoid carrying confidential content even when the underlying work is confidential. The voice profile is generated, the unit `action` and `outcome` fields are written in generic methodological language — "single-cell perturbation modeling for target nomination" rather than "perturb-seq for {specific target}". An `allowed-framings.md` document captures the pre-approved generic vocabulary; the store stays within it.

**At generation time**, the same denylist runs as a final guard on every generated artifact — resume, cover letter, blog post, site page — before it can be committed or pushed. The check is hard-fail. If a denylisted term appears in output, the publish step exits non-zero and the artifact does not ship.

None of these layers depend on the operator remembering anything. Even if you accidentally paste an internal email into your application notes, the pipeline catches it before it reaches the LLM context. Even if a paragraph in a cover letter drifts toward specifics, the final guard pulls it back. The defense is in depth, not in attention.

The framing matters here. This is not "company secret protection" as an abstract employer obligation. It is **patient-mission protection** — the work this system was built around protects programs that are themselves intended to help real patients. A leak is not just a contract violation; it is a small theft from the people the work is for. Framing it that way makes the discipline easier to sustain because the discipline has a *reason* that survives the bad day.

## What this looks like in a lab

Now the generalization. Strip away the "resume" framing and what is the system actually?

It is a pattern for producing **defensible polished prose from a structured fact store, with an LLM doing only the parts an LLM is good at** — choosing relevant elements from a pool, weaving them into a narrative, matching a voice — and never the parts where an LLM is dangerous: inventing facts, leaking specifics, sounding generic.

The same shape works for:

**Target nomination briefs.** Replace "units" with "evidence atoms." Each atom is a single piece of evidence that supports a target — a CRISPR-screen hit, a perturb-seq cluster, a genetics association, a clinical correlation. Each atom has a stable ID, a source citation, a calibrated weight, and tags. The brief is composed from atom IDs: the analyst picks which evidence to surface for which audience, the renderer produces the formatted document. Hallucination is mechanically impossible; every claim in the brief is auditable back to a source.

**Regulatory writing.** The substance lives in a controlled vocabulary of pre-approved phrasings tied to underlying data. The narrative is composed from those phrasings. The regulator-facing document is regenerated from the source of truth every time the underlying data updates.

**Paper drafts.** Each method module — sample collection, library prep, sequencing, processing, statistical analysis — lives as a unit with a stable ID. The methods section composes from module IDs in the order the analysis ran. Changes to the method propagate to the paper draft automatically.

**Lab notebook narratives.** Each experimental day produces a small set of result units. End-of-week summaries are composed from selected units; the LLM writes the connective narrative; the verifier confirms every factual claim traces to a unit. The author never has to remember what they actually did — the store does.

In every case the architecture is the same: a structured store of small, atomic, ID-addressable facts; a deterministic renderer for surfaces that should not vary; an LLM constrained to choose-and-narrate over a pre-approved pool; a confidentiality guard that runs on inputs and outputs.

The pattern is not specific to text. The same logic applies to any artifact where the cost of a fabrication is high and the benefit of polish is real. Most scientific outputs sit in that quadrant.

## What I learned about building with Claude Code

Building this in Claude Code rather than in a hand-rolled CLI changed a few things.

**Slash commands as the conversational layer.** Each user-facing entry point — `/career`, `/apply-to-job`, `/bootstrap-experience`, `/refresh-voice` — is a Claude Code slash command. The command file is a markdown document that reads like a script for a human conversation: "Ask the user for X. If they say Y, do Z; otherwise route to W." The orchestrator is the LLM following the script, not a Python state machine. The state machine lives in real code (slim Python helpers, deterministic Pydantic validators); the conversational layer lives in the slash command. This separation is the one design choice I am most certain about.

**Custom skills for repeated workflows.** A "skill" in Claude Code is a small, named, invocable instruction set — brainstorming, writing-plans, executing-plans, requesting-code-review. The skills compose with the slash commands. A brainstorming session feeds a spec; a spec feeds a writing-plans run; the resulting plan feeds an executing-plans run. Each skill is opinionated about *how* to do its part well. The discipline survives because the skill, not the operator, enforces it.

**Subagents earn their keep on parallel mechanical work.** The implementation plan for this very system had thirty-some tasks. Two-thirds of them were "write a Pydantic model + tests" or "add a YAML section + validator." Dispatching a fresh subagent per task, with full task text inlined into the prompt, kept each subagent context-clean. The two-stage review pattern — first spec-compliance, then code quality — caught issues earlier than I would have caught them reviewing manually. The cost is roughly 3× the per-task LLM calls; the win is "implementation actually finished in two weekends."

**Where to stop automating.** A few decisions stay with the human. Which units to surface for a given role is a judgment call that the human owns. Which cover letter exemplars to feed a given paragraph is a curation step. Whether a specific application is worth the time at all — that question lives upstream of the whole pipeline, in a `/career` status command that surfaces the JD, the posted salary, and the basic match before any drafting begins. The system asks the human to make the choices that matter and removes the friction from the choices that do not.

## Cost and time

Honest numbers. The first weekend was the bootstrap pipeline (extract from old PDFs, classify, atomize into units, write the voice profile). About sixteen hours. Heavy LLM use during the redaction pass, but a fixed one-time cost. The second weekend was the per-job loop (resume tailor, cover letter, render to DOCX). Another twelve hours.

Per-application: about five minutes of LLM time, five minutes of human review, two minutes of git operations. The cost in API tokens is in the cents. The cost in human attention is the only cost that scales.

Compared to writing each application by hand from a master resume: probably an hour saved per application, with the additional property that every artifact is a function of the store, so a correction to the store propagates everywhere automatically.

## What I would change next

Three things, in priority order.

A **trends analyzer** that runs over the accumulated `plan.json` files from a hundred applications and surfaces which skills appear in postings I lose, which framings work, which kinds of roles I should stop applying to. The data is already accumulating; the analysis is a future weekend.

A **gap-aware tailor** that, when the chosen units do not cover a requirement in the JD, flags it explicitly rather than glossing past it. The current system surfaces gaps; the next version should propose how to address them ("you could add a half-day project to fill X").

A **portable runtime** so this can run somewhere other than Claude Code if the tool changes. The Python core is already standalone. The slash commands are markdown documents. Most of the discipline can move to any LLM tool that supports the same conversational pattern.

## Closing

The lesson, if there is one, is that LLM-mediated polished prose is a solved problem when you stop asking the LLM to be the source of truth. The substance lives in a structured store; the LLM lives in the surface layer. Compose-from-IDs makes invention mechanically impossible. Denylist + judge makes leakage mechanically improbable. Voice modeling, with hand-edited final say, makes the output sound like you instead of the model.

None of this is novel. It is the obvious architecture once you stop assuming "LLM" and "writer" mean the same thing. The trick is keeping that distinction sharp through every design decision — and noticing, in the moments where it would be easier to let the model decide, that those are exactly the moments where the structural guarantees pay for themselves.

If your work product is a polished document, and the cost of getting it wrong is real, this is probably the architecture you want. The same pattern that produces a defensible resume produces a defensible target brief, a defensible methods section, a defensible weekly update. The store is the point. The LLM is incidental. That is a much more comfortable position to build from.
