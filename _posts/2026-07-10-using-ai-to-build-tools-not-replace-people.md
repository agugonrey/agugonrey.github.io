---
title: "Using AI to Build Tools, Not Replace People"
subtitle: "Helping Someone Reclaim Their Time With Tools They Can Promptly Use"
date: 2026-07-10
lane: agentic
description: "A practical argument for using AI-assisted development to build private, deterministic tools for people doing repetitive and confidential work."
---

## TL;DR

A lot of AI writing talks about replacing tasks, while only lightly touching on
what those tasks mean for people's livelihoods. The problem I keep thinking
about is different. I keep thinking about people who are already stretched
across human-facing work, follow-up, and repetitive administrative tasks that are
not easy to automate with state-of-the-art AI because of privacy, cost, or
company policy.

My current opinion is that the most democratic use of AI may not involve asking
everyone to use AI directly. Sometimes it is using AI-assisted development to
build small, private, deterministic tools that help people do their existing work
with less exhaustion and more control.

This post is about that pattern: using AI as a toolmaker, not as the worker.

---

## The problem I keep thinking about

AI is often described through extremes. Either it will automate whole jobs, or it
is a personal productivity layer everyone should immediately learn to use. My
intuition is that both framings miss a large group of people.

There are many workers outside the technical AI circle who are already skilled
at what they do. They understand their customers, forms, deadlines, messy
spreadsheets, and the tiny exceptions that never make it into a software demo.
They are not waiting for intelligence to arrive from a model. They already have
judgment. What they often do not have is time.

Imagine someone supporting a family in a high-cost city. They are good at their
profession and trusted by the people they serve. Their work includes human
interaction, care, context, and discretion. But to make the numbers work, they
also take on extra administrative work: filling tables, checking columns,
consolidating files, moving data between formats, and catching small errors
before those errors become larger ones.

This is not a story about someone who needs to be replaced.

It is a story about someone who deserves better tools.

---

## The problem is not lack of skill

When technical people see repetitive spreadsheet work, it is tempting to assume
the answer is training: teach Python, teach R, teach macros, teach notebooks,
teach a new platform.

Sometimes that is useful. But often, it misses the point.

The person doing the work may already be very good at Excel. They may understand
the workflow better than anyone else. They may know which fields are dangerous,
which values need a second look, and which customer-facing steps should stay
human.

The bottleneck is not intelligence or effort. It is the accumulation of small
manual operations that consume evenings, weekends, and attention: work important
enough to require accuracy, but repetitive enough that a person should not have
to carry all of it manually.

That distinction matters to me. If we misdiagnose the problem as lack of skill,
we build tools that make people feel behind. If we diagnose it as lack of time,
support, and appropriate automation, we can build tools that respect what they
already know.

---

## Why "just use AI" is the wrong answer

For many real workflows, directly using AI is not the right answer.

The work may involve confidential files. It may include customer information,
business records, medical-adjacent context, financial details, or internal
processes that should never be pasted into a public chatbot. Even when privacy
controls exist, the worker may not have an approved account, a clear policy, or
the authority to decide where that data goes.

There is also the human part of the job. Some tasks should not be automated
away. A customer may prefer a person because they trust the relationship. The
goal should not be to remove the human interaction that gives the work its
value.

So the question I keep coming back to is more specific:

How can AI help without putting private data into an AI system, replacing the
human-facing parts of the job, or asking the worker to become a programmer?

---

## AI as toolmaker, not worker

One answer is to use AI indirectly.

In this post, I use **technical helper** as a hypothetical role. It could mean
me helping a friend, or it could be any reader with enough scripting and AI-tool
fluency to translate a real workflow into a small local tool. The helper is not
there to take over the work. They are there to listen, understand the worker's
constraints, and leave behind something the person can actually run.

