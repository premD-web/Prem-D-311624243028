# Script-Controlled ACL – Restrict Record Access Based on Field Value

## Project Overview

This project demonstrates how a ServiceNow Access Control List (ACL) can use a script to restrict access to records based on a field value.

## Objective

The objective of this project is to restrict access to sensitive Incident records and allow access only to authorized users.

## Technologies Used

- ServiceNow
- JavaScript
- ACL
- GitHub

## How It Works

1. A user tries to access an Incident record.
2. The ACL checks the value of the sensitive field.
3. If the record is not sensitive, access is allowed.
4. If the record is sensitive, the user's authorization is checked.
5. Unauthorized users are denied access.

## Project Structure

```text
script-controlled-acl/
│
├── README.md
│
├── scripts/
│   └── acl_script.js
│
├── screenshots/
│
└── documentation/
    └── project-report.md
