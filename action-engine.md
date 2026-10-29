# Action Engine — YouTube Coding Log

Repository: [`n-huche/action-engine`](https://github.com/n-huche/action-engine) · Channel: [`@n-huche`](https://www.youtube.com/@n-huche)

## #1 — Task Class Redesign & First JUnit Tests

Video: [https://youtu.be/wxPHdPOo6Wo](https://youtu.be/wxPHdPOo6Wo)

- Refactored the initial domain model from five separate task subclasses (`Single`, `Recurring`, `Iterative`, `LongTerm`, `Maintenance`) and marker interfaces (`Linkable`, `Repeatable`) into a single `Task` class configured through a fluent pipeline API.
- Replaced constructor-heavy subclass initialization with pipeline methods (`type`, `goal`, `action`, `doOn`, `doAt`, `doUntil`, `link`, `cadence`) and `TaskType` / `CadenceType` enums.
- Added validation on `.add()` requiring a task goal (`GoalNotDefinedException`).
- Wrote unit tests with JUnit 5 (`TaskTest`) covering task creation, property assignment, and missing-goal validation.

## #2 — Architecture & Code Design Decision Records

Video: [https://youtu.be/Ve9m5uDGzx8](https://youtu.be/Ve9m5uDGzx8)

- Reorganized and rewrote the project's `docs/` directory to separate final system documentation (`docs/architecture.md` and `docs/design.md`, to be written once the system is complete) from decision records (`docs/decisions/`).
- Split decision records into Architecture Decision Records (`docs/decisions/architecture/`) and Design Records (`docs/decisions/design/`).
- Wrote ADR-001 (`adr-001-ai-as-ui.md`): AI as the primary user interface, backed by an MCP-friendly API and generated Markdown context.
- Wrote ADR-002 (`adr-002-sql-db-ssot.md`): SQL database as the single source of truth, with Markdown files generated as a read-only reflection of database state.
- Wrote DR-001 (`dr-001-subclass-to-each-task-type.md`): the initial class hierarchy design (abstract superclass + one subclass per task type + interfaces).
- Wrote DR-002 (`dr-002-single-class-to-all-task-types.md`): the class redesign superseding DR-001, consolidating all task types into a single `Task` class initialized via pipeline methods.

## #3 — Strong Typing, Custom Exceptions & Static Factory

Video: [https://youtu.be/iBBEVp0sqfc](https://youtu.be/iBBEVp0sqfc)

- Replaced String with a TaskType enum as the argument of Task.type(), and added a CadenceType enum.
- Added validation on Task.add() with a new custom unchecked exception (TaskTypeNotDefinedException) when a task is added without a defined type, alongside the existing GoalNotDefinedException.
- Wrote Code Design Decision Record DR-003: strong typing in method arguments, so invalid formats fail at compile time instead of throwing at runtime.
- Switched doOn and doAt to LocalDate and LocalTime arguments, keeping the fluent builder-style method chaining.
- Introduced a static factory method (Task.create()) as the way to create new tasks, and updated the JUnit 5 tests to the new API.
