# Testing Requirements

1. **Test Coverage**: All new business logic MUST have corresponding unit tests.
2. **Integration Tests**: Critical pathways and workflows require integration testing.
3. **Edge Cases**: Always write tests for negative scenarios, boundary conditions, and invalid inputs.
4. **Reproducibility**: Tests must be reliable and not flaky. Do not depend on external live services in unit tests (use mocks).
5. **No Blind Output**: The QA agent MUST execute tests and verify output before reporting PASS/FAIL.
