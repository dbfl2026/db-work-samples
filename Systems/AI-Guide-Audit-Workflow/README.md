# AI Guide Audit Workflow

This workflow audits relocation guide content for quality and consistency and logs findings for follow-up.

## How it works
You run the RR Source and Data Integrity Auditor GPT and paste one of three inputs: a guide section (or part of one), a structured table, or a list of sources used in a guide.

The GPT only audits what you provide. It does not browse the web or edit content. It does not rewrite text, add facts, or correct errors. It evaluates data quality, internal consistency, freshness, risk framing, and citation coverage using a fixed rule set.

## Outputs
The GPT returns:
- A short audit summary
- Findings grouped by severity (Blocking, Major, Minor)
- A follow-up plan ordered by priority (P0, P1, P2)
- A JSON block with the full structured audit
- A TSV block formatted for Google Sheets, one row per finding

## Logging and follow-up
You paste the TSV into a Google Sheets audit log. Each row represents a finding, tracked by `audit_id` and `finding_id`.

When a finding needs human review, it is added to a Notion database used as a review queue. Notion is not the source of truth. The Notion entry stores the `audit_id` and `finding_id` so it stays linked to the Sheets log. After review, the `notion_page_id` can be written back to Sheets to preserve traceability without duplicating records.

## Automation reliability monitoring
A separate Zapier workflow monitors failures using the Zapier Manager "New Zap Error" trigger. Zap errors are written to a `zapier_error_log` tab in Google Sheets, including the Zap name, error message, truncated context, and a link to the Zap editor.

## Design goals
- Keep the process simple and traceable
- Surface issues early
- Maintain an audit history in one place (Sheets)
- Use Notion only for human decision tracking
