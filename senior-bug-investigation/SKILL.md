---
name: Senior Bug Investigation
description: Investigate production-grade bugs by understanding business requirements, reproducing user behavior, tracing data flow, validating business rules, analyzing cross-feature impacts, identifying root causes, and generating a comprehensive Markdown investigation report. Trigger this skill whenever a user reports a bug, unexpected behavior, production issue, regression, or requests root cause analysis.
---

# Senior Bug Investigation

## Objective

Identify the true root cause of bugs instead of merely fixing symptoms.

The investigation must be evidence-based and verify every finding against the current codebase, application flow, database, and business requirements.

The goal is to answer:

- What happened?
- Why did it happen?
- Where did it originate?
- How can it be reproduced?
- What other features are affected?
- What is the safest fix?
- How can similar bugs be prevented?

Never guess.
Always verify.

---

# Investigation Philosophy

The investigation follows this order:

Understand Business

↓

Reproduce User Behavior

↓

Trace Data Flow

↓

Identify Divergence

↓

Find Root Cause

↓

Analyze Side Effects

↓

Recommend Fix

↓

Prevent Regression

Never start by reading random code.

Understand the business workflow first.

---

# Investigation Workflow

## Phase 1 — Understand the Feature

Read the related feature before opening implementation.

Determine:

- Business objective
- Expected workflow
- Actors
- Permissions
- State transitions
- Related modules
- Data ownership

Identify all business invariants.

Examples:

- Leave cannot be approved twice.
- Employee cannot approve themselves.
- Salary report only uses approved payroll.
- Attendance cannot overlap.
- Inventory cannot become negative.

---

## Phase 2 — Understand User Behavior

Determine exactly how users trigger the bug.

Generate a complete user scenario.

Include:

- User role
- Initial system state
- Preconditions
- Every UI action
- API requests
- Background jobs
- Database changes
- Final incorrect behavior

Produce a complete step-by-step sequence.

Example:

Employee Login

↓

Open Leave Page

↓

Create Leave Request

↓

Manager Approval

↓

Payroll Generation

↓

Attendance Calculation

↓

Incorrect Salary

If multiple paths exist, analyze every possible path.

---

## Phase 3 — Reproduce the Bug

Determine whether the bug can be reproduced.

Document:

Environment

Browser

Device

Role

Input

Database state

Feature flags

Configuration

External services

Cache state

Queue state

Reproduction Steps

Expected Result

Actual Result

Reproducibility

Always classify:

Always

Intermittent

Rare

Unknown

---

## Phase 4 — Trace Complete Data Flow

Trace data from beginning to end.

UI

↓

API

↓

Controller

↓

Service

↓

Repository

↓

Database

↓

Events

↓

Queue

↓

Notification

↓

Reports

↓

Dashboard

↓

Frontend

Verify every transformation.

Never skip intermediate layers.

---

## Phase 5 — Locate Divergence

Compare expected behavior with actual behavior.

Find the first location where data becomes incorrect.

Examples:

Input correct

↓

Validation incorrect

↓

Database correct

↓

Mapper incorrect

↓

Response incorrect

↓

Frontend broken

The first incorrect behavior is usually close to the root cause.

---

## Phase 6 — Root Cause Analysis

Determine why the bug exists.

Possible categories:

Business logic

Missing validation

Authorization

State transition

Race condition

Missing transaction

Concurrency

Cache

Queue

Incorrect query

Wrong assumption

Data migration

Regression

Architecture

Third-party dependency

Configuration

Infrastructure

Explain why the implementation produced incorrect behavior.

Never stop at the symptom.

---

## Phase 7 — Business Rule Validation

Validate implementation against requirements.

Questions:

Does workflow follow business rules?

Can invalid states occur?

Can duplicate operations occur?

Can users bypass approval?

Can unauthorized users modify data?

Can historical data become inconsistent?

Can reports become incorrect?

---

## Phase 8 — Security Investigation

Review:

Authentication

Authorization

IDOR

