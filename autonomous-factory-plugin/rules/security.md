# Security Guidelines

1. **Input Validation**: Never trust user input. Validate and sanitize everything at the application boundary.
2. **Authentication & Authorization**: Always verify both identity (who) and permissions (what they can do). Ensure IDOR checks are in place.
3. **Secrets Management**: Never hardcode API keys, passwords, or secrets. Use environment variables.
4. **Data Privacy**: Avoid logging sensitive information such as PII or passwords.
5. **Dependency Scanning**: Regularly check for known vulnerabilities in third-party libraries.
