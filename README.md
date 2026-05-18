# agugonrey.github.io

Personal site of **Agustin Gonzalez-Reymundez** — AI Scientist working on drug-target nomination, multi-omic ML, and agentic tooling for scientific workflows.

**Live site:** [https://agugonrey.github.io](https://agugonrey.github.io)

## Sections

- [Home](https://agugonrey.github.io/) — three-thread overview (drug-discovery AI / methods & packages / agentic tooling)
- [Papers](https://agugonrey.github.io/papers/) — full publication list, grouped by year
- [Packages](https://agugonrey.github.io/packages/) — R/Python packages and companion code repos (MOSS, eCV, …)
- [Blog](https://agugonrey.github.io/blog/) — posts and external writing (Eclipsebio, personal)
- [CV](https://agugonrey.github.io/cv/) — career history + downloadable resume
- [Now](https://agugonrey.github.io/now/) — what I'm working on this month
- [Google Scholar](https://scholar.google.com/citations?user=iM7Q6MsAAAAJ&hl=en)

## How this site is built

Static site generated with [Jekyll](https://jekyllrb.com/) and served by GitHub Pages.

The content pages (`/papers/`, `/packages/`, `/cv/`, `/blog/`) are *generated* from a structured experience store maintained in a separate (private) toolchain — the same store that powers tailored resumes and cover letters for job applications. The render step is deterministic and idempotent: publishing a new paper or package is one append in the store, and both the resume and this site update on the next render.

The toolchain itself is the subject of [this post](https://agugonrey.github.io/blog/tailored-resume-pipeline-claude-code/).

## Layout

```
_config.yml       Jekyll config (site title, baseurl, permalinks)
_layouts/         HTML templates (default page, blog post)
_posts/           Hand-written blog posts (Markdown + front matter)
assets/css/       Minimal CSS — text-first, no JS, dark-mode aware
index.md          Landing page (hand-written)
now.md            /now page (hand-written, dated)
papers.md         Generated from the experience store
packages.md       Generated from the experience store
cv.md             Generated from the experience store
blog/index.md     Generated; combines _posts/ with external posts from the store
```

## Contact

- LinkedIn: [agustin-gon-rey](https://www.linkedin.com/in/agustin-gon-rey/) — best for first contact
- GitHub: [@agugonrey](https://github.com/agugonrey)
