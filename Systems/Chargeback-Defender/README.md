# Chargeback Defender

Chargeback Defender is a 10-file operational kit for e-commerce merchants
dealing with payment chargebacks on Stripe, Shopify Payments, and PayPal.
It went from idea to live product in 9 days.

What it does: Gives merchants a complete dispute workflow - decide whether
to fight, assemble evidence mapped to the specific reason code, submit
cleanly, track outcomes, and reduce future exposure.

Live product: [guideworks.co/chargeback-defender](https://guideworks.co/chargeback-defender)
Launch Dashboard: [guideworks.co/chargeback-defender/dashboard](https://guideworks.co/chargeback-defender/dashboard)

## Contents

[Chargeback Defender Project Overview.pdf](Chargeback%20Defender%20Project%20Overview.pdf) - How the project was built,
what each component does, the QA process used, and what this work
demonstrates for operations and AI operations roles.

[CB-Fight-or-Flight-Calculator.xlsx](CB-Fight-or-Flight-Calculator.xlsx) - Decision tool that takes transaction
value, dispute fee, time cost, and win probability as inputs, then outputs
a fight-or-accept recommendation with an ROI calculation. Shows
operational decision modeling in a simple, usable format.

[CB-Dispute-Response-Tracker.xlsx](CB-Dispute-Response-Tracker.xlsx) - Workbook for tracking open disputes,
deadlines, evidence status, and outcomes. Includes a Rate Monitor tab
that flags chargeback rate against processor thresholds with a
days-to-breach trend indicator. Shows threshold monitoring and
operational tracking design.

[CB-Test-Cases.pdf](CB-Test-Cases.pdf) - Three realistic dispute scenarios (Stripe fraud
claim, Shopify product-not-received, PayPal subscription cancellation)
that validate each lane of the workflow. Shows QA thinking and test
design for operational systems.

[CB-Evidence-Assembly-Guide.pdf](CB-Evidence-Assembly-Guide.pdf) - Maps each evidence type to where it
lives in the merchant's platform, with export and packaging instructions.
Includes the Stripe Compelling Evidence 3.0 field map. Shows
domain-specific documentation and process mapping.

[CB-Project-Conventions.pdf](CB-Project-Conventions.pdf) - Internal standards document covering file
naming, terminology, folder structure, cross-reference rules, and a rule
that new decisions get documented before they get implemented. Shows how
consistency was maintained across a multi-file system.

[CB-Tracker-Schema.pdf](CB-Tracker-Schema.pdf) - Schema documentation for the Dispute Response
Tracker. Shows how the tracker was designed at the field level.

## Build methodology

AI-assisted development with human QA at every stage. Claude was the
primary drafting tool. Human review ran on every component before it
entered the kit. A three-model audit process (Claude, Gemini, ChatGPT)
ran at key checkpoints for accuracy and consistency. Scope was locked
before the build started and held throughout. Version control was
maintained across 13 document revisions with tracked corrections.
