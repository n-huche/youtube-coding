# Action Engine — YouTube Coding Log

Repository: [`n-huche/action-engine`](https://github.com/n-huche/action-engine) · Channel: [`@n-huche`](https://www.youtube.com/@n-huche)

## #1 — Refactoring Task Hierarchy into a Single Class with Pipeline API

Video: [https://youtu.be/wxPHdPOo6Wo](https://youtu.be/wxPHdPOo6Wo)

Refactored the initial domain model from five separate task subclasses (`Single`, `Recurring`, `Iterative`, `LongTerm`, `Maintenance`) and marker interfaces (`Linkable`, `Repeatable`) into a single `Task` class configured through a fluent pipeline API.

- Replaced constructor-heavy subclass initialization with pipeline methods (`type`, `goal`, `action`, `doOn`, `doAt`, `doUntil`, `link`, `cadence`) and `TaskType` / `CadenceType` enums.
- Added validation on `.add()` requiring a task goal (`GoalNotDefinedException`).
- Wrote unit tests with JUnit 5 (`TaskTest`) covering task creation, property assignment, and missing-goal validation.

## #2 — Restructuring Architecture and Code Design Decision Records (ADRs & DRs)

Reorganized and rewrote the project's `docs/` directory to separate final system documentation (`docs/architecture.md` and `docs/design.md`, to be written once the system is complete) from decision records (`docs/decisions/`).

- Split decision records into two categories:
  - **Architecture Decision Records (`docs/decisions/architecture/`):**
    - `adr-001-ai-as-ui.md` — AI as the primary user interface, backed by an MCP-friendly API and generated Markdown context.
    - `adr-002-sql-db-ssot.md` — SQL database as the single source of truth, with Markdown files generated as a read-only reflection of database state.
  - **Design Records (`docs/decisions/design/`):**
    - `dr-001-subclass-to-each-task-type.md` — Initial class hierarchy design (abstract superclass + one subclass per task type + interfaces).
    - `dr-002-single-class-to-all-task-types.md` — Class redesign superseding DR-001: consolidating all task types into a single `Task` class initialized via pipeline methods.
