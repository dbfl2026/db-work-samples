## Relocation Roadmaps - Post-Intake Routing Workflow

Built to automate post-intake contact triage for an active relocation lead generation system - 3,500+ contacts across five target markets, routed by completeness into prioritized review queues. HubSpot is the source of truth, Zapier handles the routing logic, Google Sheets keeps a log, and Gmail sends the notifications.

For a quick visual overview, see the [workflow diagram](/Screenshots/04-flow-diagram.png). For the full workflow logic and build details, see the [workflow spec](/Screenshots/relocation_roadmaps_workflow_spec.md). For system images see the [/Screenshots]

### What it does

Triggers on a new or updated HubSpot contact, evaluates three intake fields, assigns a routing status, updates HubSpot, logs the result to Google Sheets, and sends an internal Gmail alert.

- Checks `Target Country`, `Target City`, and `Move Timeframe`
- Routes the contact to one of three statuses: `Needs Info`, `Needs Review`, or `Ready for Review`
- Updates `Workflow Status` in HubSpot
- Writes the result to Google Sheets
- Sends an internal Gmail alert

### Routing rules

- **Needs Info** - `Target Country` is missing or `Unknown`
- **Needs Review** - `Target Country` exists, but `Target City` or `Move Timeframe` is missing or `Unknown`
- **Ready for Review** - `Target Country`, `Target City`, and `Move Timeframe` all exist and none are `Unknown`

### How it is used

- Contacts start with blank `Workflow Status`
- Once routed, Zapier writes one of the three statuses back to HubSpot
- Corrections are made in HubSpot, not in Google Sheets
- A filter prevents already-processed contacts from re-entering the workflow

### Notes

- This is a live Relocation Roadmaps workflow, not a demo-only build
- Google Sheets acts as both a log and a review queue
- Gmail alerts are currently sent to the same owner inbox
