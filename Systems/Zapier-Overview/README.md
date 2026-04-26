# Zapier Operations Overview

## Purpose
We use Zapier for a small set of practical workflows across Relocation Roadmaps, including intake routing, backups, sales logging, subscriber tracking, and audit queue handoff.

## Design Approach
We keep automations simple, testable, and easy to verify. If a process depends on judgment or interpretation, it stays manual.

## Active Automations

### 1. HubSpot CRM - RR Post-Intake Routing Workflow
**Purpose:** Routes HubSpot contacts after intake based on completeness.  
**Trigger:** Contact created or updated in HubSpot.  
**Actions:** Checks `Target Country`, `Target City`, and `Move Timeframe`, then sets `Workflow Status` to `Needs Info`, `Needs Review`, or `Ready for Review`, logs the result to Google Sheets, and sends a Gmail alert.  
**Notes:** Uses a filter to stop already-processed contacts from re-entering.

### 2. Auditor - Sheets -> Notion
**Purpose:** Moves audit findings into the Notion review queue.  
**Trigger:** New row in Google Sheets.  
**Actions:** Creates a Notion item and writes the Notion page ID back to Sheets.

### 3. Daily Backup - Guides -> Google Drive
**Purpose:** Backs up the Guides database.  
**Trigger:** Daily schedule.  
**Actions:** Exports Guides data to Google Drive.  
**Notes:** Uses a heartbeat ping for failure detection.

### 4. Daily Backup - Vendors -> Google Drive
**Purpose:** Backs up the Vendors database.  
**Trigger:** Daily schedule.  
**Actions:** Exports Vendors data to Google Drive.  
**Notes:** Uses the same heartbeat check as the Guides backup.

### 5. RR Sales - Payhip -> Google Sheets
**Purpose:** Logs sales for reconciliation.  
**Trigger:** Purchase in Payhip.  
**Actions:** Adds a transaction row to Google Sheets.

### 6. Buyer Tag - Payhip -> ConvertKit
**Purpose:** Tags buyers in ConvertKit.  
**Trigger:** Purchase in Payhip.  
**Actions:** Applies the buyer tag.

### 7. Subscriber Log - ConvertKit -> Google Sheets
**Purpose:** Keeps a simple subscriber log outside the email platform.  
**Trigger:** New subscriber from a Kit form.  
**Actions:** Adds subscriber info to Google Sheets.

### 8. Optional - Zapier Errors -> Google Sheets
**Purpose:** Keeps an external error log.  
**Trigger:** New Zap error from Zapier Manager.  
**Actions:** Writes error details to `zapier_error_log`.

## Limits
We use Zapier where the logic is clear and limited. HubSpot stays as the main record. Google Sheets is used for logging and follow-up when needed.