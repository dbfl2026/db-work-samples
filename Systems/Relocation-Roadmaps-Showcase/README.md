# Relocation Roadmaps - AI-Assisted Relocation Guide Production System

## Technologies Used

- **AI tools:** ChatGPT, Claude, Gemini
- **Business platforms:** Google Workspace, Google Docs, Google Sheets, Microsoft Excel, Notion, Zapier, HubSpot, WordPress
- **Data/file formats:** JSON, TSV, Markdown
- **Version control:** GitHub

Relocation Roadmaps is a structured content production system for creating high-quality relocation and retirement guides using AI-assisted writing, human review, data auditing, and reusable production workflows.

This showcase highlights how I designed a repeatable system for turning raw country, city, visa, healthcare, housing, finance, and lifestyle research into polished guide sections that are consistent, source-aware, and production-ready.

![Phuket relocation guide cover](Screenshots/01-phuket_guide_cover.png)

## What This Project Shows

This project demonstrates practical AI operations work across content systems, prompt design, quality control, structured review, and production workflows.

It includes examples of:

- AI-assisted guide section production
- Custom writer prompts and review prompts
- Red team review for quality, consistency, and risk
- Structured data pack and evidence ledger usage
- Repeatable QA and audit workflows
- Production-ready guide section samples
- Human-in-the-loop editing and final review

## Why It Matters

Relocation content is complex because it combines personal decision-making with information that changes often, including visas, healthcare access, tax exposure, banking, housing, residency rules, and local quality of life.

The goal of this system is not to generate generic AI travel content. The goal is to create a controlled production workflow where AI helps organize, draft, review, and improve guide material while humans remain responsible for judgment, accuracy, and final publishing decisions.

## System Overview

The Relocation Roadmaps workflow uses a modular production process:

1. Build or update the country and city data pack
2. Generate guide sections using structured writer prompts
3. Run QA checks against formatting, tone, structure, and source expectations
4. Red team sections for unclear claims, weak logic, missing context, or reader risk
5. Revise into production-ready guide copy
6. Maintain reusable prompts, examples, and section rules for future guides

![Relocation Roadmaps production workflow](Screenshots/rr-production_workflow.png)

## Featured Artifacts

### 1. Production-Ready Guide Section Sample

This sample shows a completed guide section after structured drafting, editing, and review. The Section 07 budget sample demonstrates how the system handles monthly cost bands, numeric anchors, source-aware claims, and reader-facing guidance.

Suggested file:

`samples/section-07-production-ready-sample.md`

### 2. Evidence Ledger Sample

The evidence ledger shows how source material is organized before it is used in guide production. It tracks source type, source class, recency, access status, numeric anchors, page evidence, and notes so the writing process has a clear evidence base.

![Evidence ledger sample](Screenshots/evidence_leger_sample.png)

### 3. AI Guide Audit Workflow

A separate work sample shows the data auditor workflow used to review AI-generated guide content against structured source material.

[View the AI Guide Audit Workflow](https://github.com/dbfl2026/db-work-samples/tree/main/Systems/AI-Guide-Audit-Workflow)

### 4. Red Team Review Prompt

This prompt is used to challenge guide sections before publication. It checks for unsupported claims, vague language, missing caveats, inconsistent structure, and areas where a reader could be misled.

Suggested file:

`prompts/red-team-review-prompt.md`

### 5. Writer Prompt Sample

This sample shows how a guide section is generated from structured input while maintaining a consistent guide voice, format, and reader focus.

Suggested file:

`prompts/section-writer-prompt-sample.md`

### 6. Source & Data Integrity Auditor

The custom auditor reviews guides, tables, and source lists before publishing. It flags missing information, source gaps, outdated claims, citation problems, internal inconsistencies, and risk areas without rewriting the content.

![Source and Data Integrity Auditor configuration](Screenshots/source_data_&_integrity_auditor.png)

### 7. Fact Checker & Red Team Auditor

The fact checker and red team auditor is designed to protect the reader from financial loss, legal rejection, logistical failure, or misleading claims caused by outdated, incorrect, vague, or non-executable information.

![Fact Checker and Red Team Auditor prompt](Screenshots/fact_checker_&_red_team_auditor.png)

## My Role

I designed and built the production system, including the workflow structure, prompt architecture, quality review process, sample guide outputs, and supporting documentation.

The work combines product thinking, content operations, AI workflow design, prompt engineering, editorial judgment, and practical automation planning.

## Key Takeaway

Relocation Roadmaps is an example of using AI as part of a controlled production system, not as a one-click content generator.

The value is in the workflow: structured inputs, reusable prompts, review layers, risk checks, and production standards that make the output more consistent and trustworthy over time.
