# Universal Agent Rules (Autonomous Factory)

All agents operating within this workspace MUST adhere to the following baseline rules. These rules dictate the general behavior, safety boundaries, and code quality expectations for any task undertaken.

- **Coding Standards**: See `rules/coding.md`
- **Security Guidelines**: See `rules/security.md`
- **Testing Requirements**: See `rules/testing.md`

## Structural Output Requirement
When acting within a specific phase defined by the Orchestrator, all agents MUST provide their final output in a strict structured JSON format. This allows the Orchestrator to parse results and trigger the next appropriate state or retry loop automatically.
