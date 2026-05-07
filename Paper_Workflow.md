# 使用 AI 完成体力式论文写作：Human-in-the-loop 的顶会顶刊工作流

这份文档记录一个面向 AI 顶会顶刊论文的现代化写作工作流。这里的“体力式论文写作”不是指写作不需要思考，而是指把已经想清楚的内容交给 AI 执行。判断论文要讲什么、claim 应该多强、证明路线是否成立、实验是否足够，是人的智力劳动；整理 LaTeX、展开草稿、统一符号、检查语法、清理 BibTeX、根据已有材料组织 rebuttal，是 AI 可以承担的体力劳动。核心思想是：人完成智力性工作，AI 完成体力性工作，并用 [`AI-Research-Skills`](https://github.com/GitZH-Chen/AI-Research-Skills) 中的两个 agent skill 分别负责主论文写作和 OpenReview rebuttal。

全文分为四节：

- [使用 AI 完成体力式论文写作：Human-in-the-loop 的顶会顶刊工作流](#使用-ai-完成体力式论文写作human-in-the-loop-的顶会顶刊工作流)
  - [1. 整体工作流简介](#1-整体工作流简介)
  - [2. 前情提示](#2-前情提示)
  - [3. 写作：使用 `ai-paper-writing`](#3-写作使用-ai-paper-writing)
    - [3.1 熟读 5 到 20 篇紧密相关论文](#31-熟读-5-到-20-篇紧密相关论文)
    - [3.2 创建项目](#32-创建项目)
    - [3.3 具体写作](#33-具体写作)
    - [3.4 参考文献与 bib check](#34-参考文献与-bib-check)
    - [3.5 AI review 与最后检查](#35-ai-review-与最后检查)
    - [3.6 最终成品标准](#36-最终成品标准)
  - [4. Rebuttal：使用 `openreview-rebuttal`](#4-rebuttal使用-openreview-rebuttal)

## 1. 整体工作流简介

本教程以 `Codex + VS Code + LaTeX Workshop + Overleaf Git` 为例，说明如何把 AI agent 纳入 AI 顶会顶刊论文写作。这个组合的分工很直接：Overleaf 负责多人协作和最终编译，Git 负责把 Overleaf 项目同步到本地，VS Code 和 LaTeX Workshop 负责本地编辑、编译和查错，Codex 负责在本地项目中读取上下文并修改 `.tex`、`.bib`、`.md` 等文件。这里的工具组合不是唯一选择。只要平台支持结构化的 skill 或类似的 system instruction，并且能够读写本地 LaTeX 项目，就可以采用同样的流程。例如，可以把 Codex 换成 Claude Code CLI、Cursor 或其他命令行 agent 平台。

这个 workflow 的核心诉求有两个。第一，要使用结构化 skill，而不是每次临时告诉 AI “帮我润色一下”。这里使用 [`AI-Research-Skills`](https://github.com/GitZH-Chen/AI-Research-Skills) 中的 `ai-paper-writing` 和 `openreview-rebuttal`，分别约束主论文写作和 rebuttal 写作。第二，要通过 Overleaf Git 连接本地和云端协作环境。这样既能保留 Overleaf 的多人协作优势，又能在本地使用 AI agent 做结构化写作、批量修改、版本管理和投稿前检查。核心就是实现 OpenAI Prism 的终极版：多人协作、AI 结构化指令和丰富上下文系统的结合。

整体流程如下：

```text
  -> Step 1: 熟读 5 到 20 篇紧密相关论文
  -> Step 2: 创建 Overleaf 项目
  -> Step 3: Git 到本地 VS Code + LaTeX Workshop
  -> Step 4: 按照 ai-paper-writing 写作，并使用本地 Markdown 笔记作为核心素材
  -> Step 5: 使用 AI review 做投稿前检查
  -> Step 6: 使用 openreview-rebuttal 写 rebuttal
```

## 2. 前情提示

判断体力劳动和智力劳动的准则很简单：任何你不知道怎么做的事情，都是智力劳动；任何你已经知道怎么做、只是需要花时间执行的事情，才是体力劳动。以数学推导为例，如果你不知道证明路线，无法验证证明细节，那么推导本身就是智力劳动，不能指望 agent 替你完成。相反，如果你已经知道证明路线，只是需要把中间代数步骤展开、把符号写整齐、把 LaTeX 整理成论文格式，那么这部分就是体力劳动，适合交给 agent。

我把这一套方法论分享给不同的人之后，发现有些人写出来的文本 AI 味很浓。差别不在工具本身，而在使用者是否已经想清楚了文章布局及技术细节，只是不想花时间展开细节，AI agent 就能显著加速写作。如果这些东西还没有想清楚，就应该先停下来自己琢磨，或者和 AI 进行多轮高强度讨论（GPT Thinking 最高模式）。否则 agent 只会输出车轱辘话。有 AI 味的论文，意味着作者对论文内容不清楚。

## 3. 写作：使用 `ai-paper-writing`

本节整理主论文写作阶段的具体流程，对应整体 workflow 中的 Step 1 到 Step 5。核心是 human-in-the-loop：你告诉 AI 怎么写，它按照你的口述草稿，整理语言并生成 LaTeX。本地 project 中应包含 Markdown 笔记，例如核心方法、技术细节、关键推导、实验结果和失败案例。这些笔记是写作素材，agent 负责组织和展开，不负责自由发挥。

**非常重要：AI 做的任何修改，作者都必须仔细复核一遍。**

### 3.1 熟读 5 到 20 篇紧密相关论文

开始写作前，先选出和自己工作最接近的 5 到 20 篇论文。这些论文是你的素材库。写作中遇到很多具体问题，都可以先回到这个素材库里找答案，例如论文整体如何布局、表格如何组织、图片如何排版、实验如何叙述、related work 如何分类。可以把这些论文和相关问题一起交给 AI，让它帮你检索可能相关的参考位置，但必须定位到原文。AI 只是帮你把相关参考找出来，最终要自己回到原文检查上下文和具体写法。

这些论文也是写作时的内容素材。例如写 related work 时，可以先口述相关文章的总结，再告诉 AI 原始 PDF 或 Markdown 笔记的位置，让它根据你的口述和材料写入文章。

### 3.2 创建项目

选择目标 venue 的官方模板，在 Overleaf 中创建项目。使用 Overleaf 的 Git 功能，把项目 clone 到本地。之后的日常工作方式是：

```text
Overleaf project
  <-> Git sync
  <-> VS Code + LaTeX Workshop + Codex
```

`VS Code + LaTeX Workshop` 不是必要组件，它主要是给人阅读用。更轻量的做法是直接使用 CLI agent 在本地修改文件，然后自动 Git push 上传到 Overleaf，从而实现“本地 AI 修改，Overleaf 同步更新，人在 Overleaf 编辑”。这是师相龙提出的方案，在此表示感谢。

写论文阶段使用 `ai-paper-writing`。第一步是在本地 LaTeX 项目根目录执行预定义命令 `init latex`，让 skill 初始化写作环境和编译配置。初始化后，一个典型项目结构可以是：

```text
paper-project/
├── AGENTS.md
├── main.tex
├── preamble.tex
├── ref.bib
├── Sec/
│   ├── 0_abstract.tex
│   ├── 1_introduction.tex
│   ├── 2_related_work.tex
│   ├── 3_method.tex
│   ├── 4_experiments.tex
│   └── 5_conclusion.tex
├── Figs/
│   ├── teaser.pdf
│   ├── method_overview.pdf
│   └── results.pdf
├── Aux/
│   ├── Method_Notes.md
│   ├── Derivations.md
│   ├── Experiments.md
│   ├── Related_Work.md
│   └── Papers/
│       ├── paper_a.pdf
│       └── paper_b.pdf
├── .latexmkrc
├── .vscode/
│   └── settings.json
└── .gitignore
```

这种结构的好处是每个章节对应一个 `.tex` 文件，因此可以逐章节写作。典型 LaTeX 组织方式可以参考我的文章 [Hyperbolic Busemann Neural Networks](https://arxiv.org/abs/2602.18858)。arXiv 论文通常可以下载 LaTeX 源码，使用 Chrome 插件 `Open in Overleaf` 会更方便，能够直接把 arXiv 源码打开到 Overleaf 中参考。

### 3.3 具体写作

具体写作时，按照章节文件逐个推进，例如先写 `Sec/1_introduction.tex`，再写 `Sec/3_method.tex`。写每个段落之前，先口述这一段的草稿，再把足够的上下文交给 Codex，包括 `Aux/` 中的相关 PDF 和 notes。Codex 根据你的口述和材料生成草稿，人再检查、修改，并继续要求它迭代。不要神话 AI，**有些情况下，即使你已经说得非常清楚，AI 写得还是不到位**。这很正常，此时不要继续让它自由发挥，而应该由人先写一个粗糙草稿，再让 AI polish。

每完成一个章节之后，使用 `ai-paper-writing` 中的 `grammar check` 做语法和格式检查。这个命令的目的不是重新润色或改写文章，而是修正 grammatical errors，并检查 LaTeX 命令是否符合预设格式规则。因此适合在每个章节稳定后执行一次。

每个章节的基本工作流如下：

```text
  -> 给 AI 下指令和上下文
  -> AI 写作
  -> 人检查和修改
  -> 多轮迭代
  -> 章节完成，grammar check
```

### 3.4 参考文献与 bib check

避免让 AI 生成参考文献。虚假引用或错误引用的风险非常大，后果也很严重，我本人没有使用过 AI 生成参考文献。更方便的方式是直接采用相关 arXiv 文章源码中的 BibTeX 作为起点，但这样必须用工具检查是否存在虚假或错误参考文献，确实有人由此导致 desk rejection。参考文献可以用专门工具检查，例如 [`True Cite`](https://www.wispaper.ai/agents/true-cite)。

另一件事是参考文献格式化。所有 BibTeX 条目应该统一采用一种格式，例如 venue 是否缩写、是否保留 volume/number/pages，title 中的专有名词要用 `{}` 保持大写。最简单的方式是使用 `ai-paper-writing` 中的 `bib check`。这个命令只改格式，不改参考文献内容，也不应该新增或替换 citation。

不管采用什么方式管理参考文献，最后都应该再用参考文献检查工具做一次检查，确认没有虚假参考文献、错误题名、错误作者或 citation 与原文不匹配的问题。

### 3.5 AI review 与最后检查

投稿前可以在网上找一些结构化的 review prompt 或 AI review 工具，让 AI 按审稿人视角检查自己的文章。这类指令和网址非常多，也可以在小红书等平台搜索。AI review 的作用是给出一份风险清单，帮助你发现明显问题。AI 给的意见仅供参考，有则改之，无则加勉。

最后还需要让 Codex 做一次最后检查，包括对全文执行 `grammar check`、对参考文献执行 `bib check`，以及根据官方模板和 guideline 检查 PDF/LaTeX。

### 3.6 最终成品标准

在 `ai-paper-writing` 的帮助下，最终成品还需要满足更高一级的检查标准：公式符号和 notation 风格完全一致，行文和排版风格完全一致，`\cref` 等交叉引用正确，图表编号和正文引用一致，文章没有 AI 味，格式符合目标 venue 的投稿要求。

## 4. Rebuttal：使用 `openreview-rebuttal`

TODO：rebuttal 的原理和论文写作一样，核心是给足够的上下文，并使用 `openreview-rebuttal`。rebuttal 材料可以直接放在当前 paper project 中。
