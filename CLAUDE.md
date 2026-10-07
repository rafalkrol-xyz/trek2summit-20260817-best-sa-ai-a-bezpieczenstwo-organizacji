# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Not a software project — it is the source for a **conference talk**: „AI a bezpieczeństwo organizacji" (AI and organizational security), delivered in Polish by Rafał Król (Head of AWS Technologies, Trek2Summit) at an internal BEST S.A. security conference on **2026-08-18**. 45 minutes including Q&A, audience of ~200 online + ~30 on-site with medium-to-high AI literacy. BEST S.A. is migrating workloads to AWS while employees use Microsoft 365 / Copilot — hence the deliberate AWS + Azure balance in the content.

The single deliverable is `presentation.md`, a [presenterm](https://github.com/mfontanini/presenterm) terminal slideshow (presenterm 0.16.1 installed via Homebrew).

## Commands

```bash
presenterm presentation.md              # render/preview
presenterm -p presentation.md           # presentation mode
presenterm --validate-overflows presentation.md   # check slides don't overflow the viewport
presenterm -e -o out.pdf presentation.md # export PDF
presenterm --list-comment-commands      # authoritative list of supported <!-- --> directives
```

`--validate-overflows` and normal rendering need a real TTY (image protocols fail with "Device not configured" when piped) — ask the user to run these with `! presenterm ...` rather than capturing output yourself.

Tooling preferences carried over from `.kiro/steering/project.md`: use `rg` for content search and `fd` for finding files, via the terminal, instead of generic grep/find.

## `.kiro/specs/` — out of scope

The deck was originally generated from a Kiro spec in `.kiro/specs/best-sa-ai-security-presentation/` (`requirements.md`, `design.md`, `tasks.md`). **Ignore those files.** They are Kiro's to maintain: don't read them for constraints, don't treat their acceptance criteria as a contract, don't update task checkboxes, and don't retrofit `presentation.md` to match them. `presentation.md` itself is the source of truth for what the talk contains.

`.kiro/steering/` *is* tracked in git and does apply — it holds the repo's tool preferences and the image SOP below. The rest of `.kiro/` is local-only (see `.gitignore`).

## presenterm conventions used here

- **Slide separator**: `<!-- end_slide -->` on its own line. `---` is reserved for the YAML front matter (title / sub_title / author), which presenterm renders as the title slide.
- **Speaker notes**: must be `<!-- speaker_note: ... -->`. A bare `<!-- ... -->` comment is *not* a speaker note — it renders as nothing and silently does nothing. The deck currently has no speaker notes.
- **Incremental reveal**: `<!-- pause -->` is used heavily (84 occurrences) — most threat slides reveal in 3–4 beats, so a slide's raw line count overstates what is on screen at once.
- **Comparisons**: `<!-- column_layout: [1, 1] -->` + `<!-- column: N -->` + `<!-- reset_layout -->` (used for traditional-vs-AI phishing).
- **Section transitions**: each section ends with an italic arrow line previewing the next topic, e.g. `→ _Zaczynamy od krajobrazu zagrożeń…_`.

## Content conventions of the deck

These are the editorial choices `presentation.md` already follows — match them when writing new slides:

- **Polish prose, English technical terms.** Keep "prompt injection", "deepfake", "Shadow AI", "vishing" and product names (AWS, Bedrock, Copilot, Purview) in English. Don't define basic AI concepts — the audience already uses Copilot daily.
- **Expert, non-promotional tone.** Factual analysis and documented incidents, no vendor sales pitch.
- **Every incident cites a verifiable public source.** `research/incidents.md` is the fact base: 11 incidents across 6 categories, each with organization, year, category, description, impact and checked source URLs. Add new incidents there first, then cite them on a slide.
- **AWS and Azure stay roughly balanced**, and a platform-specific tool is named alongside its counterpart on the other platform (Bedrock Guardrails ↔ Azure AI Content Safety, Macie ↔ Purview, and so on).
- **Threats first, then empowerment.** Roughly 60% of slides cover threats and 40% cover defense, best practices and closing. The ending points employees to PBI (Pion Bezpieczeństwa Informacji) framed as a partner, not an enforcement body.
- `my_notes.md` is the presenter's untracked scratchpad of ideas not yet in the deck (pre-AI fraud cases, EU AI Act Article 50, Bedrock Guardrails / ZDR links). Treat it as a backlog of candidate material, not as content.

## Images

Memes and photos live in `images/` and are referenced with relative paths: `![mem](images/prompt-injection-via-email-meme.png)`. Most images in the directory are unused so far — check before sourcing a new one.

Before staging any image, apply the SOP in `.kiro/steering/image-optimization.md` using macOS `sips`:

```bash
sips -g pixelWidth -g pixelHeight images/<file>          # inspect
sips --resampleHeightWidthMax 1920 images/<file>          # longest side > 1920px
sips -s formatOptions 80 images/<file>.jpeg               # JPEG > 500KB
sips -s format jpeg -s formatOptions 80 images/<f>.png --out images/<f>.jpeg   # photo PNG > 500KB
```

## Current state

`presentation.md` is content-complete: 35 slides across opening → threat landscape → eight specific threats → transition → best practices → closing + Q&A. No speaker notes yet. Only 2 of the ~20 images in `images/` are used, so check the directory before sourcing anything new.

Commit messages are written in English (imperative, often "Write Section N: … (slides X-Y)") even though the content is Polish.
