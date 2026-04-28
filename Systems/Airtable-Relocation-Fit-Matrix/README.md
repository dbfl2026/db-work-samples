# Airtable Relocation Fit Matrix - Relocation Roadmaps

## Overview

I built this Airtable system to compare relocation fit across countries, cities, personas, and decision factors.

It is not a recommendation engine. It does not rank cities, assign scores, or tell someone where to move. It organizes fit signals, tradeoffs, evidence notes, and AI-generated draft language so a relocator can make a more informed decision.

## What I Built

The base connects six Airtable tables:

Personas  
Countries  
Cities  
Fit Factors  
Fit Matrix Notes  
Evidence Notes

The main working table is **Fit Matrix Notes**. Each record ties together a persona, country, city, fit factor, fit signal, tradeoff level, supporting evidence, and AI draft outputs.

## Table Structure

<p align="center">
  <img src="Screenshots/relocation_decision_support_structure_final_clean.png" alt="Relocation decision support table relationship diagram" width="90%">
</p>

<br>

## AI-Assisted Decision Support

Airtable AI field agents generate draft language for:

Fit summary  
Best fit conditions  
Poor fit warnings  
Must-verify issues  
Confidence level

The AI is intentionally constrained. It does not recommend a destination or make the final decision. Its role is to turn structured Airtable records into clearer review language.

## Demo Record

The MVP test record uses:

Persona: US Retiree  
Country: Thailand  
City: Bangkok  
Factor: Healthcare access  
Fit Signal: Possible Fit  
Tradeoff Level: Medium

&nbsp;
<p align="center">
  <img src="Screenshots/airtable_fit_matrix_demo_us_retiree_healthcare.png" alt="Airtable Fit Matrix Interface demo for US Retiree Thailand healthcare access" width="90%">
</p>

## Backend Matrix View

The backend view shows the filtered Thailand city matrix used to review records before they appear in the demo Interface.

&nbsp;
<p align="center">
  <img src="Screenshots/airtable_thailand_city_fit_matrix_view.png" alt="Airtable Thailand city fit matrix backend view" width="90%">
</p>

<br>

## Why It Matters

This project shows practical Airtable system design, relational data modeling, evidence tracking, and controlled AI use inside a real Relocation Roadmaps workflow.

The result is a lightweight decision-support system that is structured enough to scale, but simple enough to review and maintain.

## Status

MVP complete.

Current scope includes Thailand city-level testing, seven relocation personas, evidence-linked notes, Airtable AI draft fields, filtered review views, and a portfolio demo Interface.
