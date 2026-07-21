---
name: test-case-generator
description: Generates comprehensive, production-ready test cases for any software feature across 18 categories (Functional, Security, Performance, etc.) and saves them to the project folder. Use when a user asks to generate test cases, test plans, or QA scenarios for a feature.
---

# Feature Test Case Generator

## Purpose
Generate comprehensive, production-ready test cases for any software feature before implementation or release. The goal is to find functional bugs, business logic errors, edge cases, security vulnerabilities, permission issues, data integrity problems, performance risks, UX inconsistencies, and regression risks.

## Instructions for the Agent

When the user invokes this skill, follow these steps strictly:

1. **Information Gathering & Flow Analysis**: Ask the user for the feature specification (PRD, User Story, API Docs, UI Mockup, etc.) if not fully provided. Use your context tools (like `lean-ctx`) to proactively search the project for relevant database schemas, API routes, existing UI components, and business rules. **Crucially, read the code flow and specification documents to evaluate potential vulnerabilities, estimating which bugs could be fatal vs non-fatal.** Explicitly identify any assumptions you make.
2. **Exhaustive Generation**: Generate test cases for **ALL** 18 categories listed below. Do not stop after a few examples; be exhaustive and detailed.
3. **Format**: Format all test cases using the Markdown table structure provided below.
4. **Save to Project Folder**: **DO NOT** just output the test cases in the chat. You MUST write the final output to a Markdown file directly in the user's project repository.
   - Default location: `docs/test-cases/<feature-name-or-issue-id>.md` (create the directory if it doesn't exist).
   - If the user specifies a different folder, follow their instruction.

---

## Document Structure

1. **System Flow Summary**: Start the document with a clear, easy-to-read summary of the system flow for the feature(s) being tested. Explain the core logic, actors, and workflow so the user can understand the feature at a glance.
2. **Test Cases**: Generate test cases in a Markdown table for each category.

| ID | Category | Scenario | Steps | Expected Result | Priority |
|----|----------|----------|-------|----------------|----------|

**Priority levels:**
- **Fatal** (System crash, data loss, severe security breach)
- **Critical** (Core business flow blocked)
- **High** (Major feature broken, but workaround exists)
- **Medium** (Minor bug, UI/UX issues)
- **Low** (Trivial issue, cosmetic)

---

## Test Categories (Generate for ALL)

### 1. Happy Path
Verify normal successful flow (e.g., Create successfully, Update successfully, Delete successfully, View successfully).

### 2. Validation
Test every input validation: Required field, Empty string, Max length, Min length, Invalid format, Invalid email, Invalid phone, Duplicate value, Unicode, Emoji, SQL keywords, HTML, JavaScript, XSS payload, SQL Injection payload.

### 3. Boundary Value Analysis
Test: Minimum, Maximum, Exactly minimum, Exactly maximum, One below minimum, One above maximum.

### 4. Business Rules
Verify every business rule (e.g., Cannot approve own request, Cannot cancel approved order, Only one active subscription, Leave balance cannot be negative, Stock cannot become negative).

### 5. Permission & Authorization
Generate tests for every role (Guest, Employee, Manager, HR, Finance, Admin, Super Admin). Verify: Read, Create, Update, Delete, Approve, Reject, Export, Import, API Access, Hidden UI, Direct URL access.

### 6. Authentication
Verify: Unauthenticated request, Expired token, Invalid token, Refresh token, Session timeout, Concurrent login, Logout, Password changed.

### 7. API Tests
Verify: GET, POST, PUT, PATCH, DELETE, Status code, Response schema, Headers, Pagination, Sorting, Filtering, Search, Invalid body, Malformed JSON, Unexpected fields, Mass Assignment, IDOR, Broken Object Level Authorization, Rate Limit.

### 8. Database Integrity
Verify: Foreign Key, Cascade Delete, Transaction Rollback, Duplicate Record, Soft Delete, Unique Constraint, Audit Log, Timestamp, Versioning, Concurrency.

### 9. File Upload (If applicable)
Test: PNG, JPEG, PDF, DOCX, ZIP, Executable, Large file, Empty file, Virus simulation, Double extension, Incorrect MIME Type.

### 10. UI / UX
Verify: Button disabled, Loading state, Skeleton, Empty state, Error state, Responsive, Dark mode, Accessibility, Keyboard navigation, Tab order, Focus, Tooltip, Modal behavior, Toast message, Confirmation dialog.

### 11. Performance
Verify: Large dataset, 100 users, 1000 users, Bulk operation, Pagination speed, Slow network, High latency, Memory usage, CPU usage.

### 12. Security
Generate security test cases including OWASP Top 10 (Broken Access Control, Cryptographic Failures, Injection, Insecure Design, Security Misconfiguration, Vulnerable Components, Authentication Failures, Software Integrity Failures, Logging Failures, SSRF). Also include: XSS, CSRF, SQL Injection, Path Traversal, Command Injection, XXE, Open Redirect, Clickjacking, JWT Manipulation, Replay Attack, Mass Assignment, IDOR, Privilege Escalation.

### 13. Negative Testing
Generate invalid scenarios: Unexpected null, Negative number, Decimal, Huge payload, Duplicate request, Network interruption, Timeout, Browser refresh, Double click, Multiple tabs, Race condition, Offline mode.

### 14. Concurrency
Generate concurrent access tests: Two users edit same record, Approve simultaneously, Delete while editing, Multiple browser tabs, Duplicate submission.

### 15. Integration
Verify interactions with: Authentication, Notification, Email, SMS, Payment, Inventory, Payroll, Attendance, HR, Third-party APIs, Webhooks, Queue, Scheduler, Cron.

### 16. Regression
Identify existing features that may be affected. Generate regression checklist.

### 17. Exploratory Testing
Generate exploratory ideas: Unexpected navigation, Rapid clicking, Browser Back, Browser Forward, Bookmark, Refresh, Offline, Zoom, Resize, Multiple monitors, Clipboard, Autofill, Accessibility tools.

### 18. Compatibility
Verify: Chrome, Firefox, Safari, Edge, Android, iOS, Tablet, Desktop, Different resolutions.

---

## Post-Test Case Analysis

At the end of the document, provide the following sections:

### High Risk Areas
List the most critical areas likely to fail (e.g., Permission checking, Approval workflow, Race condition, Database transaction, Data synchronization, Audit logging).

### Missing Test Coverage
Identify missing requirements that prevent complete testing (e.g., Approval rules undefined, Validation not specified, Role matrix unavailable, Error messages not documented, API contract missing).

### Automation Candidates
Recommend which test cases should be automated (Unit Test, Integration Test, API Test, E2E Test, Performance Test, Security Test). Explain why each is suitable for automation.

---

## Output Quality Requirements
- Must cover happy path and negative scenarios.
- Must cover edge cases and boundary values.
- Validate business rules thoroughly.
- Include security-focused scenarios based on OWASP Top 10.
- Verify role-based authorization and access control.
- Include API, database, UI, integration, and regression testing.
- Identify concurrency and race condition risks.
- Prioritize test cases clearly using the scale from Fatal to Low, taking into account the code flow analysis.
- Be implementation-independent and reusable across projects.
- Use clear, actionable language suitable for QA engineers and developers.
