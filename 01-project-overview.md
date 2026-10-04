# Phase 01 — Project Overview

**Project:** Script-Controlled ACL – Restrict Record Access Based on Field Value  
**Team ID:** SWTID-2026-4677  
**Team:** Botbyte

## Purpose
Project title, platform, module, core technology, team ID, team name, team leader, members, scope and intended outcome.

## Project content
## Project information

| Field | Details |
|---|---|
| Project title | Script-Controlled ACL – Restrict Record Access Based on Field Value |
| Platform | ServiceNow |
| Primary module | Incident Management |
| Core technology | Access Control List (ACL) with script condition |
| Project type | ServiceNow configuration and scripting |

## Team
- **Team ID:** SWTID-2026-4677
- **Team Name:** Botbyte
- **Team Size:** 05
- **Team Leader:** Prem. D
- **Team Members:** Harshita. R, Sharvi. M, Durga. S, Keerthika. S

## Project summary

This project demonstrates a server-side Script-Controlled Access Control List (ACL) on the ServiceNow Incident table. The ACL evaluates a configured field value and, when required, the current user's role before returning an allow/deny decision. The sample rule below uses `impact == '1'` as the protected condition and `incident_restricted_access` as the example authorized role. Replace these with the team's approved business rule and validate them in the target ServiceNow instance.

> **Important:** This repository documents a configuration pattern. It does not connect to or configure a ServiceNow instance automatically. Do not report tests as passed until they have actually been run in the instance.


## Deliverable
A concise overview of the project, team, platform, module, scope, and target outcome.

## Review checklist
- [ ] Content reviewed by team
- [ ] Assumptions confirmed with mentor
- [ ] Evidence added where applicable
- [ ] Status updated to reflect actual work