Privilege escalation

Mass assignment

SQL Injection

XSS

CSRF

Sensitive information exposure

Secrets

Rate limiting

Replay attacks

---

## Phase 9 — Database Investigation

Inspect:

Constraints

Foreign keys

Indexes

Transactions

Rollback

Soft delete

Audit log

Triggers

Data consistency

Historical records

Versioning

Migration compatibility

Determine whether incorrect data has already been persisted.

---

## Phase 10 — State Machine Validation

Review every state transition.

Example:

Draft

↓

Submitted

↓

Approved

↓

Completed

Validate:

Illegal transitions

Duplicate transitions

Missing transitions

Rollback

Cancellation

Reopening

---

## Phase 11 — Cross Feature Impact

Determine all affected modules.

Examples:

Employee

↓

Attendance

↓

Payroll

↓

Leave

↓

Approval

↓

Reports

↓

Dashboard

↓

Notification

↓

API

↓

Mobile

List every downstream dependency.

---

## Phase 12 — Performance Investigation

Inspect:

N+1 queries

Large loops

Full table scan

Missing index

Memory usage

CPU usage

Lock contention

Slow queries

Timeout

Deadlock

---

## Phase 13 — Concurrency Investigation

Analyze:

Simultaneous updates

Duplicate requests

Retry behavior

Queue duplication

Lost update

Race condition

Idempotency

Distributed locking

---

## Phase 14 — Failure Scenario Analysis

Simulate failures.

Database unavailable

Redis unavailable

Queue delayed

SMTP failure

Storage unavailable

Webhook failure

Network timeout

Partial commit

Unexpected restart

Determine whether recovery is correct.

---

## Phase 15 — Regression Analysis

Determine whether fixing this bug could introduce another bug.

Review:

Existing APIs

Reports

Background jobs

Other modules

Historical data

Mobile apps

Integrations

Backward compatibility

---

## Phase 16 — Prevention Analysis

Recommend preventive improvements.

Possible actions:

New validation

Database constraint

Transaction

Additional tests

Architecture improvement

Monitoring

Alerting

Feature flag

Audit logging

Metrics

Documentation

---

# Evidence Rules

Every finding must include evidence.

Evidence may include:

Relevant code

Execution flow

Database records

Log entries

API response

Stack trace

Query result

Requirement

Never make unsupported claims.

---

# Confidence Score

Each finding must include:

High

Medium

Low

Only High confidence findings should be treated as confirmed bugs.

---

# Severity

Critical

High

Medium

Low

---

# Investigation Report

Generate a Markdown report.

The report must contain the following sections.

# Bug Investigation Report

## Executive Summary

Short description.

Severity.

Business impact.

Confidence.

---

## Feature Overview

Describe:

Purpose

Business workflow

Actors

Permissions

State transitions

Related modules

---

## User Journey

Describe every user action that leads to the bug.

Step-by-step.

Include:

User

Screen

Action

Expected result

Actual result

API

Database changes

---

## Reproduction Steps

Numbered steps.

Expected result.

Actual result.

Environment.

---

## Data Flow Analysis

Trace every layer.

Highlight where data diverges.

---

## Root Cause Analysis

Explain:

Why

How

Where

Evidence

Confidence

---

## Business Rule Validation

List violated business rules.

---

## Security Findings

If any.

---

## Database Findings

If any.

---

## State Transition Analysis

Diagram every state involved.

---

## Cross Feature Impact

List all affected modules.

Explain downstream effects.

---

## Regression Risk

High

Medium

Low

Explain why.

---

## Recommended Fix

Describe the smallest safe fix.

Avoid unnecessary refactoring.

---

## Prevention Recommendations

Additional validation

Tests

Monitoring

Architecture

Documentation

---

## Testing Checklist

Unit Test

Integration Test

API Test

Regression Test

Security Test

Concurrency Test

Performance Test

E2E Test

---

## Final Assessment

Root cause confirmed?

Confidence

Severity

Production impact

Recommended priority
