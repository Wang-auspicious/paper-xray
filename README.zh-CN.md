<div align="center">

[English](./README.md) · **简体中文**

# Paper X-Ray

**把一篇论文还原成作者真实的思考过程，而不是复述它的摘要。**

A deep-reading skill that reconstructs how a paper was actually thought up, not what its abstract says.

![Skill](https://img.shields.io/badge/skill-paper--xray-c1502e)
![Outputs](https://img.shields.io/badge/输出-Markdown_·_交互式_HTML-58C4DD)
![Annotate](https://img.shields.io/badge/标注层-划线_笔记_反馈-2e7d4f)
![Agent](https://img.shields.io/badge/适配-Claude_Code-d97757)
![License](https://img.shields.io/badge/协议-MIT-8a8172)

![Paper X-Ray 横幅](./assets/hero-banner.png)

</div>

---

## 它做什么

一篇论文是几个月的工作被压缩成十几页之后的样子。方法部分的顺序是教学顺序，引言里的故事是事后整理的。真正决定成败的判断，比如作者看到了什么、在哪里卡住、第一版怎么失败、哪个超参数在防哪种失效，大多没有写进去。

Paper X-Ray 把这些还原出来。给它一篇论文，或者一个主题，它会：

- **还原作者的底气和弯路**：前人方法在什么具体场景下失效，作者凭什么相信能做成，措辞的强弱暴露了哪里有把握、哪里在虚；
- **站在实验台上讲**：每讲完一个机制，接一段第一版会怎么坏、负责人先跑哪个诊断、补丁和代价；
- **把数学讲到能手算**：每个符号给形状和含义，关键公式配一个能用纸笔验算的小例子；
- **怀疑式核对**：拿数字和噪声比，核对表格里的数是否自洽，论文没交代的就写没交代；
- **标注证据等级**：每条推断标【文中有据】【推断】【猜测】，推测可以大胆，但不写成事实。

讲法是 Hinton 式的直白加 3Blue1Brown 式的先看见再计算。输出有两种：长篇 Markdown，或一个单文件的交互式 HTML。

## 三份新 Demo

都是单个 HTML 文件，下载后直接用浏览器打开，不需要构建和服务器。

| Demo | 类型 | 看点 |
|---|---|---|
| [**大模型只训一次，所有决定都在小模型上做完**](./demos/llm-pretraining-xray/llm-pretraining-xray.html) · [在线打开](https://raw.githack.com/Wang-auspicious/paper-xray/master/demos/llm-pretraining-xray/llm-pretraining-xray.html) | 主题模式：基座模型的完整训练流程 | 以 2025 到 2026 年的报告为主（DeepSeek-V3.2、Kimi K2、Qwen3、Qwen3-VL、Gemini 2.5、ScaleRL）。从算力预算、数据、分词器、结构、并行、优化器、故障，一路讲到原生多模态、强化学习的缩放曲线、渲染奖励和模型怎样学会说人话。12 张交互图，其中分词器是在这页正文上现场训练的 |
| [**LayerNorm 的位置决定初始化时的梯度尺度**](./demos/preln-xray/preln-xray.html) · [在线打开](https://raw.githack.com/Wang-auspicious/paper-xray/master/demos/preln-xray/preln-xray.html) | AI 论文：Pre-LN（Xiong et al., ICML 2020） | 用一个可运行的最小实现复现了引理的数值，指出附录里漏掉的一个雅可比因子、一处写反的速度数字，以及调度和归一化位置混在一起的对照 |
| [**光电流的慢弛豫和碘空位的一次跳跃共用一个 0.6 eV**](./demos/perovskite-ion-xray/perovskite-ion-xray.html) · [在线打开](https://raw.githack.com/Wang-auspicious/paper-xray/master/demos/perovskite-ion-xray/perovskite-ion-xray.html) | 化学与材料：Eames et al., Nat. Commun. 2015 | 从 0.6 eV 的活化能手算到秒级的器件响应，检查计算势垒和阿伦尼乌斯斜率对上之后还要对上什么 |

## 图

下面是大模型那份 demo 里的局部截图。每张图都由同一套图语言画出：颜色表示角色而不是装饰，框里只写名字，连线只走横竖，图里不放标题和图例。

![大模型 demo 里的六张图](./assets/llm-figures.jpg)

从左到右、从上到下：拖动算力看 isoFLOP 曲线的谷底怎么移动；把 Kaplan 的 0.835 逐步修正到 Chinchilla 的 0.497；在本页正文上训练的字节级 BPE，拖动合并次数看切分怎么变；把 Llama 3 8B 的 80 亿个参数逐层拆开；外挂式和原生式两条多模态路线（暗色）；拖动答对个数，看 GRPO 的优势怎么分配（暗色）。

总览从全景点进细节，每一步都列出三次真实训练的选择，以及做这个决定所依据的小实验：

![训练流水线全景图](./assets/llm-map.jpg)

滑块一定驱动一张会变的图，而不是只改表格里的数字。比如每帧给多少个 token，决定一百万 token 的上下文能装多长的视频：

![每帧 token 数与视频时长](./assets/llm-video.jpg)

## 标注层

HTML 自带标注层，读者什么都不用装。打开 ✎，选中文字就能划线、写笔记，或者反馈**不懂**、**啰嗦**、**已懂**。笔记显示在右侧边栏，用细线连回原文。

![标注层：划线和边注](./assets/llm-annotations.png)

点 ⤓ 把标注写回这个 HTML 文件本身。下一次调用 skill 时，它会读这些标注：标了**不懂**的概念下次换一个角度重讲，同一类段落反复被标**啰嗦**就默认写短，标了**已懂**的以后一句话带过。读者档案和日志存在本地的 `user/` 目录里，不进仓库。

## 安装

**一句话提示词**：把这句原样发给你的 Agent。

```text
把 https://github.com/Wang-auspicious/paper-xray 克隆到我的 Agent Skills 目录下的 paper-xray 文件夹，并确认 Skill 注册成功、可被调用。
```

**Git clone**（推荐，参考文件和组件库一起带上）：

```bash
git clone https://github.com/Wang-auspicious/paper-xray.git ~/.claude/skills/paper-xray
```

Windows 上的 Skills 目录是 `C:\Users\<你>\.claude\skills\paper-xray`。只复制 `SKILL.md` 也能用，但 HTML 交付需要 `references/` 里的页面骨架和图组件。

## 用法

```text
/paper-xray D:/papers/rope.pdf
/paper-xray 2104.09864 html
/paper-xray 大模型的完整训练流程 html
```

1. **给材料**：本地 PDF、arXiv 编号或链接、粘贴的文本，或者一个主题。有公开代码就一起给，代码里的归一化、预热、数据过滤有时才是效果的真正来源。
2. **选形式**：`md` 是长篇文字版，`html` 是交互版；不指定时会问一次。
3. **等它读完**：它会通读正文、附录、脚注和图注，再分节写完，不会为了单次输出长度压缩内容。主题太大时，先给一份分篇地图。

第一次使用时会弹一次简短问卷，确定数学和动手的程度，之后按档位调整写法。

## 仓库结构

```text
paper-xray/
├── SKILL.md                       # 中文规格：工作流程、写作要求、主题模式、读者档案
├── VERSION
├── references/
│   ├── SKILL.en.md                # 英文规格
│   ├── html.md                    # HTML 交付规格：页面、图的视觉语言、交互、标注层、自检
│   ├── reader-kit.html            # 页面骨架：版式、目录、明暗、标注层、XRAY.lint
│   └── figure-kit.html            # 图组件：f.row / f.zoom / FK.plot / FK.tokens / FK.heat / FK.iso / FK.lint
├── demos/
│   ├── llm-pretraining-xray/      # 主题模式 demo，含正文、图脚本、分词器训练脚本和构建脚本
│   ├── preln-xray/                # Pre-LN 论文 demo，含最小复现脚本
│   └── perovskite-ion-xray/       # 钙钛矿离子迁移 demo，含手算脚本
├── assets/                        # README 用图
├── README.md
├── README.zh-CN.md
└── LICENSE
```

## Star History

如果它帮你省掉了一次重读，点个 star 能让更多人看到。

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=wang-auspicious/paper-xray&type=Date&theme=dark&v=20261023">
  <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=wang-auspicious/paper-xray&type=Date&theme=light&v=20261023">
  <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=wang-auspicious/paper-xray&type=Date&theme=light&v=20261023">
</picture>

## 协议

MIT，见 [LICENSE](./LICENSE)。
