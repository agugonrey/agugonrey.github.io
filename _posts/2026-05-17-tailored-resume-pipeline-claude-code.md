## TL;DR

Over two weekends, I built a personal job-application pipeline that generates tailored resumes and cover letters from a pasted job description in about ten minutes — without allowing the LLM to invent claims. Every resume bullet traces back to an atomic experience unit stored in YAML. The same compose-from-IDs pattern, combined with confidentiality guards, generalizes well to scientific writing workflows where accuracy and information control matter.

The system runs on Claude Code with a lightweight Python backend: roughly 2,000 lines of Python, four slash commands, and a single experience store. It cuts application prep from about an hour to a few minutes of review and curation.

This post covers the architecture, the design decisions that made it reliable, and why the same pattern works for things like target-review briefs, methods sections, and regulatory writing.

---

## The problem with generic LLM resume tools

Most AI resume tools follow the same workflow: paste your resume, paste a job description, get a tailored version back. That works reasonably well for generic experience, but breaks down for technical or confidential work.

Three issues show up quickly:

- **Hallucination.** The model rewrites your experience to better match the posting and quietly introduces inaccurate claims.
- **Confidentiality leakage.** Internal targets, programs, or methods end up in an external model context window.
- **Voice flattening.** The output sounds like the model rather than the person applying.

These are architectural problems, not prompt-engineering problems.

---

## The store as source of truth

The key design decision was separating **what can be claimed** from **how it is presented**.

All factual content lives in a structured YAML store. Presentation is handled separately through templates and constrained LLM writing.

The atomic object is a **unit**: a small, self-contained experience fragment with a stable ID, action, outcome, optional metric, and retrieval tags. Every factual claim in a generated resume must come from one of these units.

The store becomes the single source of truth. Generated resumes are disposable outputs; the store is what gets maintained.

---

## Compose-from-IDs

Instead of letting the LLM freely write resumes, the model only selects which unit IDs should appear for a given job description.

It outputs a structured plan containing IDs and ordering hints. A deterministic template renderer then assembles the final document directly from the store.

This creates an important guarantee:

> the model can choose from existing claims, but it cannot invent new ones.

A resume becomes a deterministic function of `(store, plan)`. The same inputs always produce the same artifact, and every bullet is traceable back to a source unit.

Cover letters are handled differently because they require narrative flow. There, the LLM is constrained to specific allowed units per paragraph, and a verifier checks that every factual statement is supported by the provided source material.

---

## Confidentiality safeguards

The system assumes confidentiality cannot rely on human discipline alone.

Protection happens in three stages:

1. **Ingestion:** a redaction pipeline removes sensitive terms before material enters the store.
2. **Storage:** units are written in generalized methodological language rather than project-specific language.
3. **Generation:** every output artifact passes through a final denylist check before export.

The result is defense-in-depth rather than “remember to be careful.”

---

## Why the pattern generalizes

Underneath the resume framing, this is really a system for generating polished prose from a structured fact store while constraining the LLM to the parts it handles well: selection, organization, and narrative flow.

The same architecture works for:

- target nomination briefs
- regulatory writing
- methods sections
- lab notebook summaries
- scientific status updates

In each case:

- facts live in atomic, auditable units
- rendering is deterministic where possible
- LLMs operate only over approved material
- confidentiality checks run on both inputs and outputs

The pattern matters most in domains where polished language is useful but factual drift is expensive.

---

## What I learned building it with Claude Code

A few design choices mattered more than expected:

- **Slash commands** worked well as the conversational orchestration layer.
- **Custom skills** helped enforce repeatable workflows.
- **Subagents** were useful for parallel mechanical implementation work.
- Some decisions still belong to the human: selecting emphasis, curating examples, and deciding which applications are worth pursuing.

The best automation removes friction without removing judgment.

---

## Closing

The main lesson is simple:

LLMs work much better when they are not treated as the source of truth.

The structured store holds the facts. The model operates at the presentation layer. Once those roles stay separated, hallucination becomes controllable, confidentiality becomes manageable, and the output starts sounding human again.

That same architecture extends naturally beyond resumes to scientific and technical writing where traceability and precision matter.