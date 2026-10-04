# Phase 13 — Testing Strategy

**Project:** Script-Controlled ACL – Restrict Record Access Based on Field Value  
**Team ID:** SWTID-2026-4677  
**Team:** Botbyte

## Purpose
Test cases for allowed/denied access, field changes, ACL state, operation separation and regression.

## Project content
Use `../tests/test-cases.csv`. Minimum cases:
- Non-protected field value.
- Protected value with authorized role.
- Protected value without authorized role.
- Change protected value.
- Inactive ACL.
- Multiple records.
- Separate Write ACL test.
- Regression test.

All actual results remain NOT RUN until executed in the ServiceNow instance.

## Review checklist
- [ ] Content reviewed by team
- [ ] Assumptions confirmed with mentor
- [ ] Evidence added where applicable
- [ ] Status updated to reflect actual work
