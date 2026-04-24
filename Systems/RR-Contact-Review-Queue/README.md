## Relocation Roadmaps - Post-Intake Routing Workflow

Built to automate post-intake contact triage for an active relocation lead generation system - 3,500+ contacts across five target markets, routed by completeness into prioritized review queues. HubSpot is the source of truth, Zapier handles the routing logic, Google Sheets keeps a log, and Gmail sends the notifications.
This workflow handles contacts after they have already been created in HubSpot. It checks whether the intake is complete, assigns a routing status, logs the result, and sends an internal email alert. HubSpot is the source of truth, Zapier handles the routing logic, Google Sheets keeps a log, and Gmail sends the notifications.

For a quick visual overview, see the [workflow diagram](./Screenshots/04-flow-diagram.png). For the full workflow logic and build details, see the [workflow spec](./relocation_roadmaps_workflow_spec.md). For system images see the [Screenshots](./Screenshots/) folder.

### What it does

Triggers on a new or updated HubSpot contact, evaluates three intake fields, assigns a routing status, updates HubSpot, logs the result to Google Sheets, and sends an internal Gmail alert.

### What it does

At a high level, this workflow takes a new or updated HubSpot contact, evaluates a small set of intake fields, and routes that contact into the correct next state.

- Triggers when a HubSpot contact is created or updated
- Checks `Target Country`, `Target City`, and `Move Timeframe`
- Routes the contact to one of three statuses:
  - `Needs Info`
  - `Needs Review`
  - `Ready for Review`
- Updates `Workflow Status` in HubSpot
- Writes the result to Google Sheets
- Sends an internal Gmail alert

### Routing rules

These are the conditions that determine which status the contact receives after the Zap runs.

- **Needs Info**
  - `Target Country` is missing or `Unknown`
- **Needs Review**
  - `Target Country` exists, but `Target City` is missing, or `Move Timeframe` is missing or `Unknown`
- **Ready for Review**
  - `Target Country` exists
  - `Target City` exists
  - `Move Timeframe` exists
  - `Move Timeframe` is not `Unknown`

### How it is used

These notes explain how the workflow behaves in practice once it is live.

- Contacts start with blank `Workflow Status`
- Once routed, Zapier writes one of the three statuses back to HubSpot
- Corrections are made in HubSpot, not in Google Sheets
- A filter prevents already-processed contacts from re-entering the workflow

### Notes

These are a few practical details about how the workflow is currently set up.

- This is a live Relocation Roadmaps workflow, not a demo-only build
- Google Sheets acts as both a log and a review queue
- Gmail alerts are currently sent to the same owner inbox
