---
name: Senior Code Review
description: Perform a production-grade code review focusing on correctness, security, architecture, maintainability, and business requirements. Considers cross-feature data integration and side effects. Trigger this skill when the user asks for a code review or architectural review.
---

# Skill: Senior Code Review

## Purpose
Perform a production-grade code review that focuses on correctness, security, maintainability, performance, architecture, and business requirements—not code style alone. This skill conducts a production readiness review similar to approaches in large enterprise systems.

## AI Review Constraints
To ensure high-quality and relevant feedback, you must strictly follow these constraints:
- **Never recommend:** Rewrite architecture, Refactor for style only, Premature optimization, Pattern changes without measurable benefit.
- Prefer minimal changes that solve the issue.

## Review Philosophy
- Verify before commenting.
- Understand requirements before reviewing implementation.
- Review behavior, not coding style. Technical correctness is more important than subjective preferences.
- Every finding should include evidence.
- Do not suggest unnecessary complexity (YAGNI).
- Consider backward compatibility and production impact.

## The 5-Phase Review Workflow

### Phase 1: Architecture Understanding
Understand the system context, domain, and business flow before evaluating the implementation.
- **Domain Invariants Review:** Every domain has strict rules (e.g., Leave cannot be approved twice, Employee cannot approve themselves). Ensure no business invariant can be violated.
- **State Machine Validation:** Ensure valid transitions (e.g., Can Completed return to Draft? Can Deleted become Approved?).
- **Feature Interaction Review:** Analyze if the new feature breaks another feature (e.g., Leave -> Payroll -> Attendance -> Dashboard).

### Phase 2: Threat & Failure Modeling
Identify security threats, abuse, and failure scenarios before diving into code details.
- **Threat Modeling:** Beyond OWASP. Ask: What assets are protected? Who are the attackers? Trust/Privilege boundaries? Can a user edit hidden fields/salary/role? Can they modify approval hierarchy?
- **Input & State Validation:** Required, bounds, formats, duplicates.
- **Abuse Case Review:** Spam, double submit, rapid click, refresh, replay requests, huge payload, rate limit bypass, automation abuse.
- **Failure Scenario Review:** Database timeout -> Redis down -> SMTP fail -> Queue fail. Check for graceful degradation, retry, rollback, compensation, and circuit breakers.

### Phase 3: Cross-System Impact Analysis
Trace the impact of changes across modules, events, caches, and integrations.
- **Side Effect Analysis:** What else consumes this data? (e.g., Employee Update -> Payroll -> Reports). Identify cross-feature dependencies.
- **Event & Async Flow Review:** Queues, Kafka, Redis, Webhooks. Check for retry behavior, idempotency, lost events, ordering issues, dead letters, duplicate notifications, race conditions.
- **Distributed System Review:** Eventually consistent? Duplicate messages? Retry safe? Clock skew? Partial failure? Timeout? Network partition?
- **Data Migration Review:** Backward compatible? Rollback safe? Large table locks? Migration order? Data loss? Index rebuilds?
- **Cache Review:** Cache invalidation, cache stampede, TTL, stale data, cache poisoning, distributed cache consistency.
- **Financial/Data Accuracy Review:** Rounding, overflow, precision, currency, duplicate transactions, negative inventory.
- **API Contract Review:** Breaking responses? Nullable fields? Versioning? Deprecation? Will mobile apps or third-party integrations fail?

### Phase 4: Production Readiness Assessment
Ensure operational readiness, observability, scalability, and coverage.
- **Production Readiness:** Can we monitor this? Metrics, alerts, logs, feature flags, rollbacks, health checks, canary deployments?
- **Observability Review:** Tracing, correlation IDs, metrics, distributed tracing, request IDs, audit events.
- **Scalability Review:** From 100 to 1M users. Check for hot tables, lock contention, memory usage, cache, pagination, indexes, large payloads, streaming.
- **Permission Matrix Review:** Verify all roles across Read/Create/Update/Delete/Export/Approve actions.
- **Test Gap Analysis:** Missing Unit, Integration, API, E2E, Concurrency, Load, Security, Regression, or Mutation tests?
- **UI / UX Review:** Responsive, loading/empty/error states, accessibility (WCAG).

### Phase 5: Evidence & Confidence Validation
Every finding must be backed by evidence to minimize false positives.
- **AI-Assisted False Positive Verification:** Every finding MUST include Evidence, Reproduction path, Why current code fails, Why recommendation fixes it, and Confidence (High/Medium/Low). If Confidence is Low, flag as "Potential issue, Needs confirmation".
- **Risk Scoring:** Evaluate Severity, Likelihood, Impact, and Confidence (e.g., Severity: High, Likelihood: High, Impact: Critical, Confidence: 95%).
- **Root Cause Analysis:** Why did this happen? Architecture? Missing validation? Wrong abstraction? Bad ownership? Lack of transactions?
- **Performance Complexity:** Analyze Time Complexity, Space Complexity, Database Complexity, Query Count, Memory Allocation, Lock Duration.

## Severity Levels
- **Critical (Must be fixed before merge):** Security vulnerability, broken authorization, data corruption, broken business logic, race condition causing incorrect data, missing transaction.
- **High (Should be fixed before merge):** Incorrect validation, missing edge case, incorrect error handling, performance bottleneck, missing rollback, missing audit logging, API inconsistency.
- **Medium (Should be fixed soon):** Code duplication, large function, poor naming, maintainability issue, missing documentation, architectural drift.
- **Low (Optional improvements):** Simplification, minor refactoring, readability improvements.

## Findings Format
For each issue, strictly use the following structure:

### [Severity] Title
- **Location:** File, Function, Line
- **Problem:** Explain the issue clearly.
- **Risk Scoring:** Severity: [X], Likelihood: [X], Impact: [X], Confidence: [X]%
- **Root Cause Analysis:** Why did this happen? (e.g., missing validation, architecture)
- **Cross-System Impact:** Explain potential side effects across features.
- **Recommendation:** Provide a concrete, minimal fix.
- **Evidence & Reproduction:** Reference relevant code, why it fails, and steps to reproduce. Note if it's a potential issue needing confirmation (Low Confidence).

## Review Summary Format
At the end of your review, provide:
1. **Overall Assessment:** Ready to Merge / Ready After Minor Fixes / Changes Requested / Blocked
2. **Architecture & Data Integration Summary:** How this code fits into the overall architecture and impacts interconnected features.
3. **Critical Issues:** List all Critical findings.
4. **High Priority Issues:** List all High priority findings.
5. **Medium Priority Issues:** List all Medium findings.
6. **Low Priority Suggestions:** List all optional improvements.
7. **Positive Findings:** Highlight good implementation decisions.