This role is not very visible in popular AI narratives. We talk a lot about the
individual AI user, the autonomous agent, or the company-wide automation
strategy. We talk less about the person in the middle: someone who uses AI tools
to build safer, simpler tools for someone else, especially when that person
cannot safely use AI directly.

Instead of asking an AI model to process confidential work, a technical helper
can use AI-assisted development to create deterministic scripts that run locally
on the worker's machine. The scripts do not call an AI model, upload data, or
make fuzzy decisions. They perform explicit, reviewable operations on files that
stay under the worker's control.

For example, a local tool might:

- combine weekly spreadsheets into one standardized workbook
- check whether required columns are present
- flag missing values or duplicated records
- reformat dates and identifiers consistently
- split a large table into customer-specific files
- generate a validation log that a person can review

The AI is used upstream, by the technical person, to help write and test the
tooling. The person's actual work remains local, deterministic, and auditable.

That separation is the key: AI helps build the tool, but the tool does not need
AI to run. The confidential material never has to become part of a model
conversation.

---

## Tools someone can actually use

For this kind of work, the technical design matters. But the usability boundary
matters more.

If the person needs to understand Python environments, package managers, Docker,
or Git before the tool helps them, the tool has already failed. The interface has
to match the reality of their machine, their day, and their available attention.

For a Windows user, that might mean:

- a clearly named folder for input files
- a clearly named folder for output files
- a PowerShell script or double-clickable launcher
- no paid vendor software
- no AI subscription
- no data upload
- readable error messages
- outputs that never overwrite the original files
- logs that explain what changed
- a small example dataset for practice
- a simple recovery path when something goes wrong

This is not glamorous software engineering. But it is the difference between a
tool someone uses once and a tool that quietly saves them hours.

A useful first version might look as simple as this:

```text
spreadsheet-helper/
  input/
    weekly_report.xlsx
  output/
  logs/
  run_clean_tables.ps1
  README.txt
```

The person should not need to understand the code. They should only need to know
what to place in `input/`, what to run, and where to find the result.

---

## The interview before the automation

Before writing scripts, the technical helper has to understand the work. In this
role, the first job is not coding. It is translation: turning someone's lived
workflow into a tool boundary that preserves what should stay human.

That means asking practical questions:

- Which steps take the most time?
- Which steps are most error-prone?
- Which steps require human judgment?
- Which files are safe to use as examples?
- What output would feel trustworthy?
- What would make the tool annoying enough to abandon?
- What mistakes would be costly?

This interview matters because automation is a workflow problem, not just a code
problem. A script that solves the wrong step can create more work. A script that
hides what it changed can reduce trust. A script that fails without a clear
message can make the person feel less capable, even if the code is technically
correct.

The goal is not to show off automation. The goal is to remove friction without
removing control.

---

## What technical people can do

People with technical skills and access to AI tools have an advantage right now.
We can turn vague friction into working prototypes much faster than before. My
concern is that this advantage can become another source of inequality. My hope
is that it can also become a way to build small bridges.

The bridge does not have to be a startup, a platform, or a generalized product.
Sometimes it is a folder, a script, and a README written for one person's actual
day.

That kind of help is easy to undervalue because it is small. But small tools
matter when someone is balancing paid work, family responsibilities, and the
emotional load of staying afloat in an expensive place.

AI will not become democratic just because more chat windows exist. It becomes
more democratic when people with access use it to make useful things for people
who would otherwise be left out of the benefit.

---

## What comes next

This post is the framing. The next step is more concrete.

I want to document the process of interviewing a real workflow, identifying
which steps should stay human, and building a small local toolkit around the
repetitive spreadsheet operations. The goal is to share a public example with
mock data, a GitHub repository, and instructions written for someone who does not
identify as a programmer.

The point is not that every repetitive task should be automated. The point is
that people deserve tools that respect their constraints.

Sometimes the best use of AI is not to put AI in the workflow. Sometimes it is
to build the tool that lets a person keep doing their work with a little more
time, privacy, and dignity.
