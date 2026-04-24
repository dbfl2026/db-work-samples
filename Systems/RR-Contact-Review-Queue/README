## Relocation Roadmaps - Post-Intake Routing Workflow

This workflow routes HubSpot contacts after intake, classifies them based on data completeness, writes the result back to HubSpot, logs the outcome in Google Sheets, and sends an internal Gmail alert.

### Stack
- HubSpot
- Zapier
- Google Sheets
- Gmail

### Purpose
The workflow begins after a contact already exists in HubSpot. It is used to sort new or updated contacts into one of three statuses:
- `Needs Info`
- `Needs Review`
- `Ready for Review`

### How it works
1. A contact is created or updated in HubSpot.
2. Zapier checks whether the contact has already been processed.
3. If `Workflow Status` is still blank, Zapier evaluates:
   - `Target Country`
   - `Target City`
   - `Move Timeframe`
4. The contact is routed into one of three paths:
   - **Needs Info** - key intake data is missing
   - **Needs Review** - intake exists but is incomplete or unclear
   - **Ready for Review** - intake is complete enough for final review
5. Zapier updates `Workflow Status` in HubSpot.
6. Zapier logs the outcome to Google Sheets.
7. Zapier sends an internal Gmail alert.

### Routing logic
**Ready for Review**
- `Target Country` exists
- `Target City` exists
- `Move Timeframe` exists
- `Move Timeframe` is not `Unknown`

**Needs Review**
- `Target Country` exists
- and one of the following is true:
  - `Target City` is missing
  - `Move Timeframe` is missing
  - `Move Timeframe` is `Unknown`

**Needs Info**
- `Target Country` is missing
- or `Target Country` is `Unknown`

### Source of truth
HubSpot is the source of truth. Corrections are made in HubSpot, not in Google Sheets.

### Notes
- Google Sheets acts as a log and working queue.
- Gmail alerts are currently sent to the same owner inbox.
- The workflow includes a guard so already-processed contacts do not keep re-entering the Zap.
