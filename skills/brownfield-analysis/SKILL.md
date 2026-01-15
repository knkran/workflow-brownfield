# Brownfield Analysis Phase

This skill handles the analysis phase of the brownfield development workflow.

## Instructions

When this skill is invoked, follow these steps exactly:

### Step 1: Determine Task Type

Use AskUserQuestion to determine the type of work:

**Question:** "What type of task are you working on?"

**Options:**
1. **User Story** - "I have a well-defined user story from the Product Owner that I can paste"
2. **Ad-hoc Task** - "Library upgrade, technical debt, refactoring, or task without formal user story"

---

### Step 2A: User Story Extraction (if User Story selected)

Ask the user to provide the user story:

```
Please paste your complete user story. Include:

- **Title**: The user story title
- **Description**: Full description/narrative
- **Acceptance Criteria**: All acceptance criteria
- **Technical Notes**: Any technical requirements or constraints
- **Dependencies**: Related stories or dependencies
- **Links**: Any relevant documentation links

Paste your user story below:
```

After receiving the user story, confirm understanding by summarizing:
- The main goal
- Key acceptance criteria
- Technical considerations

Ask: "Is this understanding correct? Are there any clarifications needed?"

---

### Step 2B: Ad-hoc Task Extraction (if Ad-hoc Task selected)

Gather requirements through a series of questions:

**Question 1:** "What is the goal of this task? Describe what needs to be accomplished."

**Question 2:** "What systems, components, or files are affected by this change?"

**Question 3:** "Describe the current state (what exists now) and the desired state (what should exist after)."

**Question 4:** "Are there any constraints, dependencies, or risks to consider?"

**Question 5:** "What is your definition of done? How will we know this task is complete?"

---

### Step 3: Gherkin Scenario Definition

Based on the gathered requirements, propose Gherkin scenarios:

```
Based on the requirements, I'll draft test scenarios in Gherkin format.
These scenarios will drive our TDD implementation.
```

Create scenarios covering:
1. **Happy path scenarios** - Main success cases
2. **Alternative paths** - Valid alternative flows
3. **Edge cases** - Boundary conditions
4. **Error scenarios** - Error handling and validation

Format:
```gherkin
Feature: [Feature name derived from requirements]
  As a [user role]
  I want [capability/action]
  So that [business value/benefit]

  Background:
    Given [common setup steps]

  @happy-path
  Scenario: [Primary success scenario]
    Given [precondition]
    And [additional precondition]
    When [action]
    Then [expected outcome]
    And [additional expected outcome]

  @alternative
  Scenario: [Alternative flow scenario]
    Given [different precondition]
    When [action]
    Then [different but valid outcome]

  @edge-case
  Scenario: [Boundary condition scenario]
    Given [edge case setup]
    When [action at boundary]
    Then [expected boundary behavior]

  @error
  Scenario: [Error handling scenario]
    Given [setup that will cause error]
    When [action that triggers error]
    Then [error should be handled gracefully]
    And [appropriate error message shown]
```

**After presenting scenarios, ask:**
1. "Are these scenarios complete and accurate?"
2. "Are there additional scenarios we should consider?"
3. "Should any scenarios be modified or removed?"

---

### Step 4: Additional Context Gathering

Before completing analysis, verify you have sufficient context:

**Codebase Understanding:**
- Use Glob and Grep to explore relevant parts of the codebase
- Identify existing patterns for similar features
- Find related tests to understand testing patterns

**Ask if needed:**
- "What testing framework does this project use?"
- "Are there existing similar features I should reference?"
- "Are there specific coding conventions I should follow?"
- "What is the project's branching/commit strategy?"

---

### Step 5: Analysis Summary

Create a summary document with all gathered information:

```markdown
# Analysis Summary: [Feature/Task Name]

## Requirements Source
[User Story | Ad-hoc Task]

## Summary
[Brief summary of what needs to be done]

## Detailed Requirements
[Full requirements as gathered]

## Gherkin Scenarios
[All defined scenarios]

## Technical Context
- Affected files/components: [list]
- Testing framework: [identified framework]
- Related code patterns: [references]

## Open Questions
[Any unresolved questions]

## Ready for Implementation
[ ] Requirements are clear
[ ] Scenarios are complete
[ ] Technical context is understood
[ ] No blocking questions remain
```

Save this to `.claude/docs/analysis-[feature-name].md`

---

### Completion

When analysis is complete, inform the user:

```
Analysis phase complete!

Created: .claude/docs/analysis-[feature-name].md

Next steps:
1. Review the analysis summary
2. Run `/brownfield-implement` to start the implementation phase
   - This will create a PRD and implementation plan
   - Then proceed with TDD implementation

Ready to proceed to implementation?
```
