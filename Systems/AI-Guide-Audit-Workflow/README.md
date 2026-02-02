# AI Guide Audit Workflow

This workflow uses our RR Source & Data Integrity Auditor GPT to audit relocation guide content for quality and consistency, and then logs findings for follow-up.

## Quick overview
User runs our auditor GPT. Findings go into a Sheets log as TSV. Zapier picks up each new row and creates a new task in a Notion database. The Notion page ID is sent back in Sheets for traceability. Editors use Notion as a task list.

## How it works
You run the auditor and paste one of three inputs: a guide section (or part of one), a structured table, or a list of sources used in a guide.

Guide name and the link to the guide or section are required, and the GPT propmpts the user if they are missing.

The auditor only audits what you provide. It doesn't browse the web, edit content, rewrite text, add facts, or correct errors. It evaluates data quality, consistency, freshness, risk, and citation coverage using a fixed rule set.

## Outputs
The auditor returns:
- A short audit summary
- Findings grouped by severity
- A follow-up plan ordered by priority
- A JSON block with the full structured audit
- A TSV block formatted for Google Sheets, one row per finding

## Logging and follow-up
A user manually pastes the TSV rows into a log in Sheets.

A Zapier workflow uses the Google Sheets trigger "New Spreadsheet Row" to create a corresponding record in a Notion database used as a review queue. The Notion record stores the `audit_id` and `finding_id`, and Notion returns a `notion_page_id` that can be written back to the Sheets for traceability.

## Automation reliability monitoring
A separate Zapier workflow monitors automation failures using the Zapier Manager "New Zap Error" trigger. Zap errors are written to a `zapier_error_log` tab in Google Sheets, including the Zap name, error message, truncated context, and a link to the Zap editor.

## Design goals
- Find issues early, before going through our Fact - Checker & Red Team Auditor prompt
- Maintain an audit history in one place
- Create a task list system in for editors
- Keep the process simple and traceable
