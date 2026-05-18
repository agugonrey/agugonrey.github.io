---
layout: default
title: Home

hero_tagline: "Bioinformatics ML/AI scientist working across target discovery, perturbation modeling, multiomic machine learning, and reliable AI tooling for scientific research."

hero_image: /assets/images/hero/headshot.jpeg
hero_image_alt: "Casual headshot of Agustin Gonzalez-Reymundez outdoors"

threads:
  - id: drug-discovery
    title: "Drug discovery AI"
    body: |
      Biology no longer suffers from a lack of data. The challenge is turning that data into decisions. The work in this thread focuses on translating high-dimensional biological signals into artifacts a program team can act on: ranked targets, companion diagnostic candidates, antibody leads, and defensible evaluation briefs.

      The toolkit includes single-cell perturbation modeling, multiomic integration, probabilistic ML, and antibody-design workflows. The emphasis is less on giant monolithic models and more on reproducible pipelines with traceable inputs and explainable outputs.

      The constraint shaping all of it is confidentiality. Specific programs and indications remain private; the publicly visible layer is the methodological stack.
    cta_text: "See papers"
    cta_href: "/papers/"
    thumb: /assets/images/threads/drug-discovery.png
    thumb_alt: "Workflow diagram for computational drug discovery and target nomination"

  - id: methods
    title: "Methods & packages"
    body: |
      High-dimensional biology depends on statistical software that is both rigorous and practical. Much of the existing ecosystem either overfits small datasets or oversimplifies complex structure. The work here aims for methods that are reproducible, interpretable, and usable on real biological data.

      Two CRAN packages anchor this thread. **MOSS** (Multi-Omic Sparse Singular Value Decomposition) models shared structure across omic layers without collapsing everything into a single representation. **eCV** (extended Concordance Voting) measures reproducibility in omic experiments and helps separate biological signal from measurement noise.

      Beyond the packages: sixteen peer-reviewed publications spanning multiomic ML, cancer genomics, plant breeding statistics, and ribosome profiling. Different applications, same underlying preference for methods that are transparent, maintainable, and easy to reproduce.
    cta_text: "Browse packages"
    cta_href: "/packages/"
    thumb: /assets/images/threads/methods.png
    thumb_alt: "Minimalist infographic for statistical software and multiomic methods"

  - id: agentic
    title: "Agentic tooling for science"
    body: |
      Most AI-agent demos avoid the hard part of scientific work: verification. In research and regulatory settings, hallucinations are expensive. The goal is not simply to automate scientific writing, but to build systems that produce outputs that can be defended.

      The pattern that has worked best for me is compose-from-IDs. Every claim in a generated artifact traces back to a structured source. The model selects and organizes canonical facts, while deterministic tooling handles rendering and validation. A confidentiality guard sits in front of every publish step.

      The blog documents practical implementations of this pattern: tailored-resume pipelines, Claude Code skills for scientific workflows, and systems for generating reviewable artifacts from structured inputs. The focus is always the same: fast iteration without sacrificing traceability or reliability.
    cta_text: "Read the blog"
    cta_href: "/blog/"
    thumb: /assets/images/threads/agentic.png
    thumb_alt: "Workflow diagram for reliable AI-assisted scientific tooling"
---

{% include hero.html %}

Below is the work organized into threads, each centered on a different class of problem. The boundaries blur more than the headings suggest.

## The work

{% for t in page.threads %}
  {% include thread-card.html thread=t %}
{% endfor %}

{% include recent-posts.html %}