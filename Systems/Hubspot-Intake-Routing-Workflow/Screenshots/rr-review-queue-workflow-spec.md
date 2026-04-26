# Relocation Roadmaps - Post-Intake Routing Workflow

## Purpose
This workflow routes newly created or updated HubSpot contacts into one of three post-intake statuses based on intake completeness, logs the result to Google Sheets, and sends an internal Gmail alert.

## Business Context

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

The workflow only evaluates contacts whose `Workflow Status` has not already been set to one of the final routing values.

## Filter Rule
The Zap continues only when `Workflow Status` is not already one of the following:
- `Needs Info`
- `Needs Review`
- `Ready for Review`

This prevents already-processed contacts from re-entering the workflow after Zap-driven updates.

## Custom HubSpot Properties Used
- `Target Country`
- `Target City`
- `Move Timeframe`
- `Workflow Status`
- `Review Notes`

## Routing Logic

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
At the moment, all alerts are sent to the same internal owner inbox.

### Subject Lines
- `RR Needs Info - {{First Name}} {{Last Name}}`
- `RR Needs Review - {{First Name}} {{Last Name}}`
- `RR Ready for Review - {{First Name}} {{Last Name}}`

### Email Purpose
- **Needs Info:** contact is too incomplete to evaluate
- **Needs Review:** contact is usable but still needs operator judgment or cleanup
- **Ready for Review:** contact is complete enough for final review

## Re-Entry Logic
This is a post-intake routing workflow.

Because the trigger is **created or updated**, a contact can enter the workflow again after a manual change in HubSpot. In practice, the filter prevents that from happening once `Workflow Status` has already been set to one of the three routing values.

If a contact needs to be re-tested manually, `Workflow Status` can be cleared and the record can be updated again.

## Operational Meaning of Each Status
- **Needs Info:** key intake information is missing
- **Needs Review:** intake exists but is incomplete or questionable
- **Ready for Review:** intake is complete enough to hand off for final review

## What This Workflow Does Not Cover
This workflow does not handle pre-HubSpot intake logic. It begins only after a contact record already exists in HubSpot.

## Current Outcome
The workflow has been tested successfully across all three paths:
- Needs Info
- Needs Review
- Ready for Review

It updates HubSpot correctly, writes to Google Sheets, and sends Gmail alerts.
