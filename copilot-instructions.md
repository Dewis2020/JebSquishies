# copilot-instructions.md

## Purpose
This file defines conventions, automation hints, and actionable rules for humans and Copilot-style assistants contributing to this **Blazor WebAssembly .NET 10** solution. It is written for a TDD-first workflow, reusable UI components, MudBlazor + Material Design, SOLID, and Clean Code practices.

---

## Scope
- Applies to all code, tests, UI components, ADRs, and CI changes in this repository.
- Targets `src/`, `libs/ui/`, and `tests/` projects.
- Intended to be copy-paste ready and machine-friendly for automation.

---

## Core Principles
- **TDD First**: Red → Green → Refactor for every behavior.
- **Single Responsibility**: One reason to change per class or component.
- **SOLID**: Apply across layers.
- **Composition Root**: Only `Program.cs` configures DI and third-party services.
- **Wrap Third-Party UI**: `libs/ui` is the only place to reference MudBlazor directly.

---

## Repository Layout
**Top-level folders**
- `src/` — application projects
- `libs/ui/` — app UI library wrapping MudBlazor primitives
- `tests/unit/` — unit tests for domain and view models
- `tests/components/` — bUnit component tests
- `tests/integration/` — hosted server integration tests
- `docs/` — ADRs and design notes
- `scripts/` — templates and helper scripts

**Project boundaries**
- Feature projects reference `libs/ui` and `src/MyApp.Shared` only as needed.
- `libs/ui` must not contain business logic.

---

## Naming Conventions
- **Components**: `PascalCase.razor` and optional `PascalCase.razor.cs`.
- **Tests**: `ClassName_MethodUnderTest_State_Expected.cs`.
- **Interfaces**: `IThingService`.
- **Implementations**: `ThingService`.
- **Files**: One top-level type per file unless tightly coupled.

---

## TDD Workflow
1. **Write a failing test** (Red).
2. **Implement the minimal code** to pass the test (Green).
3. **Refactor** for clarity and remove duplication (Refactor).
- Tests must be **fast**, **deterministic**, and **isolated**.
- Use **Arrange / Act / Assert** structure.
- Prefer small, focused PRs that add one behavior at a time.

---

## Test Strategy
- **Unit tests**: domain logic and view models in `tests/unit`.
- **Component tests**: bUnit tests in `tests/components`.
- **Integration tests**: hosted server flows in `tests/integration`.
- **Contract tests**: for external API expectations when applicable.

**Test doubles**
- Prefer lightweight fakes and in-memory stores.
- Use DI to swap implementations in tests.
- Avoid heavy, brittle mocking of UI frameworks.

---

## Component Design Rules
- **Single responsibility** per component.
- Prefer **stateless** components; move state to view models or services.
- Use **EventCallback** for interactions.
- Use **RenderFragment** for templating and customization.
- Keep parameter lists short and intention-revealing.
- Provide XML comments for public component APIs.

---

## libs UI Guidelines
- `libs/ui` wraps MudBlazor primitives into app-specific components.
- Each wrapper must:
  - Enforce consistent props and behavior.
  - Include bUnit tests.
  - Include a sample page demonstrating usage.
- Do not leak MudBlazor types outside `libs/ui` unless explicitly intended.

---

## Theming and Tokens
- Centralize theme tokens in a single provider in `libs/ui`.
- Follow Material Design spacing and typography scales.
- Avoid inline styles; prefer theme variables and CSS classes.
- Provide a single place to change palette and typography.

---

## Accessibility
- Ensure keyboard navigation and ARIA attributes are present.
- Validate contrast ratios and semantic markup.
- Test components with keyboard-only navigation and screen reader tools.

---

## Performance
- Use AOT and trimming strategies for WebAssembly bundle size.
- Avoid unnecessary render cycles; prefer `ShouldRender` and careful state updates.
- Keep components lightweight and avoid heavy synchronous work on render.

---

## Clean Code and SOLID Checklist
- **Meaningful names** and intention-revealing identifiers.
- Methods short and at one level of abstraction.
- Favor composition over inheritance for UI behaviors.
- Use immutable value objects for domain primitives where appropriate.
- Keep side effects explicit and localized.