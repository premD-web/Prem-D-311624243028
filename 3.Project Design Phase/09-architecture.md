# Phase 09 — Solution Architecture & Data Flow

**Project:** Script-Controlled ACL – Restrict Record Access Based on Field Value  
**Team ID:** SWTID-2026-4677  
**Team:** Botbyte

## Purpose
Layered architecture, data flow steps and text flow diagram.

## Project content
`User request → Incident table → ACL engine → Scripted field check → Allow/deny → ServiceNow response`

Layers: User/browser; Incident Management; ACL security engine; server-side script; Incident data table.

1. User requests access.
2. ServiceNow identifies operation.
3. Applicable ACLs are evaluated.
4. Script checks record field and role if required.
5. Script returns true/false.
6. Overall ACL evaluation determines the outcome.

## Review checklist
- [ ] Content reviewed by team
- [ ] Assumptions confirmed with mentor
- [ ] Evidence added where applicable
- [ ] Status updated to reflect actual work
