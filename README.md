# Script-Controlled ACL – Restrict Record Access Based on Field Value

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


## Repository contents

- `docs/` — consolidated project documentation and implementation guide.
- `phases/` — phase-wise deliverables 01–14, ready to review and upload.
- `servicenow/acl_scripts/` — sample ACL script and implementation notes.
- `tests/` — test cases and UAT report template.
- `templates/` — reusable blank template for evidence and sign-off.
- `assets/screenshots/` — add genuine screenshots from your ServiceNow instance.

## Quick start

1. Review `docs/project-documentation.md`.
2. Confirm the protected field/value and authorized role with your project mentor.
3. In a development/personal ServiceNow instance, create the ACL described in `docs/implementation-guide.md`.
4. Paste the reviewed script into the ACL Script field.
5. Test as both authorized and unauthorized users using `tests/test-cases.csv`.
6. Replace placeholders and record actual outcomes in `tests/uat-report.md`.
7. Add genuine screenshots to `assets/screenshots/`.
8. Commit the complete repository to GitHub.

## Example rule used in this package

- Table: `incident`
- Operation: `read` (create separate ACLs for other operations if needed)
- Protected field: `impact`
- Protected value: `1`
- Example role: `incident_restricted_access`

For this example, non-protected incidents are allowed by this script; incidents with impact `1` require the example role. Existing ServiceNow ACL rules still apply, so a `true` result from this ACL does not override a denial from another applicable ACL.

## GitHub publication checklist

- [ ] Confirm team names and team ID.
- [ ] Confirm the final field, value, operation, and role with the mentor.
- [ ] Run allowed and denied scenarios in the instance.
- [ ] Replace all `NOT RUN` / placeholder results with real evidence.
- [ ] Add screenshots without passwords, personal data, or sensitive incident details.
- [ ] Review repository for secrets and instance credentials.
- [ ] Commit and push the repository.
- [ ] Submit the GitHub repository URL using the required college/training process.

## Suggested Git commit sequence

1. `docs: add project overview and requirements`
2. `docs: add ideation and solution design phases`
3. `feat: add sample scripted incident ACL`
4. `test: add ACL test cases and UAT template`
5. `docs: finalize implementation evidence and submission checklist`
