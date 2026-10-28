# Project Pulse Implementation Plan

## Summary

Build a lightweight static dashboard that helps Mona's contributors scan active projects, owners, status, recent activity, and priority or risk. Use `app/project-data.json` as the data source, render visible project cards from `app/index.html`, and provide a VS Code launch configuration that serves the `app/` directory and opens `index.html`.

Keep implementation within the four assigned files. Use accessible semantic HTML, responsive styling, and clear loading or error messaging if project data cannot be loaded.

## Ordered Steps and File Ownership

1. **Designer: establish the visual and accessibility contract.** Define the dashboard hierarchy, card layout, status and priority treatment, responsive behavior, accessible contrast, and focus states. Own `app/styles.css`; include `.dashboard` and `.project-card` selectors, `border-radius`, and `box-shadow`. Share the expected HTML hooks with Coder before integration.

2. **Parallel implementation after the contract is agreed.**
   - **Designer:** implement the agreed styles in `app/styles.css`.
   - **Coder:** create `app/project-data.json` with a top-level `projects` array. Every project must include `name`, `owner`, `status`, `recentActivity`, and `priority`.
   - **Coder:** create `.vscode/launch.json` as strict JSON with no comments. Add the configuration named **Run Project Pulse Dashboard**, run `python3 -m http.server 5500` with `cwd` set to `${workspaceFolder}/app`, and configure `serverReadyAction` to open `http://localhost:%s/index.html`.

3. **Coder: implement and integrate `app/index.html`.** Use the exact title "Project Pulse"; reference `styles.css` and `project-data.json`; render a `.project-card` for each project and display its name, owner, status, recent activity, and priority. Use the Designer's agreed selectors and accessible structure. Include understandable loading, empty-data, and data-load failure states.

4. **Orchestrator: validate the integrated dashboard and report remaining risks.** Keep changes limited to the four assigned files; do not stage, commit, or push as part of implementation.

## Dependencies and Work Ordering

The Designer and Coder must first agree on the HTML/CSS hooks and data contract. After that, the stylesheet, JSON data, and launch configuration can be implemented in parallel because each has a distinct file owner and the brief fixes their core requirements. HTML integration depends on the agreed hooks and data schema, so it follows that parallel work. Integrated validation comes last.

## Responsibilities

- **Designer:** own visual design and `app/styles.css`; guide layout, information hierarchy, accessibility, responsive behavior, and visual clarity; report design decisions and validation recommendations.
- **Coder:** own `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`; implement data-driven card rendering and launch support; validate JSON and confirm the runnable configuration.
- **Orchestrator:** delegate by file scope, keep overlapping work out of parallel phases, integrate handoffs, and verify the completed dashboard.

## Edge Cases and Assumptions

- Handle an empty `projects` array, failed JSON loading, and long project names or activity text without breaking the layout.
- Keep asset and data references relative so the app works when served from `app/`.
- The brief asks for a short contributor-friendly summary but does not define a `summary` data field. Treat `recentActivity` as the concise contributor-facing context unless Mona specifies an additional field.
- No real project records are supplied; use representative, clearly fictional sample entries.
- Port `5500` is specified by the exercise. If it is already occupied during the smoke test, resolve the conflict while keeping the configured server command and URL consistent.

## Validation Expectations

- Confirm all four assigned files exist.
- Run `python3 -m json.tool app/project-data.json` and `python3 -m json.tool .vscode/launch.json`; both must parse successfully.
- Check `app/index.html` for the exact title, stylesheet and data references, card markup, and rendered `status`, `recentActivity`, and `priority` fields.
- Check `app/styles.css` for `.dashboard`, `.project-card`, `border-radius`, and `box-shadow`; review responsive layout, readability, and accessibility.
- In VS Code, launch **Run Project Pulse Dashboard**. Confirm the browser opens `http://localhost:5500/index.html` and displays the dashboard rather than a directory listing. Check that project cards and their fields are visible, then stop the server.
- Treat the Step 3 workflow checks as automated phrase and JSON checks, not as proof that the app runs. The repository's `scripts/validate-exercise.sh` also checks starter-template conditions, including learner answer files not being tracked, so it is not the integrated dashboard smoke test.

## Open Questions

- Should project summaries be a separate data field, or is `recentActivity` sufficient?
- Which representative project names and sample activity should be used?
