# Implementation Guide

## Example configuration (confirm before using)

- **Type:** Record ACL
- **Operation:** Read
- **Name/table:** Incident (`incident`)
- **Active:** Yes after testing
- **Example protected field:** `impact`
- **Example protected value:** `1`
- **Example role:** `incident_restricted_access`

## Script

Copy the content of `servicenow/acl_scripts/incident_field_value_acl.js` into the ACL Script field.

## Important ServiceNow behavior

- ACL evaluation is server-side.
- A true result from one ACL does not guarantee access if another applicable ACL denies it.
- The sample role name is illustrative. Create/use the approved role in the instance.
- Do not test by changing production ACLs. Use a development or training instance.
- Test Read separately from Write. A Read ACL does not automatically secure Write operations.
