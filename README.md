<div align="center">

# Paper X-Ray

**A deep-reading skill that reconstructs how a paper was actually thought up — not what its abstract says.**

[中文文档](./README.zh-CN.md) · [Skill](./SKILL.md) · [Showcase](#showcase)

![Skill](https://img.shields.io/badge/skill-paper--xray-c1502e)
![Prompt](https://img.shields.io/badge/prompt-verbatim_15_sections-2e7d4f)
![Outputs](https://img.shields.io/badge/outputs-markdown__html-58C4DD)
![Agent](https://img.shields.io/badge/agent-Claude_Code-d97757)
![License](https://img.shields.io/badge/license-MIT-8a8172)

![Paper X-Ray banner](./assets/hero-banner.png)

</div>

## Overview

Most paper explanations restate the paper. Paper X-Ray recovers what the paper left out: the specific scene where prior methods failed, the bet the authors placed, which designs carry the result and which are decoration, what each symbol looks like on a concrete example, and where the authors are confident versus bluffing. The reader should finish understanding the paper more deeply than from reading the original ten times.

The method combines a Hinton-style voice (plain language, mechanisms over adjectives, honest about weak explanations) with a 3Blue1Brown-style exposition (show first, then compute; one idea per figure; consistent color per symbol).

## Features

- **Author reconstruction** — identifies the structural failure behind the work, the authors' strongest card, and the evidence for it.
- **Concrete mathematics** — every symbol ships with shape and meaning; every key formula is preceded by its purpose and followed by a hand-computable micro-example.
- **Full worked examples** — multi-round traces with real state, run on both the paper's method and the baseline, down to the step where the baseline breaks.
- **Skeptical review** — hyperparameters, ablations, baselines, leakage, cost, and scope are checked; missing information is stated as missing, never papered over.
- **Two delivery branches** — `md` for a long-form Markdown document, `html` for a self-contained interactive page (KaTeX, sliders, step-through traces, SVG/Canvas).
- **Paper-type adaptation** — emphasis shifts for methods, theory, systems, empirical studies, agent/LLM pipelines, and datasets.

## Showcase

The complete prompt, rendered as paginated A4 sheets for presentation and sharing:

![A4 showcase page](./assets/showcase-a4.png)

## Installation

Copy `SKILL.md` into your skills directory:

```bash
mkdir -p ~/.claude/skills/paper-xray
cp SKILL.md ~/.claude/skills/paper-xray/SKILL.md
```

## Usage

1. Provide the paper: a local PDF, an arXiv identifier or link, or pasted text. Attach public code and the original figure directory when available — code takes precedence over text, figures are referenced by absolute path.
2. Select the delivery branch: `md` for the text edition, `html` for the interactive visual edition. If neither is specified, the skill asks once.
3. The skill reads the full text including appendices, footnotes, and captions, then writes the document section by section. Long documents are appended incrementally and never compressed to fit a single response.

## One-Line Agent Prompt

To have your own agent install this project, send it exactly this:

```text
Install SKILL.md from the paper-xray repository as a skill named paper-xray into my agent skills directory and confirm it is registered and callable.
```

## Repository Layout

```text
paper-xray/
├── SKILL.md                  # The complete skill prompt (verbatim, 15 sections + delivery rules)
├── README.md                 # This file
├── README.zh-CN.md           # 中文文档
└── assets/
    ├── hero-banner.png       # Project banner
    └── showcase-a4.png       # A4 showcase preview
```

## License

MIT. See [LICENSE](./LICENSE).
