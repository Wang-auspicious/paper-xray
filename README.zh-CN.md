<div align="center">

# Paper X-Ray

**将一篇论文还原为作者真实的思考过程，而非复述其摘要的深度解读 Skill。**

[English](./README.md) · [Skill](./SKILL.md) · [展示](#展示)

![Skill](https://img.shields.io/badge/skill-paper--xray-c1502e)
![Prompt](https://img.shields.io/badge/prompt-15_节完整版-2e7d4f)
![Outputs](https://img.shields.io/badge/输出-Markdown_HTML-58C4DD)
![Agent](https://img.shields.io/badge/适配-Claude_Code-d97757)
![License](https://img.shields.io/badge/协议-MIT-8a8172)

![Paper X-Ray 横幅](./assets/hero-banner.png)

</div>

## 概述

多数论文解读复述论文。Paper X-Ray 还原论文未写出的部分：前人方法失效的具体场景、作者押注的底牌、承重的设计与装饰性的设计、每个符号在具体例子上的形态、作者有把握与心虚的位置。读者读完，对论文的理解应当超过反复阅读原文十遍。

方法结合 Hinton 式的写作语气（朴素语言、机制优先于形容词、对薄弱解释直言不讳）与 3Blue1Brown 式的讲解（先展示后计算、一图一事、一符号一色）。

## 功能

- **作者思路还原**——定位工作背后的结构性失败、作者最硬的底牌及其证据。
- **公式具体化**——每个符号首次出现即给出形状与含义；每个关键公式先说明目的，再给出可手算的微型实例。
- **完整推演**——携带真实状态的多轮追踪，在论文方法与基线上各走一遍，精确到基线出错的那一步。
- **怀疑式审读**——核查超参数来源、消融隔离性、基线对齐、数据泄露、代价与适用范围；缺失的信息明确标出缺失，不代为圆场。
- **两种交付分支**——`md` 输出 Markdown 长文；`html` 输出自包含交互网页（KaTeX、参数滑块、逐步播放、SVG/Canvas）。
- **按论文类型调整重心**——方法、理论、系统、实证分析、智能体/LLM 流程、数据集各有展开重点。

## 展示

完整 prompt 的 A4 分页渲染版，用于展示与分享：

![A4 展示页](./assets/showcase-a4.png)

## 安装

将 `SKILL.md` 复制至 Skills 目录：

```bash
mkdir -p ~/.claude/skills/paper-xray
cp SKILL.md ~/.claude/skills/paper-xray/SKILL.md
```

## 用法

1. 提供论文：本地 PDF、arXiv 编号或链接、粘贴正文均可。有公开代码与原图目录一并提供——代码效力高于正文，原图按绝对路径引用。
2. 选择交付分支：`md` 为文字版，`html` 为交互视觉版；未指定时 Skill 会询问一次。
3. Skill 通读全文（含附录、脚注、图注表注）后分节撰写文档。长文档分多次追加写完，不因单次输出长度压缩内容。

## 一句话 Agent 部署提示词

让自己的 Agent 部署本项目时，原样发送这一句：

```text
把 paper-xray 仓库中的 SKILL.md 安装为名为 paper-xray 的 Skill，放入我的 Agent Skills 目录，并确认注册成功、可被调用。
```

## 仓库结构

```text
paper-xray/
├── SKILL.md                  # 完整 Skill 提示词（15 节正文 + 交付规则，一字未删）
├── README.md                 # English documentation
├── README.zh-CN.md           # 本文件
└── assets/
    ├── hero-banner.png       # 项目横幅
    └── showcase-a4.png       # A4 展示页预览
```

## 协议

MIT，见 [LICENSE](./LICENSE)。
