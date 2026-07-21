---
name: code-review-skill
description: Checklist and best practices for code reviews.
---

# Code Review Skill

This skill contains the checklist and strategies to review code correctly.

## 1. Security Check
- Are there any hardcoded secrets?
- Is user input validated?
- Are permissions checked?

## 2. Correctness
- Does the code fulfill the requirement?
- Are there off-by-one errors?
- Do all boundary tests pass mentally?

## 3. Architecture
- Are dependencies flowing correctly?
- Are we violating DRY or SOLID principles unnecessarily?

*This skill is strictly for reviewing, not implementing.*
