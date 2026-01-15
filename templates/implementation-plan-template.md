# Implementation Plan: {{FEATURE_NAME}}

**Created:** {{DATE}}
**PRD Reference:** `.claude/docs/prd-{{feature-name}}.md`
**Status:** Not Started | In Progress | Completed

---

## Overview

### Summary
{{Brief summary of what will be implemented}}

### Approach
{{High-level approach - TDD with incremental implementation}}

### Context Window Constraints
Each task is designed to:
- Complete within **50% of context window**
- Be independently testable
- Have minimal dependencies on other tasks
- Follow existing codebase patterns

---

## Task Execution Order

```
[Task 1: Tests] → [Task 1: Implementation] → [Run Tests] → [Repeat for next task] → [Final Review]
```

---

## Tasks

### Task 1: {{Task Name}}

**Status:** [ ] Not Started | [ ] Tests Written | [ ] Implemented | [ ] Verified

**Complexity:** Small | Medium | Large

**Prerequisites:** None

**Gherkin Scenarios Covered:**
- {{Scenario 1 reference}}
- {{Scenario 2 reference}}

#### 1.1 Test Phase
**Files to create/modify:**
- `{{test/path/to/test-file}}`

**Test cases:**
```
- [ ] Test: {{test case description}}
- [ ] Test: {{test case description}}
- [ ] Test: {{edge case description}}
```

**Invoke:** `@test-agent` with context:
```
Task: Write tests for {{task description}}
Scenarios: {{Gherkin scenarios}}
Test file: {{target test file}}
Pattern reference: {{existing similar test file}}
```

#### 1.2 Implementation Phase
**Files to modify:**
- `{{src/path/to/file}}`

**Changes required:**
- {{Specific change 1}}
- {{Specific change 2}}

**Invoke:** `@implementation-agent` with context:
```
Task: Implement {{task description}}
Make tests pass: {{test file reference}}
Pattern reference: {{existing similar implementation}}
```

#### 1.3 Verification
```bash
# Run tests
{{test command}}

# Expected: All tests pass
```

**Checklist:**
- [ ] All new tests pass
- [ ] No regression in existing tests
- [ ] Code follows project patterns

---

### Task 2: {{Task Name}}

**Status:** [ ] Not Started | [ ] Tests Written | [ ] Implemented | [ ] Verified

**Complexity:** Small | Medium | Large

**Prerequisites:** Task 1 complete

**Gherkin Scenarios Covered:**
- {{Scenario reference}}

#### 2.1 Test Phase
{{Same structure as Task 1}}

#### 2.2 Implementation Phase
{{Same structure as Task 1}}

#### 2.3 Verification
{{Same structure as Task 1}}

---

### Task N: {{Final Task Name}}

{{Same structure}}

---

## Final Verification

### All Tests Pass
```bash
# Run full test suite
{{full test command}}
```

### Coverage Check
```bash
# Check test coverage
{{coverage command}}
```

---

## Code Review Phase

**Status:** [ ] Not Started | [ ] In Progress | [ ] Approved

**Invoke:** `@review-agent`

### Review Checklist
- [ ] All acceptance criteria met
- [ ] Code follows project conventions
- [ ] No security vulnerabilities introduced
- [ ] No performance regressions
- [ ] Error handling is appropriate
- [ ] Edge cases are handled
- [ ] Tests are comprehensive

### Review Focus Areas
1. {{Specific area to review}}
2. {{Specific area to review}}
3. {{Specific area to review}}

---

## Completion Criteria

- [ ] All tasks completed
- [ ] All tests passing
- [ ] Code review approved
- [ ] PRD acceptance criteria verified
- [ ] Documentation updated (if needed)

---

## Notes

### Discovered Issues
{{Track any issues discovered during implementation}}

### Decisions Made
{{Document any implementation decisions}}

### Follow-up Tasks
{{Tasks identified but deferred}}
