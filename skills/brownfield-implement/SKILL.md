# Brownfield Implementation Phase

This skill handles the implementation phase of the brownfield development workflow.

## Prerequisites

Before running this phase:
- Analysis phase must be complete
- Analysis document must exist at `.claude/docs/analysis-[feature].md`

---

## Instructions

When this skill is invoked, follow these steps:

### Step 1: Load Analysis

1. **Find and read the analysis document**
   - Look for `.claude/docs/analysis-*.md`
   - If multiple exist, ask user which one to use
   - If none exist, inform user to run analysis first

2. **Extract key information**
   - Requirements summary
   - Gherkin scenarios
   - Technical context
   - Affected components

### Step 2: Create PRD

Using the PRD template structure (Overview, Requirements, Test Scenarios, Technical Considerations, Implementation Plan, Definition of Done):

1. **Generate PRD document**
   - Fill in all sections from analysis
   - Add technical details discovered during analysis
   - Include all Gherkin scenarios

2. **Break down into tasks**

   **CRITICAL:** Each task must fit within 50% of context window.

   Guidelines for task breakdown:
   - One Gherkin scenario per task (typically)
   - Complex scenarios may need multiple tasks
   - Group related small changes together
   - Each task should be independently testable

   Example breakdown:
   ```
   Original: Implement user authentication feature

   Task 1: Implement login validation (Scenario: Valid login)
   Task 2: Implement error handling (Scenarios: Invalid password, User not found)
   Task 3: Implement session management (Scenario: Session persistence)
   Task 4: Implement logout (Scenario: User logout)
   ```

3. **Save PRD**
   - Save to `.claude/docs/prd-[feature-name].md`

### Step 3: Create Implementation Plan

Using the implementation plan template structure (Task Execution Order, Per-Task Details, Progress Tracking, Final Verification):

1. **Define task execution order**
   - Consider dependencies between tasks
   - Start with foundational tasks
   - Build up complexity

2. **For each task, specify:**
   - Test file location
   - Implementation file location
   - Gherkin scenarios covered
   - Verification steps

3. **Save implementation plan**
   - Save to `.claude/docs/plan-[feature-name].md`

### Step 4: Confirm with User

Present the plan:

```
## Implementation Plan Created

PRD: .claude/docs/prd-[feature].md
Plan: .claude/docs/plan-[feature].md

### Task Overview

| # | Task | Scenarios | Complexity |
|---|------|-----------|------------|
| 1 | [Task 1] | [Scenarios] | [Size] |
| 2 | [Task 2] | [Scenarios] | [Size] |
...

### Execution Order
1. Task 1: Tests → Implementation → Verify
2. Task 2: Tests → Implementation → Verify
...
Final: Code Review

Ready to proceed with Task 1?
```

### Step 5: Execute TDD Cycle

For each task:

#### 5.1: Test Phase

Use the Task tool to invoke the test agent:
```
Task tool with subagent_type: "workflow-brownfield:test-agent"
Prompt: "Write tests for Task [N]: [Task description]. Scenarios: [Gherkin scenarios]. Target test file: [Test file]"
```

The test agent will write failing tests following TDD principles.

**After tests written:**
- Verify tests exist
- Run tests to confirm they fail
- Proceed to implementation

#### 5.2: Implementation Phase

Use the Task tool to invoke the implementation agent:
```
Task tool with subagent_type: "workflow-brownfield:implementation-agent"
Prompt: "Implement Task [N]: [Task description]. Test file: [Test file with failing tests]. Target files: [Implementation targets]"
```

The implementation agent will write code to make the failing tests pass.

**After implementation:**
- Run tests to confirm they pass
- If tests fail, continue implementation
- If tests pass, proceed to next task or review

#### 5.3: Verification
```bash
# Run task-specific tests
[test command] [test file]

# Run full test suite to check regressions
[test command]
```

**Update implementation plan status:**
- Mark task as complete
- Note any issues or discoveries
- Proceed to next task

### Step 6: Repeat for All Tasks

Continue the TDD cycle for each task until all tasks are complete.

Track progress:
```
## Progress Update

| Task | Tests | Implementation | Verified |
|------|-------|----------------|----------|
| 1 | [x] | [x] | [x] |
| 2 | [x] | [x] | [x] |
| 3 | [ ] | [ ] | [ ] |
...
```

### Step 7: Final Verification

When all tasks complete:

1. **Run full test suite**
   ```bash
   [full test command]
   ```

2. **Verify all tests pass**
   - No failures
   - No regressions

3. **Check coverage (if available)**
   ```bash
   [coverage command]
   ```

### Step 8: Code Review

When all tests are green, use the Task tool to invoke the review agent:
```
Task tool with subagent_type: "workflow-brownfield:review-agent"
Prompt: "Review the implementation for [Feature name]. All tests are passing. Review code quality, security, and test coverage."
```

The review agent will perform a comprehensive code review.

---

## Completion

When review is approved:

```
## Brownfield Workflow Complete!

### Summary
- Feature: [Feature name]
- Tasks completed: [N]
- Tests added: [N]
- Files modified: [N]

### Documents Created
- PRD: .claude/docs/prd-[feature].md
- Plan: .claude/docs/plan-[feature].md
- Analysis: .claude/docs/analysis-[feature].md

### Review Status
- Status: Approved
- Issues found: [N] (all resolved)

Ready for commit/merge!
```

---

## Handling Issues

### Tests Won't Pass
1. Review test expectations
2. Check implementation logic
3. Verify test setup is correct
4. Ask user for clarification if needed

### Task Too Large
1. Break task into smaller sub-tasks
2. Update implementation plan
3. Continue with smaller scope

### New Requirements Discovered
1. Document in implementation plan notes
2. If minor: add to current scope
3. If major: flag for user decision

### Review Rejection
1. Address all critical issues
2. Re-run affected tests
3. Request re-review
