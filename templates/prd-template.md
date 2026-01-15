# Product Requirements Document: {{FEATURE_NAME}}

**Document Version:** 1.0
**Created:** {{DATE}}
**Status:** Draft | In Review | Approved

---

## 1. Overview

### 1.1 Summary
{{Brief 2-3 sentence summary of the feature/task}}

### 1.2 Background
{{Context about why this work is needed. What problem does it solve?}}

### 1.3 Goals
- {{Primary goal}}
- {{Secondary goals}}

### 1.4 Non-Goals
- {{What this work explicitly does NOT include}}

---

## 2. Requirements

### 2.1 Functional Requirements

| ID | Requirement | Priority | Notes |
|----|-------------|----------|-------|
| FR-001 | {{Requirement description}} | Must Have | {{Notes}} |
| FR-002 | {{Requirement description}} | Should Have | {{Notes}} |
| FR-003 | {{Requirement description}} | Nice to Have | {{Notes}} |

### 2.2 Non-Functional Requirements

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| NFR-001 | Performance | {{Criteria}} |
| NFR-002 | Security | {{Criteria}} |
| NFR-003 | Compatibility | {{Criteria}} |

### 2.3 Acceptance Criteria
{{List acceptance criteria from user story or derived from requirements}}

- [ ] {{Criterion 1}}
- [ ] {{Criterion 2}}
- [ ] {{Criterion 3}}

---

## 3. Test Scenarios (Gherkin)

### 3.1 Feature Definition
```gherkin
Feature: {{Feature name}}
  As a {{user role}}
  I want {{capability}}
  So that {{benefit}}
```

### 3.2 Scenarios

#### Happy Path
```gherkin
Scenario: {{Primary success scenario}}
  Given {{precondition}}
  When {{action}}
  Then {{expected outcome}}
```

#### Alternative Flows
```gherkin
Scenario: {{Alternative scenario}}
  Given {{different precondition}}
  When {{action}}
  Then {{alternative outcome}}
```

#### Edge Cases
```gherkin
Scenario: {{Edge case scenario}}
  Given {{boundary condition}}
  When {{action}}
  Then {{expected boundary behavior}}
```

#### Error Handling
```gherkin
Scenario: {{Error scenario}}
  Given {{error-inducing condition}}
  When {{action}}
  Then {{graceful error handling}}
```

---

## 4. Technical Considerations

### 4.1 Affected Components
| Component | Type of Change | Impact |
|-----------|----------------|--------|
| {{File/Module}} | New / Modified / Deleted | {{Impact description}} |

### 4.2 Dependencies
- {{Internal dependency}}
- {{External dependency}}

### 4.3 Technical Constraints
- {{Constraint 1}}
- {{Constraint 2}}

### 4.4 Risks and Mitigations
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| {{Risk}} | Low/Medium/High | Low/Medium/High | {{Mitigation strategy}} |

---

## 5. Implementation Plan

### 5.1 Task Breakdown

**IMPORTANT:** Each task must be completable within 50% of context window.

| Task # | Description | Estimated Complexity | Dependencies | Test Coverage |
|--------|-------------|---------------------|--------------|---------------|
| 1 | {{Task description}} | Small/Medium/Large | None | {{Related scenarios}} |
| 2 | {{Task description}} | Small/Medium/Large | Task 1 | {{Related scenarios}} |
| 3 | {{Task description}} | Small/Medium/Large | Task 1, 2 | {{Related scenarios}} |

### 5.2 Task Details

#### Task 1: {{Task Title}}
**Description:** {{Detailed description}}

**Scope:**
- {{Specific change 1}}
- {{Specific change 2}}

**Test Scenarios Covered:**
- {{Scenario reference}}

**Files to Modify:**
- `{{path/to/file}}`

**Definition of Done:**
- [ ] Tests written and passing
- [ ] Implementation complete
- [ ] Code reviewed

---

#### Task 2: {{Task Title}}
{{Same structure as Task 1}}

---

## 6. Definition of Done

### 6.1 Implementation Complete
- [ ] All tasks completed
- [ ] All tests passing
- [ ] No regressions introduced

### 6.2 Quality Criteria
- [ ] Code follows project conventions
- [ ] Code reviewed and approved
- [ ] Documentation updated (if applicable)

### 6.3 Verification
- [ ] All Gherkin scenarios verified
- [ ] Edge cases handled
- [ ] Error scenarios handled

---

## Appendix

### A. Related Documents
- {{Link to related documentation}}

### B. Glossary
- **{{Term}}**: {{Definition}}

### C. Change Log
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | {{DATE}} | {{Author}} | Initial draft |
