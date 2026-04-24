# Relocation Roadmaps - Post-Intake Routing Workflow

## Purpose
This workflow routes HubSpot contacts into the correct post-intake status based on intake completeness, writes the result back to HubSpot, logs the outcome in Google Sheets, and sends an internal Gmail alert.

## Business Context
This is a live Relocation Roadmaps workflow, not a demo-only build. It begins after a contact already exists in HubSpot. Contacts may enter HubSpot through form submission, manual entry, import, or another source.

## Stack
- HubSpot
- Zapier
- Google Sheets
- Gmail

## Source of Truth
HubSpot is the source of truth.

Corrections are made in HubSpot, not in Google Sheets. Google Sheets is used as a log and working queue. Gmail is used for alerts.

## Trigger
**Zapier Trigger:** HubSpot - Contact Recently Created or Updated

This is a post-intake routing workflow. It does not handle anything that happens before the contact is created in HubSpot.

## Filter Rule
The Zap should continue only for contacts that have not already been processed.

In practice, that means the Zap continues only when `Workflow Status` is not already one of the following:
- `Needs Info`
- `Needs Review`
- `Ready for Review`

This prevents contacts that have already been routed from re-entering the workflow after Zap-driven updates.

## Custom HubSpot Properties Used
- `Target Country`
- `Target City`
- `Move Timeframe`
- `Workflow Status`
- `Review Notes`

## Routing Logic
The workflow evaluates three intake fields:
- `Target Country`
- `Target City`
- `Move Timeframe`

Based on those fields, the contact is routed into one of three paths.

### Path 1 - Ready for Review
A contact goes to **Ready for Review** when:
- `Target Country` exists
- `Target City` exists
- `Move Timeframe` exists
- `Move Timeframe` is not `Unknown`

**Actions**
1. Update HubSpot contact:
   - `Workflow Status = Ready for Review`
2. Create spreadsheet row in Google Sheets
3. Send Gmail alert

### Path 2 - Needs Review
A contact goes to **Needs Review** when:
- `Target Country` exists
- and one of the following is true:
  - `Target City` does not exist
  - `Move Timeframe` does not exist
  - `Move Timeframe` exactly matches `Unknown`

**Actions**
1. Update HubSpot contact:
   - `Workflow Status = Needs Review`
2. Create spreadsheet row in Google Sheets
3. Send Gmail alert

### Path 3 - Needs Info
A contact goes to **Needs Info** when:
- `Target Country` does not exist
- or `Target Country` exactly matches `Unknown`

**Actions**
1. Update HubSpot contact:
   - `Workflow Status = Needs Info`
2. Create spreadsheet row in Google Sheets
3. Send Gmail alert

## Google Sheets Log
**Spreadsheet:** `relocation_roadmaps_review_queue`

The sheet acts as a running log of workflow outcomes and a working queue for follow-up when needed.

**Columns**
- Timestamp
- Contact ID
- First Name
- Last Name
- Email
- Target Country
- Target City
- Move Timeframe
- Workflow Status
- Review Notes

## Gmail Alerts
Gmail is used to send internal workflow alerts after routing.

At the moment, all alerts are sent to the same owner inbox.

**Subject Lines**
- `RR Needs Info - {{First Name}} {{Last Name}}`
- `RR Needs Review - {{First Name}} {{Last Name}}`
- `RR Ready for Review - {{First Name}} {{Last Name}}`

**Operational Meaning**
- **Needs Info:** the contact is too incomplete to evaluate and needs more intake data
- **Needs Review:** the contact is usable, but still needs operator judgment or cleanup
- **Ready for Review:** the contact is complete enough for final review

## Re-Entry Logic
Because the trigger is **created or updated**, a contact can re-enter the workflow after a manual change in HubSpot.

In normal operation, the filter prevents that from happening once `Workflow Status` has already been set to one of the three routing values:
- `Needs Info`
- `Needs Review`
- `Ready for Review`

If a contact needs to be tested again manually, `Workflow Status` can be cleared and the record can be updated again.

## What This Workflow Does Not Cover
This workflow does not handle pre-HubSpot intake logic. It begins only after a contact record already exists in HubSpot.

## Current Outcome
The workflow has been tested successfully across all three paths:
- Needs Info
- Needs Review
- Ready for Review

It updates HubSpot correctly, writes to Google Sheets, and sends Gmail alerts.
