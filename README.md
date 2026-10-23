<div align="center">

**English** · [简体中文](./README.zh-CN.md)

# Paper X-Ray

**A deep-reading skill that reconstructs how a paper was actually thought up, not what its abstract says.**

把一篇论文还原成作者真实的思考过程，而不是复述它的摘要。

![Skill](https://img.shields.io/badge/skill-paper--xray-c1502e)
![Outputs](https://img.shields.io/badge/outputs-Markdown_·_interactive_HTML-58C4DD)
![Annotate](https://img.shields.io/badge/annotation_layer-highlight_note_feedback-2e7d4f)
![Agent](https://img.shields.io/badge/agent-Claude_Code-d97757)
![License](https://img.shields.io/badge/license-MIT-8a8172)

![Paper X-Ray banner](./assets/hero-banner.png)

</div>

---

## What it does

A paper is months of work compressed into a dozen pages. The method section is in teaching order, and the introduction tells a story assembled after the fact. Most of the judgment calls that decided the outcome never make it to the page: what the authors saw, where they got stuck, how the first version failed, which oddly specific hyperparameter is guarding against which failure.

Paper X-Ray recovers that. Give it a paper, or a topic, and it will:

- **Reconstruct the bet and the detours.** The concrete scene where prior methods break, what gave the authors confidence, and what the strength of their wording reveals about where they are sure and where they are bluffing.
- **Write from the lab bench.** After every mechanism, a passage on how the first version fails, the cheapest diagnostic a lead would run, and the patch with its cost.
- **Make the math hand-checkable.** Every symbol gets its shape and meaning; every key formula gets a small example you can verify on paper.
- **Read skeptically.** Numbers are checked against noise and against each other; what the paper does not report is marked as unreported.
- **Grade its evidence.** Every inference is tagged as stated in the paper, inferred, or guessed. Bold guesses are fine; guesses dressed as facts are not.

The voice is Hinton-plain and the exposition is 3Blue1Brown-style: see it first, then compute it. Output is either a long-form Markdown document or a single-file interactive HTML page.

## Three new demos

Each is one HTML file. Download and open it in a browser; no build, no server. The demos are written in Chinese.

| Demo | Kind | What to look at |
|---|---|---|
| [**Big models are trained once; every decision is made on small ones**](./demos/llm-pretraining-xray/llm-pretraining-xray.html) · [open online](https://raw.githack.com/Wang-auspicious/paper-xray/master/demos/llm-pretraining-xray/llm-pretraining-xray.html) | Topic mode: the full training pipeline of a foundation model | Built mainly on 2025–2026 reports (DeepSeek-V3.2, Kimi K2, Qwen3, Qwen3-VL, Gemini 2.5, ScaleRL). Compute budgets, data, tokenizers, architecture, parallelism, optimizers and failures, through native multimodality, RL scaling curves, rendering rewards, and how a model learns to stop sounding like a model. Twelve interactive figures; the tokenizer is trained live on the page's own text |
| [**Where LayerNorm sits sets the gradient scale at initialization**](./demos/preln-xray/preln-xray.html) · [open online](https://raw.githack.com/Wang-auspicious/paper-xray/master/demos/preln-xray/preln-xray.html) | ML paper: Pre-LN (Xiong et al., ICML 2020) | A runnable minimal reimplementation reproduces the lemma's numbers and finds a Jacobian factor missing from the appendix, a swapped speed figure, and a comparison that confounds the schedule with the normalization |
| [**A slow photocurrent and a single iodide-vacancy hop share 0.6 eV**](./demos/perovskite-ion-xray/perovskite-ion-xray.html) · [open online](https://raw.githack.com/Wang-auspicious/paper-xray/master/demos/perovskite-ion-xray/perovskite-ion-xray.html) | Chemistry and materials: Eames et al., Nat. Commun. 2015 | Hand calculations from a 0.6 eV activation energy to device response in seconds, and what else must agree once a computed barrier matches an Arrhenius slope |

## Figures

Crops from the LLM demo. Every figure is drawn in one figure language: color marks a role rather than decorating, a box holds a name and nothing else, wires run only horizontally and vertically, and no figure carries a title or a legend.

![Six figures from the LLM demo](./assets/llm-figures.jpg)

Left to right, top to bottom: drag the compute budget and watch the bottom of the isoFLOP curve move; step Kaplan's 0.835 down to Chinchilla's 0.497 one correction at a time; a byte-level BPE trained on the page itself, re-segmenting as you drag the merge count; Llama 3 8B's eight billion parameters taken apart layer by layer; the bolt-on and native routes to multimodality (dark theme); GRPO advantages as you change how many of 16 answers are correct (dark theme).

The overview opens into detail. Each step lists what three real training runs chose and the small experiment that decision rested on:

![Overview of the training pipeline](./assets/llm-map.jpg)

A slider always drives a figure that changes, never just a number in a table. Here, tokens per frame decide how much video fits in a million-token context:

![Tokens per frame against video length](./assets/llm-video.jpg)

## Annotation layer

The HTML ships with its own annotation layer; readers install nothing. Turn on ✎, select text, and highlight it, write a note, or mark it as **lost**, **too long**, or **got it**. Notes sit in the right margin, tied back to the text by a thin line.

![Annotation layer with a highlight and a margin note](./assets/llm-annotations.png)

⤓ writes the annotations back into the HTML file itself. The next time the skill runs it reads them: a concept marked lost is explained again from a different angle, a kind of passage repeatedly marked too long gets shorter by default, and a concept marked got it is mentioned in one line from then on. The reader profile and the log live in a local `user/` folder that never enters the repository.

## Install

**One-line prompt**: paste this into your agent.

```text
Clone https://github.com/Wang-auspicious/paper-xray into a folder named paper-xray in my agent skills directory, then confirm the skill is registered and callable.
```

**Git clone** (recommended; brings the references and the figure kit along):

```bash
git clone https://github.com/Wang-auspicious/paper-xray.git ~/.claude/skills/paper-xray
```

On Windows the skills directory is `C:\Users\<you>\.claude\skills\paper-xray`. Copying only `SKILL.md` works for Markdown output, but HTML output needs the page skeleton and figure kit in `references/`.

## Usage

```text
/paper-xray D:/papers/rope.pdf
/paper-xray 2104.09864 html
/paper-xray the full training pipeline of a foundation model html
```

1. **Provide the material**: a local PDF, an arXiv identifier or link, pasted text, or a topic. Attach public code when there is some: normalization, warmup and data filtering that only exist in the code are sometimes where the results actually come from.
2. **Pick a format**: `md` for the long-form text, `html` for the interactive page. If you name neither, it asks once.
3. **Let it read**: it reads the body, appendices, footnotes and captions, then writes section by section without compressing to fit a single response. For a topic too big for one document, it first proposes a map of how to split it.

On first use it asks a short questionnaire about your math and hands-on background and adjusts the writing to match.

## Repository layout

```text
paper-xray/
├── SKILL.md                       # Chinese specification: workflow, writing rules, topic mode, reader profile
├── VERSION
├── references/
│   ├── SKILL.en.md                # English specification
│   ├── html.md                    # HTML delivery spec: page, figure language, interaction, annotation, self-checks
│   ├── reader-kit.html            # Page skeleton: layout, contents, themes, annotation layer, XRAY.lint
│   └── figure-kit.html            # Figure components: f.row / f.zoom / FK.plot / FK.tokens / FK.heat / FK.iso / FK.lint
├── demos/
│   ├── llm-pretraining-xray/      # Topic-mode demo with its body, figure code, tokenizer trainer and build script
│   ├── preln-xray/                # Pre-LN paper demo with the minimal reimplementation
│   └── perovskite-ion-xray/       # Perovskite ion-migration demo with the hand-calculation script
├── assets/                        # Images for this README
├── README.md
├── README.zh-CN.md
└── LICENSE
```

## Star History

If this saved you a reread, a star helps other people find it.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=wang-auspicious/paper-xray&type=Date&theme=dark&v=20261023">
  <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=wang-auspicious/paper-xray&type=Date&theme=light&v=20261023">
  <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=wang-auspicious/paper-xray&type=Date&theme=light&v=20261023">
</picture>

## License

MIT. See [LICENSE](./LICENSE).
