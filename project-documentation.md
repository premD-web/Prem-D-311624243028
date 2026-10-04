# ServiceNow Project Documentation

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


## 1. Introduction

ServiceNow uses Access Control Lists (ACLs) to decide whether users can access records or fields. A scripted ACL can evaluate the current record's field values and return a Boolean access decision. This project applies that pattern to Incident records so access can vary according to the record's configured field value.

### 1.1 Objectives
- Control access to Incident records using a scripted ACL.
- Evaluate a selected Incident field before allowing access.
- Restrict unauthorized reading or modification of protected records.
- Keep the access rule understandable and maintainable.
- Validate expected and denied scenarios through functional testing and UAT.

### 1.2 Scope
- Incident table and record-level access.
- A field-value decision for the selected ACL operation.
- Authorized and unauthorized access tests.
- Documentation of problem, requirements, design, implementation, and UAT.

## 2. Ideation — Define the Problem

### Problem statement 1
- **User:** Service desk / Incident user
- **Trying to:** Access Incident records needed for work
- **But:** Broad ACL rules may make too many records accessible
- **Because:** Access is not sufficiently controlled by record conditions
- **Impact:** Sensitive or restricted records may be exposed

### Problem statement 2
- **User:** ServiceNow administrator
- **Trying to:** Apply a field-based access rule
- **But:** Role-only rules do not express every record-level condition
- **Because:** The record's field values can change the access decision
- **Impact:** Manual administration and security risk may increase

### Selected problem focus
Restrict Incident access dynamically by evaluating a selected field value in a scripted ACL. The script should allow access only when the approved rule is satisfied.

## 3. Empathize and Discover — Empathy Map

| Area | Project context |
|---|---|
| Think and feel | Need Incident information available to authorized users while protecting restricted records. |
| See | Incident forms, lists, roles, field values, and different access outcomes. |
| Hear | Requirements about confidentiality, least privilege, and controlled access. |
| Say and do | Open, read, update, and manage records according to responsibilities. |
| Pain | Overly broad access, manual checks, inconsistent rules, accidental exposure. |
| Gain | A predictable, centrally configured access decision based on record data and authorization. |

## 4. Brainstorming and Idea Prioritization

Options considered:
1. Use role-based ACLs only.
2. Use a field condition without scripting.
3. Use a scripted ACL that evaluates the record field value.
4. Combine role validation and field-value validation.
5. Create separate read and write ACLs.
6. Add monitoring for denied access where required.

**Selected idea:** Use a Script-Controlled ACL to evaluate the required Incident field and, where appropriate, the user's role.

## 5. Problem–Solution Fit

| Element | Details |
|---|---|
| Customer segment | ServiceNow administrators, ITSM process owners, security administrators, service desk users |
| Job to be done | Allow authorized users to access records while restricting records that meet the protected condition |
| Trigger | A user attempts to read or modify an Incident |
| Before | Broad or static access rules |
| After | Access decision considers record field values through an ACL script |
| Existing approaches | Role-only ACLs, manual checks, broad table permissions |
| Root cause | Access rules may not account for changing record-level conditions |
| Solution | A scripted ACL evaluates the configured field and returns an access decision |

## 6. Proposed Solution

Create an ACL on the Incident (`incident`) table. Its script checks a selected field, such as `impact`, and can check an authorized role for protected records.

| Component | Purpose |
|---|---|
| Incident table | Stores the records being protected |
| ACL rule | Defines table and operation |
| ACL script | Evaluates the field and returns true/false |
| User/role context | Provides authorization context when role checks are used |
| Security engine | Applies ACL results before allowing the operation |

### 6.1 Example business rule

For demonstration, an Incident with `impact == '1'` is treated as protected and requires the example role `incident_restricted_access`. Other incidents are allowed by this script, subject to the rest of ServiceNow's ACL hierarchy. Confirm the business rule before using it outside a demo.

## 7. User Stories and Acceptance Criteria

| ID | User story | Acceptance criteria | Priority |
|---|---|---|---|
| US-01 | As an administrator, I can create an ACL for Incident records. | ACL is active and applies to the intended table and operation. | High |
| US-02 | As an administrator, I can use a script to evaluate a field value. | Script returns the expected decision for each test condition. | High |
| US-03 | As an authorized user, I can access a protected Incident when permitted. | Record opens or updates when all applicable ACLs permit access. | High |
| US-04 | As an unauthorized user, I cannot access a protected Incident. | The operation is denied when the protected condition is not authorized. | High |
| US-05 | As an administrator, I can test different field values. | Changing the field value changes the script decision according to the rule. | Medium |

## 8. Solution Requirements

### 8.1 Functional requirements
- The system shall provide an ACL for the Incident table.
- The ACL shall evaluate the configured field value.
- The script shall return an allow/deny decision.
- Authorized access shall be permitted when the approved rule and all applicable ACLs permit it.
- Unauthorized access to protected records shall be denied.
- The rule shall be tested with multiple records and field values.
- Separate ACLs may be created for read, write, create, or delete as required.

### 8.2 Non-functional requirements
- **Security:** follow least privilege.
- **Maintainability:** keep the script simple and documented.
- **Reliability:** same inputs should produce consistent decisions.
- **Performance:** avoid unnecessary database queries in ACL scripts.
- **Usability:** give authorized users predictable access.
- **Auditability:** keep configuration changes traceable.

