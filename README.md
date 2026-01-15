# Brownfield Workflow Plugin for Claude Code

A structured development workflow plugin for Claude Code that enables Test-Driven Development (TDD) practices in existing codebases (brownfield projects).

## Features

- **Two-phase workflow**: Analysis followed by implementation
- **Gherkin scenario support**: Human-readable test definitions
- **TDD methodology**: Write tests first, implement second
- **Specialized agents**: Dedicated roles for testing, implementation, and code review
- **Task decomposition**: Breaking work into manageable context-window-friendly segments
- **Automated documentation**: Generates PRDs, analysis summaries, and implementation plans

## Installation

### Option 1: Install from GitHub (Recommended)

```bash
claude /plugin install knkran/workflow-brownfield
```

### Option 2: Manual Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/knkran/workflow-brownfield.git
   ```

2. Copy the plugin to your Claude Code plugins directory:
   ```bash
   cp -r workflow-brownfield ~/.claude/plugins/
   ```

3. Restart Claude Code

## Usage

### Available Commands

| Command | Description |
|---------|-------------|
| `/brownfield` | Start the complete workflow (analysis + implementation) |
| `/brownfield-analysis` | Run only the analysis phase |
| `/brownfield-implement` | Continue to implementation (requires completed analysis) |

### Workflow Overview

#### Phase 1: Analysis
1. **Task categorization** - Determine if working on a user story or ad-hoc task
2. **Requirement collection** - Gather all necessary information
3. **Gherkin scenario definition** - Define test scenarios in human-readable format
4. **Codebase exploration** - Understand existing patterns and conventions

#### Phase 2: Implementation
1. **PRD creation** - Generate Product Requirements Document
2. **Task decomposition** - Break work into context-window-friendly tasks
3. **TDD cycle** - For each task:
   - Write failing tests (Test Agent)
   - Implement code to pass tests (Implementation Agent)
   - Verify and refactor
4. **Code review** - Comprehensive review (Review Agent)

### Specialized Agents

| Agent | Purpose | Invocation |
|-------|---------|------------|
| **Test Agent** | Writes unit tests based on Gherkin scenarios | `workflow-brownfield:test-agent` |
| **Implementation Agent** | Writes code to make tests pass | `workflow-brownfield:implementation-agent` |
| **Review Agent** | Reviews code quality, security, and coverage | `workflow-brownfield:review-agent` |

## Generated Documentation

The workflow creates documentation in `.claude/docs/`:

| File | Description |
|------|-------------|
| `analysis-[feature].md` | Requirements and Gherkin scenarios |
| `prd-[feature].md` | Product Requirements Document |
| `plan-[feature].md` | Implementation plan with task breakdown |

## Requirements

- Claude Code CLI
- Git (for version control integration)

## Project Structure

```
workflow-brownfield/
├── .claude-plugin/
│   └── plugin.json           # Plugin configuration
├── agents/
│   ├── test-agent.md         # Test writing specialist
│   ├── implementation-agent.md  # Code implementation specialist
│   └── review-agent.md       # Code review specialist
├── templates/
│   ├── prd-template.md       # PRD template
│   └── implementation-plan-template.md  # Implementation plan template
├── skills/
│   ├── brownfield/           # Main workflow skill
│   ├── brownfield-analysis/  # Analysis phase skill
│   └── brownfield-implement/ # Implementation phase skill
├── README.md
└── LICENSE
```

## Contributing

Contributions are welcome! Please feel free to submit issues and pull requests.

## License

MIT License - see [LICENSE](LICENSE) for details.
