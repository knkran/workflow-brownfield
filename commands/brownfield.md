---
description: Start the complete brownfield workflow (analysis + implementation)
argument-hint: "<feature or task description>"
allowed-tools: Bash(git:*), Bash(npm:*), Read, Write, Edit, Glob, Grep, Task, TodoWrite, AskUserQuestion, EnterPlanMode, ExitPlanMode
---

# Brownfield Development Workflow

A structured workflow for brownfield development supporting both well-defined user stories and ad-hoc tasks (like library upgrades).

**Feature to implement**: $ARGUMENTS

## Overview

This workflow guides you through two main phases:
1. **Analysis Phase** - Gather requirements, define scenarios, collect additional context
2. **Implementation Phase** - Create PRD, plan tasks, implement using TDD, review code

---

## PHASE 1: ANALYSIS

### Step 1.1: Requirement Extraction

First, determine the type of work:

Use AskUserQuestion to ask: **What type of task are you working on?**

Options:
1. **User Story** - I have a well-defined user story from the Product Owner
2. **Ad-hoc Task** - Library upgrade, tech debt, or undefined task

**If User Story selected:**
Ask the user to paste the complete user story including:
- Title
- Description
- Acceptance Criteria
- Any linked documentation or references

**If Ad-hoc Task selected:**
Gather information by asking:
- What is the goal of this task?
- What systems/components are affected?
- What is the current state vs desired state?
- Are there any constraints or dependencies?
- What is the definition of done?

### Step 1.2: Scenario Definition with Gherkin

Based on the requirements gathered, work with the user to define test scenarios using Gherkin syntax:

```gherkin
Feature: [Feature name from requirements]
  As a [role]
  I want [capability]
  So that [benefit]

  Background:
    Given [common preconditions]

  Scenario: [Scenario name]
    Given [initial context]
    When [action is taken]
    Then [expected outcome]
    And [additional outcomes]

  Scenario Outline: [Parameterized scenario name]
    Given [context with <parameter>]
    When [action with <parameter>]
    Then [outcome with <parameter>]

    Examples:
      | parameter | expected |
      | value1    | result1  |
      | value2    | result2  |
```

**Ask the user:**
- Are these scenarios complete?
- Are there edge cases we should consider?
- Are there error scenarios to handle?

### Step 1.3: Additional Information Gathering

Before proceeding to implementation, ensure you have:
- [ ] Clear understanding of the existing codebase structure
- [ ] Knowledge of existing test patterns in the project
- [ ] Understanding of dependencies and integrations
- [ ] Any technical constraints or requirements
- [ ] Coding standards and conventions used

**Ask clarifying questions** if any of the above is unclear.

---

## PHASE 2: IMPLEMENTATION

### Step 2.1: Create PRD and Implementation Plan

Create a PRD file at `.claude/docs/prd-[feature-name].md` using the template.

**Critical Requirement:** Break down the implementation into tasks where each task:
- Can be completed within 50% of the context window
- Is independently testable
- Has clear inputs and outputs
- Follows the existing codebase patterns

### Step 2.2: TDD Implementation Cycle

For each task in the implementation plan:

#### 2.2.1: Write Tests First (Use Test Agent)

Use the Task tool to invoke the test agent:
```
Task tool with subagent_type: "workflow-brownfield:test-agent"
```
- Write unit tests based on Gherkin scenarios
- Tests should fail initially (Red phase)
- Cover happy path and edge cases

#### 2.2.2: Implement Feature (Use Implementation Agent)

Use the Task tool to invoke the implementation agent:
```
Task tool with subagent_type: "workflow-brownfield:implementation-agent"
```
- Write minimal code to make tests pass (Green phase)
- Follow existing patterns in the codebase
- Keep changes focused and small

#### 2.2.3: Run Tests
- Execute the test suite
- Verify all new tests pass
- Ensure no regression in existing tests

#### 2.2.4: Refactor (if needed)
- Clean up code while keeping tests green
- Apply DRY principles
- Improve readability

**Repeat cycle for each task until all tasks are complete.**

### Step 2.3: Code Review (Use Review Agent)

Once all tests are green, use the Task tool to invoke the review agent:
```
Task tool with subagent_type: "workflow-brownfield:review-agent"
```
- Review all changes for quality
- Check adherence to coding standards
- Verify test coverage
- Identify potential issues

---

## Workflow Commands

- `/brownfield` - Start the brownfield workflow (this command)
- `/brownfield-analysis` - Run only the analysis phase
- `/brownfield-implement` - Continue to implementation (requires completed analysis)

---

## Files Created by This Workflow

- `.claude/docs/prd-[feature].md` - Product Requirements Document
- `.claude/docs/plan-[feature].md` - Implementation Plan
- `.claude/docs/scenarios-[feature].feature` - Gherkin scenarios