## 9. Solution Architecture

| Layer | Component | Responsibility |
|---|---|---|
| User | ServiceNow browser / workspace | Requests access |
| Application | Incident Management | Handles the requested operation |
| Security | ACL engine | Finds and evaluates applicable ACLs |
| Script | ACL script | Checks field value and authorization |
| Data | Incident table | Supplies record values |

### 9.1 Data flow
1. User requests access to an Incident.
2. ServiceNow identifies the operation, such as read or write.
3. The ACL engine evaluates applicable ACLs.
4. The script checks the configured field.
5. The script evaluates the approved condition and role, if applicable.
6. The script returns true or false.
7. ServiceNow allows or blocks the request according to the full ACL evaluation.

### 9.2 Architecture flow

`User request → Incident record → ACL engine → Scripted field check → Allow/deny decision → ServiceNow response`

## 10. Technology Stack

| Technology | Use |
|---|---|
| ServiceNow platform | Development and execution environment |
| Incident Management | Primary module and table |
| Access Control List | Security mechanism |
| Server-side JavaScript | Field-value access decision |
| User/role model | Authorization context |
| ServiceNow database | Stores Incident records and field values |
| Browser / workspace | User interface |

## 11. Project Planning and Sprint Estimation

| Sprint | Task | Story points |
|---|---|---:|
| Sprint 1 | Requirement analysis and problem definition | 2 |
| Sprint 1 | ACL design and table/operation configuration | 3 |
| Sprint 1 | Scripted field-value access logic | 3 |
| Sprint 2 | Read/write access test scenarios | 3 |
| Sprint 2 | Negative/unauthorized access testing | 2 |
| Sprint 2 | Regression testing and UAT documentation | 3 |
| **Total** | **2 planned sprints** | **16** |

Illustrative velocity: 16 points / 2 sprints = 8 points per sprint.

## 12. Implementation — Script-Controlled ACL

### 12.1 Create the ACL
1. Sign in to a development ServiceNow instance with suitable administrator/developer permissions.
2. Open the Access Control (ACL) configuration area.
3. Create a new ACL for the Incident (`incident`) table.
4. Select the operation to protect (start with Read for this demonstration).
5. Configure roles/conditions only as approved for the business rule.
6. Enable the Script option.
7. Add the reviewed script from `servicenow/acl_scripts/incident_field_value_acl.js`.
8. Save and activate the ACL.
9. Test with authorized and unauthorized accounts.

### 12.2 Example ACL script

See `servicenow/acl_scripts/incident_field_value_acl.js`. The sample is a design pattern; the exact field, protected value, operation, and role must be confirmed and tested in the target instance.

### 12.3 Implementation logic
- Initialize the decision as false.
- Read the relevant field from the current Incident.
- Compare it with the protected value.
- Allow non-protected records according to the project rule.
- For protected records, verify the required role.
- Return the Boolean decision through the ACL script.

## 13. Testing Strategy

See `tests/test-cases.csv` for the detailed cases. Test both allowed and denied outcomes, field-value changes, inactive ACL behavior, and separate read/write ACLs. Record the actual result and evidence from the ServiceNow instance.

## 14. UAT Execution and Report

UAT verifies that the ACL behaves according to the approved rule and does not unintentionally block authorized Incident operations.

| UAT area | Planned cases | Status |
|---|---:|---|
| ACL configuration | 2 | NOT RUN — update after testing |
| Field-value evaluation | 3 | NOT RUN — update after testing |
| Authorized access | 2 | NOT RUN — update after testing |
| Unauthorized access | 2 | NOT RUN — update after testing |
| Read/write separation | 2 | NOT RUN — update after testing |
| Regression / end-to-end | 3 | NOT RUN — update after testing |

**UAT sign-off:** Pending actual execution in the team's ServiceNow instance.

## 15. Known Issues and Limitations

- The field name, protected value, operation, and role must match the approved rule.
- Client-side UI controls do not replace server-side ACL security.
- ACL scripts should avoid unnecessary database lookups.
- Another applicable ACL can still deny access even if this script returns true.
- Test with appropriate user roles to verify real behavior.
- The example script must be replaced if the team's final rule differs.

## 16. Future Enhancements

- Create separate read, write, create, and delete ACLs as required.
- Support multiple field values and business conditions.
- Combine field checks with role, group, or user authorization.
- Add Automated Test Framework coverage.
- Add security monitoring and audit reporting.
- Use reusable Script Includes for complex logic when appropriate.
- Extend the approach to Change or Problem records after review.

## 17. Conclusion

The project demonstrates how ServiceNow can enforce record-level security using a field-value-based scripted access decision. By evaluating an Incident before allowing an operation, the solution supports controlled access, least privilege, and consistent security behavior. The repository includes the project design, implementation pattern, test plan, and UAT evidence template.

## Appendix A — Suggested ACL Configuration

| Configuration item | Value |
|---|---|
| Table | Incident (`incident`) |
| Operation | Read for initial demo; configure other operations separately |
| Active | True after review |
| Field | `impact` (example only) |
| Protected value | `1` (example only) |
| Role | `incident_restricted_access` (example only) |
| Script | Use the reviewed and tested script in this repository |
| Testing | Verify authorized and unauthorized scenarios before submission |
