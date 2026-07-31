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
| Project instructions | `X_Instructions/` | Systematic, project-specific instructions for each stage. |
| 0. Preparation | `0_Aux/` | Guidelines, papers, notes, and early drafts. |
| 1. Implementation | `1_Code/` | Code. |
| 2. Theory and experiment records | `2_TheoriesAndExperimentsLog/` | Theoretical derivations and experiment records. |
| 3. Submission | `3_Submission/` | Manuscripts. |
| 4. Rebuttal | `4_Rebuttal/` | Reviews and rebuttal. |
| 5. Finalization | `5_Release_code/` | Camera-ready checks and reviewed public artifacts. |

The purpose of this structure is to make the entire project accessible from any research stage, so an agent does not treat each task in isolation. During rebuttal, for example, the agent should see the manuscript, code, theory and experiment records, submitted versions, reviewer comments, and response history, rather than only a review question or the paper itself. This cross-stage context enables consistent and evidence-based decisions.

`X_Instructions/Lessons/` records recurring, generalizable problems found during actual use, together with their causes and verified corrections. These reusable lessons can then be incorporated into the relevant personal research skills, preventing the same mistakes and continuously improving the workflow.

## Rebuttal Evidence Workflow

A rebuttal usually has two stages. The initial stage answers the original reviews. The discussion stage handles reviewer follow-ups, narrower evaluation criteria, and newly requested analyses or experiments. Organize both stages around stable reviewer-question IDs so that later work remains connected to the original concern.

The internal evidence workflow is independent of the final response format:

```text
notes/
  Internal reasoning, question decomposition, derivations, experiment plans,
  and gaps identified during discussion
        │
        ▼
log/
  Commands, configurations, run records, raw outputs, failures, reruns,
  diagnostics, and aggregation evidence
        │
        ▼
Stable question-level records in the rebuttal evidence root
  Core settings, final tables, verified conclusions, limitations,
  and an evidence index
        │
        ▼
Authoritative response workspace
  Paste-ready initial responses and discussion replies
```

Use only the layers a question needs: conceptual questions can move directly from an internal note to a paste-ready response, while durable experimental results, substantial derivations, and other auditable findings require a stable question-level record.

### Reference Structure

The following example uses reviewer numbers and question numbers. `R1`, `R2`, and `R3` identify reviewers in platform display order. `Q1`, `Q2`, and `Q3` identify actionable questions in the order recorded for that reviewer.

```text
2_TheoriesAndExperimentsLog/
└── Rebuttal-<Venue-Year>/
    ├── 00-README.md
    ├── 01-Question-Registry.md
    │
    ├── R1-Q2-Additional-Experiment.md
    ├── R2-Q1-Efficiency-Analysis.md
    ├── R3-Q3-Robustness.md
    │
    ├── notes/
    │   ├── R1/
    │   │   ├── 00-Reviewer-Map.md
    │   │   ├── Q1-Conceptual-Clarification.md
    │   │   └── Q2-Additional-Experiment/
    │   │       ├── 00-README.md
    │   │       ├── Round-01-Initial-Question-and-Preparation.md
    │   │       ├── Round-01-Experiment-Design.md
    │   │       ├── Round-02-Discussion-Gaps.md
    │   │       ├── Round-02-Experiment-Design.md
    │   │       └── 90-Evidence-Index.md
    │   │
    │   ├── R2/
    │   │   ├── 00-Reviewer-Map.md
    │   │   ├── Q1-Efficiency-Analysis/
    │   │   │   ├── 00-README.md
    │   │   │   ├── Round-01-Initial-Question-and-Preparation.md
    │   │   │   ├── Round-01-Experiment-Design.md
    │   │   │   └── 90-Evidence-Index.md
    │   │   └── Q2-Scope-and-Limitations.md
    │   │
    │   └── R3/
    │       ├── 00-Reviewer-Map.md
    │       ├── Q1-Definition.md
    │       ├── Q2-Comparison.md
    │       └── Q3-Robustness/
    │           ├── 00-README.md
    │           ├── Round-01-Initial-Question-and-Preparation.md
    │           ├── Round-01-Experiment-Design.md
    │           └── 90-Evidence-Index.md
    │
    └── log/
        ├── R1-Q2-Additional-Experiment/
        │   ├── R1-Q2-current.md
        │   ├── run-<date>.md
        │   ├── raw/
        │   └── aggregate/
        ├── R2-Q1-Efficiency-Analysis/
        └── R3-Q3-Robustness/
```

`00-README.md` defines the scope and authoritative locations, while `01-Question-Registry.md` tracks each question's review source, responses, discussion rounds, experiment status, evidence record, response file, and conclusion. Reuse the same `Q` ID for repeated issues, assign a new one only to genuinely new questions, and keep simple questions in a single note while giving experiment-heavy, theoretical, or recurring questions a directory with `Round-01` for the initial rebuttal and later rounds only as needed. The root stable record should summarize verified settings, final results, validity issues, conclusions, claim boundaries, and authoritative links; keep temporary hypotheses in `notes/`, operational details in `log/`, and reviewer-facing prose in the response workspace.

For a Markdown-based review platform, the response workspace can use the following layout:

```text
4_Rebuttal/
└── <Venue-Year>/
    ├── Reviews.md
    ├── Initial/
    │   ├── R1.md
    │   ├── R2.md
    │   └── R3.md
    └── Discussion/
        ├── R1.md
        ├── R2.md
        └── R3.md
```

## Two Writing Resources

- [`Tutorial.pdf`](Tutorial.pdf) covers LaTeX organization, references, equations, submission, rebuttal, tools, papers, and code.
- [`Paper_Workflow.md`](Paper_Workflow.md) explains a human-in-the-loop workflow for AI-assisted paper and rebuttal writing. AI produces drafts, while the researcher supplies context, verifies claims, rewrites, and iterates.

You may also be interested in [WritingAIPaper](https://github.com/hzwer/WritingAIPaper).
