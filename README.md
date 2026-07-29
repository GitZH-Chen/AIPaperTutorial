# AI-Assisted Research Framework

This project is a practical guide to AI-assisted research. It covers the full lifecycle from ideas and experiments to submission, rebuttal, camera-ready preparation, and release. The repository also includes two practical writing resources: [`Tutorial.pdf`](Tutorial.pdf) and [`Paper_Workflow.md`](Paper_Workflow.md).

## Introduction

In the current era, conducting research without AI assistance is like using an abacus in the age of computers. Researchers should actively embrace AI as a research tool. Many AI research frameworks already exist, but no generic framework can fit everyone because research needs are highly individual. Fortunately, rapid advances in agent such as Codex make it increasingly easy to build a personal research skill set or even platform. This document offers one possible framework, not a universal solution.

Every researcher should develop and continuously refine personal skills for different research stages. These skills should encode individual workflows, tools, standards, corrections, and reusable lessons, while allowing AI to access the relevant project context. This repository deliberately does not provide a set of skills for every research node. It only shows how a complete research lifecycle can be divided and organized. Each researcher should adapt it to their own needs.

## Overall Research Framework

Here is reference structure:

```text
<project-root>/
├── AGENTS.md
├── X_Instructions/
│   ├── README.md
│   ├── Lessons/
│   │   ├── 1_Ideation.md
│   │   ├── 2_Experiments.md
│   │   ├── 3_Writing.md
│   │   ├── 4_Rebuttal.md
│   │   └── 5_Finalization.md
│   ├── 0_Aux.md
│   ├── 0_Aux/
│   │   ├── Shared-Rules.md
│   │   └── <Venue-Year>.md
│   ├── 1_Code.md
│   ├── 1_Code/
│   │   ├── Code-and-Server-Map.md
│   │   ├── Dataset-Map.md
│   │   └── <Codebase-or-Workflow>.md
│   ├── 2_TheoriesAndExperimentsLog.md
│   ├── 2_TheoriesAndExperimentsLog/
│   │   ├── Record-Organization.md
│   │   └── <Evidence-Source>.md
│   ├── 3_Submission.md
│   ├── 3_Submission/
│   │   ├── Shared-Rules.md
│   │   └── <Venue-or-Project>.md
│   ├── 4_Rebuttal.md
│   ├── 4_Rebuttal/
│   │   ├── Shared-Rules.md
│   │   └── <Venue-Year>.md
│   ├── 5_Release_code.md
│   └── 5_Release_code/
│       └── Release-Checklist.md
├── 0_Aux/
├── 1_Code/
├── 2_TheoriesAndExperimentsLog/
├── 3_Submission/
├── 4_Rebuttal/
└── 5_Release_code/
```

| Component | Directory | Purpose |
| --- | --- | --- |
| Project instructions | `X_Instructions/` | Systematic, project-specific instructions or skills for each stage. |
| 0. Preparation | `0_Aux/` | Guidelines, papers, notes, and early drafts. |
| 1. Implementation | `1_Code/` | Code. |
| 2. Theory and experiment records | `2_TheoriesAndExperimentsLog/` | Theoretical derivations and experiment records. |
| 3. Submission | `3_Submission/` | Manuscripts. |
| 4. Rebuttal | `4_Rebuttal/` | Reviews and rebuttal. |
| 5. Finalization | `5_Release_code/` | Camera-ready checks and reviewed public artifacts. |

The purpose of this structure is to make the entire project accessible from any research stage, so an agent does not treat each task in isolation. During rebuttal, for example, the agent should see the manuscript, code, theory and experiment records, submitted versions, reviewer comments, and response history, rather than only a review question or the paper itself. This cross-stage context enables consistent and evidence-based decisions.

## Two Writing Resources

- [`Tutorial.pdf`](Tutorial.pdf) covers LaTeX organization, references, equations, submission, rebuttal, tools, papers, and code.
- [`Paper_Workflow.md`](Paper_Workflow.md) explains a human-in-the-loop workflow for AI-assisted paper and rebuttal writing. AI produces drafts, while the researcher supplies context, verifies claims, rewrites, and iterates.

You may also be interested in [WritingAIPaper](https://github.com/hzwer/WritingAIPaper).
