# Project Report

## Project Title

Script-Controlled ACL – Restrict Record Access Based on Field Value

## Objective

To restrict access to sensitive Incident records in ServiceNow based on the value of a field.

## Technologies Used

- ServiceNow
- JavaScript
- Access Control List (ACL)
- GitHub

## Working

1. A user attempts to access an Incident record.
2. The ACL checks the value of the sensitive field.
3. If the record is not sensitive, access is allowed.
4. If the record is sensitive, the user's authorization is checked.
5. Unauthorized users are denied access.

## Testing

The ACL will be tested using authorized and unauthorized users.

## Expected Result

Unauthorized users should not be able to access sensitive records, while authorized users should be able to access them.

## Conclusion

This project demonstrates how a scripted ServiceNow ACL can control record access based on field values.
## Users and Roles Creation

### Assigned Member
Sharvi-M-311624243037

### Task
Create the required users and roles in ServiceNow for the project.

### Planned Configuration
- Create the required ServiceNow users.
- Create the required roles.
- Assign appropriate roles to the users.
- Verify the user and role configuration.
- Use the configured users and roles for ACL testing.

### Status
In Progress

### Test Results
To be updated after the ServiceNow users and roles are created and tested.
