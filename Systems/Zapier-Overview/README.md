# Zapier Operations Overview - Relocation Roadmaps

## Purpose
We use Zapier to support day-to-day operating workflows across Relocation Roadmaps. That includes post-intake routing, backups, sales logging, subscriber tracking, and moving audit findings into review queues. The goal is simple: keep automations clear, testable, and easy to verify.

## Design Approach
Every workflow should be easy to verify. We use Zapier for routing, logging, notifications, and handoffs when the logic is clear and limited. If a process depends on open-ended judgment, interpretation, or editorial decision-making, it stays manual.

## Active Automations

### 1. HubSpot CRM - RR Post-Intake Routing Workflow
**Purpose**  
Routes new or updated HubSpot contacts based on intake completeness after the contact already exists in HubSpot.

**Trigger**  
Contact recently created or updated in HubSpot.

**Actions**  
Checks `Target Country`, `Target City`, and `Move Timeframe`, then routes the contact into one of three statuses:
- `Needs Info`
- `Needs Review`
- `Ready for Review`

Writes the resulting `Workflow Status` back to HubSpot, logs the outcome to Google Sheets, and sends an internal Gmail alert.

**Failure Handling**  
The workflow uses a filter to keep already-processed contacts from re-entering the Zap after status has been written back. Corrections are made in HubSpot, not in Google Sheets. If a record needs to be tested again manually, `Workflow Status` can be cleared and the contact can be updated again.

**Reference**  
See the workflow diagram and supporting screenshots in the workflow folder.

### 2. Auditor - Sheets -> Notion (Audit Review)
**Purpose**  
Turns audit findings into an editor review queue.

**Trigger**  
New Spreadsheet Row in Google Sheets.

**Actions**  
Creates a matching item in Notion (Audit Review) and writes the returned Notion page ID back to the original Google Sheets row for traceability.

**Failure Handling**  
We rely on Zapier’s built-in error logs. If the Notion queue count looks off, we review the Zap history and reconcile it against the Sheets log.

### 3. Daily Backup - Guides -> Google Drive
**Purpose**  
Backs up the Guides database to Google Drive for redundancy.

**Trigger**  
Runs every day on a schedule.

**Actions**  
Exports the current Guides data and saves a file to Google Drive.

**Failure Handling**  
Sends a heartbeat ping to an external monitor at the end of the run. If the Zap fails or hangs, the ping never sends and we get an alert.

### 4. Daily Backup - Vendors -> Google Drive
**Purpose**  
Backs up the Vendors database to Google Drive.

**Trigger**  
Runs every day on a schedule.

**Actions**  
Exports the Vendors data and saves the file to Google Drive.

**Failure Handling**  
Uses the same heartbeat check as the Guides backup. If it misses a run, we know.

### 5. RR - Sales - Payhip -> Google Sheets
**Purpose**  
Logs sales for quick reconciliation.

**Trigger**  
A customer buys something in Payhip.

**Actions**  
Adds a new row to a Google Sheet with the transaction details.

**Failure Handling**  
We rely on Zapier’s built-in error logs. No external monitoring here.

### 6. Buyer Tag - Payhip -> ConvertKit
**Purpose**  
Segments buyers from the general mailing list.

**Trigger**  
A customer buys something in Payhip.

**Actions**  
Tags the subscriber in ConvertKit.

**Failure Handling**  
Standard Zapier status checks. We review errors manually if the numbers look off.

### 7. Subscriber Log - ConvertKit -> Google Sheets
**Purpose**  
Keeps a simple log of new subscribers outside the email platform.

**Trigger**  
A new user joins the list through a Kit form on our home page.

**Actions**  
Adds subscriber info to a Google Sheet.

**Failure Handling**  
Standard Zapier error logs.

### 8. Optional - Zapier Errors -> Google Sheets (`zapier_error_log`)
**Purpose**  
Keeps a persistent error log outside Zapier for visibility and review.

**Trigger**  
Zapier Manager - New Zap Error.

**Actions**  
Writes a row to a dedicated `zapier_error_log` tab in Google Sheets with the Zap name, error message, limited context, and a link back to the Zap.

**Failure Handling**  
This is a monitoring Zap. If it fails, we fall back to Zapier’s native task history and error reporting.

## Intentional Limitations
We use Zapier where the logic is explicit, bounded, and easy to test. If a workflow becomes hard to verify, too repetitive, or too dependent on manual judgment, we simplify it or rebuild it. HubSpot stays as the main record. Google Sheets is used for logging and follow-up when needed.
