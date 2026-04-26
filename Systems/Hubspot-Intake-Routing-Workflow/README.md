# HubSpot Intake Routing Workflow

## Technologies Used

- **Business platforms:** HubSpot, Zapier, Google Sheets, Gmail
- **Data/file formats:** Markdown
- **Version control:** GitHub

## Overview

This workflow handles post-intake contact routing for Relocation Roadmaps, an active relocation lead generation system with 3,500+ contacts across five target markets.

New contacts do not always arrive with complete intake details. Some are ready for review. Some need cleanup. Others are missing basic information. This workflow sorts them automatically so the review queue stays usable.

HubSpot stays as the source of truth. Zapier runs the routing logic. Google Sheets keeps the review queue and audit log. Gmail sends the internal alerts.

[View the full workflow spec](Screenshots/rr-review-queue-workflow-spec.md)

## What It Does

When a HubSpot contact is created or updated, the workflow checks three intake fields: `Target Country`, `Target City`, and `Move Timeframe`.

Based on those fields, it assigns one of three statuses, updates the contact in HubSpot, adds a row to Google Sheets, and sends an internal Gmail alert.

## Routing Logic

| Status | Rule | Operational meaning |
|---|---|---|
| `Needs Info` | `Target Country` is missing or `Unknown` | Not enough information to evaluate |
| `Needs Review` | `Target Country` exists, but `Target City` or `Move Timeframe` is missing or `Unknown` | Usable contact, but needs operator judgment or cleanup |
| `Ready for Review` | `Target Country`, `Target City`, and `Move Timeframe` all exist, and `Move Timeframe` is not `Unknown` | Complete enough for final review |

## Source of Truth

HubSpot is the source of truth.

Corrections happen in HubSpot, not in Google Sheets. The spreadsheet is only a log and working review queue. That keeps the system clean: HubSpot holds the contact record, while Google Sheets gives the operator a simple place to review what happened.

## Re-Entry Protection

The trigger runs when a contact is created or updated, so the Zap needs a guardrail.

A filter stops contacts from re-entering the workflow after they already have one of the final routing statuses: `Needs Info`, `Needs Review`, or `Ready for Review`.

To test a contact again, the operator can clear `Workflow Status` in HubSpot and update the record.

## Why This Matters

This workflow turns messy intake data into a clear review queue.

Instead of checking every new contact by hand, the system separates contacts into practical groups: missing key information, usable but incomplete, and ready for final review. That creates a cleaner handoff and keeps the main operational record inside HubSpot.

## Current Outcome

The workflow has been tested successfully across all three paths: `Needs Info`, `Needs Review`, and `Ready for Review`.

It updates HubSpot, writes to Google Sheets, and sends Gmail alerts.

## My Role

I designed and built the workflow logic, HubSpot fields, Zapier routing paths, Google Sheets review queue, Gmail alerts, and documentation.

This work combines CRM operations, automation design, intake triage, workflow testing, and practical business systems implementation.

## Evidence

### Visual Workflow

<img src="Screenshots/04-flow-diegram.png" alt="Post-Intake Routing Workflow" width="650">

### Zapier Routing Workflow

<img src="Screenshots/02-zap-overview.png" alt="Zapier Routing Workflow" width="650">

### Google Sheets Review Queue

<img src="Screenshots/03-google-sheets-log.png" alt="Google Sheets Review Queue" width="650">

### HubSpot Contact Fields

<img src="Screenshots/01-hubspot-contact-fields.png" alt="HubSpot Contact Fields" width="650">

### Zapier Workflow List

<img src="Screenshots/05-Zaps.png" alt="Zapier Workflow List" width="650">
