# Project Pulse implementation plan

## Summary

Build a lightweight, polished static dashboard that helps Alex's contributors quickly see active projects, owners, status, recent activity, priority or risk, and a short contributor-friendly summary. Use the existing custom agents through GitHub Copilot CLI: the Orchestrator coordinates, the Planner defines the work, the Designer guides the interface, and the Coder implements and validates it.

## Ordered implementation steps

1. **Confirm requirements and design direction**
   - **Agents:** Orchestrator coordinates; Designer owns the dashboard experience.
   - **Files:** no files required for this decision; Designer may provide guidance in the Orchestrator's task context.
   - Specify the information hierarchy, card layout, status and priority treatments, responsive behavior, and accessible markup expectations before implementation.

2. **Create the project data**
   - **Agent:** Coder.
   - **File:** `app/project-data.json`.
   - Add a representative set of projects under a top-level `projects` array. Each object must contain `name`, `owner`, `status`, `recentActivity`, and `priority`; include contributor-friendly summary text as well.
   - Keep the sample data deterministic and use consistent status and priority values so the interface can render them clearly.

3. **Implement the dashboard interface and styling**
   - **Agents:** Designer guides visual and accessibility decisions; Coder implements the files.
   - **Files:** `app/index.html`, `app/styles.css`.
   - Use the exact document title and visible page heading `Project Pulse`. Link `styles.css`, load `project-data.json`, and render each project as a `.project-card` inside a `.dashboard` region.
   - Show every required data field, including status, recent activity, priority, and summary. Use semantic structure, accessible text and contrast, responsive layout, clear status/priority badges, rounded cards, and subtle shadows.

4. **Add the runnable preview configuration**
   - **Agent:** Coder.
   - **File:** `.vscode/launch.json`.
   - Add a strict JSON launch configuration named `Run Project Pulse Dashboard`. Serve from `${workspaceFolder}/app` with `python3 -m http.server 5500`, and configure `serverReadyAction` to open `http://localhost:%s/index.html` so the browser displays the dashboard rather than a directory listing.

5. **Integrate and validate**
   - **Agents:** Coder validates implementation; Orchestrator reviews the integrated result and reports the handoff.
   - **Files:** all four deliverable files.
   - Validate the JSON structure and required fields, the HTML title and stylesheet/data references, visible rendering of every project field, required CSS hooks and responsive/polished styles, and valid strict JSON for the launch configuration.
   - Run the launch configuration and confirm that it serves the `app` directory and opens `index.html` at the expected URL.

## Dependencies and parallel work

- Step 1 should precede implementation so Designer's direction informs the interface.
- The data schema in step 2 and the page structure in step 3 must agree. They can be developed in parallel only after the required fields and rendering contract are agreed; otherwise create the data shape first.
- The Designer can develop visual/accessibility guidance in parallel with Coder's data work because the file scopes do not overlap. Coder should use that guidance before finalizing `app/index.html` and `app/styles.css`.
- `.vscode/launch.json` can be prepared independently of the dashboard content, but final launch verification depends on the app files existing.
- Integration and launch validation in step 5 must run after all deliverables are in place.

## Edge cases and risks

- Fetching JSON requires serving the app over HTTP; opening `index.html` directly with a `file://` URL may fail. The launch task must serve from `app/`.
- Handle an empty or malformed `projects` collection and a failed data request with a clear visible message rather than a blank dashboard.
- Keep status and priority legible without relying on color alone, and ensure long project names or activity summaries wrap without breaking the card layout on narrow screens.
- Avoid presenting priority as status or vice versa; use consistent labels and sample values.
- `python3` and port `5500` must be available. If the port is occupied or the command is unavailable in the target environment, report the issue and use an agreed alternative rather than silently changing the launch behavior.

## Validation expectations

- `app/project-data.json` parses as JSON, has a top-level `projects` array, and every project includes `name`, `owner`, `status`, `recentActivity`, `priority`, and contributor-friendly summary text.
- `app/index.html` has the exact title `Project Pulse`, references `styles.css` and `project-data.json`, renders visible project cards with class `project-card`, and displays status, recentActivity, priority, and summary.
- `app/styles.css` defines `.dashboard` and `.project-card`, includes `border-radius` and `box-shadow`, and supports a responsive layout with readable spacing and accessible contrast.
- `.vscode/launch.json` is valid JSON without comments; it includes `Run Project Pulse Dashboard`, uses `${workspaceFolder}/app` as its working directory, serves on port `5500`, and opens `http://localhost:%s/index.html`.
- Run the preview and confirm the browser shows the dashboard UI rather than a directory listing.

## Open questions

- No product-specific project names, owners, statuses, activity, or priority values were provided. Use realistic, clearly illustrative sample data unless Alex supplies real examples.
- The brief requires a contributor-friendly summary but does not define its exact wording or a schema key. Use a `summary` field unless the Orchestrator confirms a different convention.
- Confirm the execution environment provides `python3`; the exercise specifies that command and port `5500`.
