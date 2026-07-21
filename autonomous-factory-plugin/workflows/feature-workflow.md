# Feature Workflow

This file defines the state machine transitions for the Orchestrator, incorporating all specialized agents.

## Phases
1. **PRODUCT_OWNER**: Clarifies requirements (PRDs). Next -> REQUIREMENT_ANALYST.
2. **REQUIREMENT_ANALYST**: Transforms PRDs to Technical Requirements. Next -> SOLUTION_ARCHITECT.
3. **SOLUTION_ARCHITECT**: System Architecture & APIs. Next -> DATABASE_ARCHITECT.
4. **DATABASE_ARCHITECT**: DB Schema, ERDs, Migrations. Next -> BACKEND_LEAD.
5. **BACKEND_LEAD**: Designs backend scaffolding. Next -> BACKEND_DEVELOPER.
6. **BACKEND_DEVELOPER**: Implements backend code. Next -> FRONTEND_LEAD.
7. **FRONTEND_LEAD**: Designs UI updates & state. Next -> FRONTEND_DEVELOPER.
8. **FRONTEND_DEVELOPER**: Implements frontend code. Next -> INTEGRATION_AGENT.
9. **INTEGRATION_AGENT**: Ensures end-to-end connectivity. Next -> SECURITY_REVIEWER.
10. **SECURITY_REVIEWER**: Reviews for vulnerabilities.
    - If PASS: Next -> PERFORMANCE_REVIEWER.
    - If FAIL: Target -> BACKEND_DEVELOPER or FRONTEND_DEVELOPER (increment `security` retry count).
11. **PERFORMANCE_REVIEWER**: Checks performance bottlenecks.
    - If PASS: Next -> CODE_REVIEWER.
    - If FAIL: Target -> BACKEND_DEVELOPER or FRONTEND_DEVELOPER (increment `performance` retry count).
12. **CODE_REVIEWER**: General code & architecture review.
    - If PASS: Next -> REGRESSION_IMPACT_AGENT.
    - If FAIL: Target -> BACKEND_DEVELOPER or FRONTEND_DEVELOPER (increment `review` retry count).
13. **REGRESSION_IMPACT_AGENT**: Analyzes existing modules impacted. Next -> QA_ENGINEER.
14. **QA_ENGINEER**: Generates/runs automated test cases.
    - If PASS: Next -> DEVOPS_ENGINEER.
    - If FAIL: Target -> BACKEND_DEVELOPER or FRONTEND_DEVELOPER (increment `qa` retry count).
15. **DEVOPS_ENGINEER**: Docker, Github Actions, Deployment. Next -> DOCUMENTATION_AGENT.
16. **DOCUMENTATION_AGENT**: Updates READMEs, Swagger, Architecture records. Next -> DEPENDENCY_RELEASE_AGENT.
17. **DEPENDENCY_RELEASE_AGENT**: Dependency changes & Release notes. Next -> RELEASE.
18. **RELEASE**: Done.

## Escalate Conditions
If `retry_counts.security` > `max_retries` OR `retry_counts.performance` > `max_retries` OR `retry_counts.review` > `max_retries` OR `retry_counts.qa` > `max_retries`, halt and escalate to human.
