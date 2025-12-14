<!--
Project: Tester-Tester
Purpose: Guidance for AI coding agents to be productive in this repository.
-->
# Copilot instructions for Tester-Tester

Big picture:
- This is a small web app prototype to calculate product cost based on recipes.
- The cost model is split into Material, Labor, and Overhead costs (see README.md).

Repo layout and where to work:
- Static frontend lives in the `Main/` folder. Edit `Main/Main.html` and `Main/Main.css` for UI.
- Add new JS or data under `Main/` (e.g., `Main/app.js`, `Main/data/materials.json`).

Key constraints and patterns (must follow):
- Material costs frequently change and must be easily editable by an administrator; do not hardcode costs into UI logic.
- Keep cost data decoupled from code: use JSON files, a simple API, or a configuration file under `Main/data/`.
- Respect the 3 cost categories: Material, Labor, Overhead; keep calculations explicit and testable.

Developer workflows and commands:
- This is a static site. Quick local run: `python -m http.server 8000` from the repository root and open `http://localhost:8000/Main/Main.html`.
- For development in VS Code, use Live Server or a static file server extension if available.

Integration points & data formats:
- Expect a JSON file mapping materials to unit cost. Example structure to add under `Main/data/materials.json`:

```
{
  "sugar": {"unit":"kg", "cost":1.25},
  "flour": {"unit":"kg", "cost":0.8}
}
```

- The UI should accept a recipe (ingredient + quantity pairs) and compute the total by summing MATERIAL_COST + LABOR_COST + OVERHEAD.

Project-specific examples and conventions:
- Place all static assets in `Main/`. Suggested new files: `Main/app.js`, `Main/data/materials.json`, `Main/admin.html` (for editing materials).
- Don't couple material identifiers with cost values in `app.js`. Instead, pull the cost mapping from `Main/data/materials.json` and fallback to a sensible default if a material is missing.

What reviewers expect from PRs:
- Small, focused PRs; include static file updates for updates to markup/styles and a sample `materials.json` for any pricing-related change.
- If introducing interactive JS, include a minimal demonstration page (Main/Main.html) and a README note describing how to test it locally.

Files to check first when reviewing a change:
- README.md — project assumptions and task goals.
- Main/Main.html — frontend proof-of-concept.
- Any `Main/data/*.json` files — material costs and example payloads.

When in doubt:
- Prefer storing configuration in JSON under `Main/data/` and wiring that into `app.js` instead of embedding values or business logic in markup.

If you need more context or there are conflicting choices, ask maintainers by opening an issue with a small reproduction and suggested code change.
