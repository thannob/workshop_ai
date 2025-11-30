# Speckit Constitution

<!--
SYNC IMPACT REPORT (2025-11-30)
================================================================
VERSION CHANGE: None → 1.0.0 (MAJOR - Initial Constitution)

CHANGE SUMMARY:
- Constitution created from template
- Established 5 core principles aligned with speckit workflow
- Defined quality gates and governance model
- Set primary timezone to GMT+7 (Bangkok/Asia)

PRINCIPLES DEFINED:
1. Specification-First Development (NEW)
2. Incremental Planning (NEW)
3. Test-Driven Development (NEW)
4. Documentation as Code (NEW)
5. Safety-First Operations (NEW)

SECTIONS ADDED:
- Core Principles (5 principles)
- Quality Gates
- Development Workflow
- Governance

TEMPLATES REQUIRING UPDATES:
✅ .specify/templates/plan-template.md - Constitution Check section references this file
✅ .specify/templates/spec-template.md - Aligned with spec-first principle
✅ .specify/templates/tasks-template.md - Aligned with incremental planning & TDD
⚠ .claude/commands/*.md - Review for agent-specific references (not generic)

FOLLOW-UP TODOS:
- None - all placeholders filled
- Templates validated for consistency

RATIONALE FOR VERSION 1.0.0:
- Initial constitution establishing governance framework
- Major version appropriate for first ratification
- Sets baseline for all future amendments
================================================================
-->

## Core Principles

### I. Specification-First Development

Every feature begins with a detailed specification BEFORE any implementation work starts. Specifications must be created using the `/speckit.specify` command and include:

- **User scenarios** with prioritized user stories (P1, P2, P3...)
- **Functional requirements** (FR-XXX format) that are testable and clear
- **Success criteria** that are measurable and technology-agnostic
- **Edge cases** that define boundary conditions and error scenarios

**Rationale**: Clear specifications prevent scope creep, enable better planning, ensure stakeholder alignment, and provide a single source of truth for what "done" means. Specifications serve as contracts between intent and implementation.

**Non-negotiable**: No code may be written until the specification is approved by stakeholders. Clarifications must be resolved using `/speckit.clarify` before proceeding to planning.

### II. Incremental Planning

Complex features are broken down into manageable phases following the research → design → tasks workflow. Planning must be created using the `/speckit.plan` command and produce:

- **Phase 0 (Research)**: Technical context, dependency analysis, pattern identification
- **Phase 1 (Design)**: Data models, API contracts, component architecture, quickstart guide
- **Phase 2 (Tasks)**: Dependency-ordered task list generated via `/speckit.tasks`

**Rationale**: Breaking work into 1-hour implementation chunks maintains focus, enables parallel work, provides clear progress milestones, and reduces cognitive load. Each phase builds on the previous, creating a clear path from concept to code.

**Non-negotiable**: Plans must identify the minimum viable implementation (P1 user story only) that delivers standalone value. Features that cannot be scoped to <8 hours for MVP must be split into smaller features.

### III. Test-Driven Development

Tests are written FIRST, must FAIL initially, and must be approved BEFORE implementation begins. Testing discipline includes:

- **Contract tests**: Verify API/interface contracts match specifications
- **Integration tests**: Validate user journeys from spec match actual behavior
- **Unit tests**: Cover business logic and edge cases (optional unless specified)
- **Red-Green-Refactor**: Tests fail (red) → implement (green) → improve (refactor)

**Rationale**: TDD ensures code meets requirements, prevents regression, improves design through testability constraints, and provides living documentation of expected behavior.

**Non-negotiable**: For any feature where tests are explicitly requested in the specification, tests must be written and verified to fail BEFORE any implementation code. Implementation without failing tests first is prohibited.

### IV. Documentation as Code

All planning artifacts, specifications, and session records are stored as versioned markdown in the repository:

- **Specifications**: `/specs/[###-feature]/spec.md` (from `/speckit.specify`)
- **Plans**: `/specs/[###-feature]/plan.md` (from `/speckit.plan`)
- **Tasks**: `/specs/[###-feature]/tasks.md` (from `/speckit.tasks`)
- **Research artifacts**: `research.md`, `data-model.md`, `contracts/`, `quickstart.md`
- **Retrospectives**: `retrospectives/YYYY/MM/YYYY-MM-DD_HH-MM_retrospective.md`
- **Context issues**: GitHub issues with `context:` label for session state preservation

**Rationale**: Documentation in version control creates an audit trail, enables collaboration, survives across sessions, and integrates with standard development workflows. Markdown ensures readability, searchability, and tool independence.

**Non-negotiable**: All planning commands (`/speckit.specify`, `/speckit.plan`, `/speckit.tasks`) MUST write output to the designated file paths. Session retrospectives created with `rrr` short code MUST include AI Diary and Honest Feedback sections - these are mandatory for context preservation.

### V. Safety-First Operations

All operations prioritize reversibility, auditability, and data preservation:

- **Version Control**: No force pushes, no destructive git operations, safe merge practices only
- **File Operations**: No `rm -rf`, interactive confirmations for deletions, prefer edits over rewrites
- **Pull Requests**: NEVER merge PRs without explicit user permission - only provide PR links
- **Command Safety**: No `-f` or `--force` flags, verbose output for transparency
- **Package Management**: Lockfile changes reviewed, no blind updates

**Rationale**: Safety-first prevents data loss, maintains project history, enables rollback, builds trust, and supports collaborative workflows. AI assistants must prioritize caution over speed.

**Non-negotiable**: Any operation that could result in data loss or history corruption is PROHIBITED unless explicitly requested by the user with full understanding of implications. The user reviews and approves all PRs - the AI assistant only creates them.

## Quality Gates

*GATE: Constitutional compliance must be verified before proceeding with implementation*

All features must pass constitution alignment checks at key milestones:

### Before Phase 0 (Research)
- [ ] Specification exists and is approved (`/speckit.specify` completed)
- [ ] User stories prioritized with independent test criteria
- [ ] Functional requirements use FR-XXX format and are testable
- [ ] Success criteria are measurable and technology-agnostic

### After Phase 1 (Design)
- [ ] Plan includes Constitution Check section with validation results
- [ ] MVP scope (P1) identified and achievable in <8 hours
- [ ] Project structure matches one of the standard layouts (single/web/mobile)
- [ ] If tests requested: Test strategy defined before task generation
- [ ] Complexity violations justified in Complexity Tracking table (if any)

### After Phase 2 (Task Generation)
- [ ] Tasks organized by user story with [Story] labels (US1, US2, etc.)
- [ ] Each user story is independently implementable and testable
- [ ] Test tasks (if requested) marked to run BEFORE implementation tasks
- [ ] Parallel opportunities marked with [P] for efficiency
- [ ] Dependencies clearly documented with execution order

### At Implementation Time
- [ ] Tests written first and verified to fail (if tests requested)
- [ ] Implementation follows task order and dependency graph
- [ ] Commits reference task IDs and user stories
- [ ] No force operations or destructive commands used

### Before PR Creation
- [ ] All tests pass (if tests exist)
- [ ] Documentation updated per Documentation as Code principle
- [ ] Retrospective planned (use `rrr` for session documentation)
- [ ] PR body links to spec and task tracking issue

## Development Workflow

### Context Management (ccc → nnn → gogogo)

**Context Capture (`ccc`)**:
1. Gather git status, recent commits, branch info
2. Create GitHub issue with `context:` label capturing session state
3. Compact conversation to preserve tokens

**Planning (`nnn`)**:
1. Check for recent context issue (auto-run `ccc` if missing)
2. Analyze specification and codebase
3. Create comprehensive plan issue with `plan:` label
4. Execute `/speckit.plan` to generate planning artifacts

**Implementation (`gogogo`)**:
1. Locate most recent `plan:` issue
2. Execute `/speckit.tasks` to generate task breakdown
3. Implement step-by-step following task dependencies
4. Test and verify (tests must pass if TDD applied)
5. Commit with descriptive messages linking tasks
6. Create PR (NEVER merge - provide link for user review)

**Retrospective (`rrr`)**:
1. Gather session data (git diff, commits, timeline)
2. Create retrospective in `retrospectives/YYYY/MM/` with ALL sections
3. **MANDATORY**: Complete AI Diary (first-person narrative) and Honest Feedback (frank assessment)
4. Update `claude.md` with lessons learned (append to bottom only)
5. Commit retrospective and link to relevant issue/PR

### Short Code Reference

- **`lll`**: List project status (issues, PRs, commits) - get current state overview
- **`ccc`**: Create context issue and compact conversation
- **`nnn`**: Smart planning (auto-runs `ccc` if needed, then creates implementation plan)
- **`gogogo`**: Execute the most recent plan step-by-step
- **`rrr`**: Create detailed session retrospective (AI Diary & Honest Feedback REQUIRED)

### Time Zone Standard

**Primary Time Zone**: GMT+7 (Bangkok/Asia)

All timestamps in retrospectives, session logs, and user-facing documentation MUST show GMT+7 time first, with UTC in parentheses for reference.

**Example**: `15:30 GMT+7 (08:30 UTC)`

**Filenames**: May use UTC for technical consistency (e.g., `2025-11-30_08-30_retrospective.md`)

**Rationale**: Matches user's observed preference and working timezone, improving readability and reducing mental conversion overhead.

## Governance

### Amendment Process

This constitution supersedes all other development practices and guidelines. Amendments require:

1. **Proposal**: Document proposed change with rationale and impact analysis
2. **Review**: Evaluate consistency with existing principles and template dependencies
3. **Version Increment**: Follow semantic versioning (MAJOR.MINOR.PATCH)
   - **MAJOR**: Backward-incompatible governance changes, principle removals/redefinitions
   - **MINOR**: New principles added, materially expanded guidance
   - **PATCH**: Clarifications, wording improvements, typo fixes
4. **Sync Check**: Update all dependent templates (plan, spec, tasks, commands)
5. **Approval**: User must explicitly approve constitutional amendments
6. **Migration**: If existing features affected, provide migration guidance

### Compliance & Enforcement

- All planning commands (`/speckit.*`) automatically enforce constitutional principles
- The `Constitution Check` section in `plan.md` verifies compliance at design time
- The `/speckit.analyze` command performs cross-artifact consistency validation
- Violations must be justified in the `Complexity Tracking` table with:
  - What principle is being violated
  - Why the violation is necessary
  - What simpler alternatives were rejected and why

### Principle Hierarchy

When principles conflict (rare), apply this precedence:

1. **Safety-First Operations** (prevents data loss)
2. **Specification-First Development** (prevents wasted effort)
3. **Test-Driven Development** (prevents regressions)
4. **Incremental Planning** (prevents overwhelming complexity)
5. **Documentation as Code** (prevents knowledge loss)

### Living Document

This constitution is a living document that evolves with the project:

- **Lessons Learned**: Append new patterns/anti-patterns to `claude.md` bottom (never remove history)
- **Template Evolution**: Templates may be refined but must maintain constitutional alignment
- **User Preferences**: Observed preferences documented in `claude.md` User Preferences section
- **Retrospective Insights**: AI Diary and Honest Feedback sections inform constitutional improvements

**Version**: 1.0.0 | **Ratified**: 2025-11-30 | **Last Amended**: 2025-11-30
