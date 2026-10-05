# Copilot instructions for this repo

## Project shape
- This repo is a GitHub Copilot CLI orchestration exercise, not a framework app. The deliverable is a static dashboard for Mona's team called Project Pulse.
- Main UI files live under `app/`: `index.html` renders the page, `styles.css` contains the product styling, and `project-data.json` provides the dashboard data.
- The app is expected to run from the `app/` directory via `.vscode/launch.json` using `python3 -m http.server 5500` and then open `http://localhost:%s/index.html`.
- The repo's custom agent team is defined in `.github/agents/*.agent.md` (`Orchestrator`, `Planner`, `Designer`, `Coder`). Follow the orchestration pattern described in `docs/agent-team.md` and `docs/project-pulse-plan.md`.

## Required data and UI conventions
- `app/project-data.json` must contain a top-level `projects` array. Each project should include `name`, `owner`, `status`, `recentActivity`, `priority`, and a contributor-friendly `summary`.
- `app/index.html` is expected to reference `styles.css` and `project-data.json`, include a visible `Project Pulse` title, and render project cards using the class `.project-card` inside a `.dashboard` region.
- The dashboard should show project status, recent activity, priority, and summary text, not just raw JSON.
- CSS should include recognizable hooks like `.dashboard`, `.project-card`, `border-radius`, and `box-shadow`; the visual intent is a polished, responsive product dashboard rather than a bare table.

## Implementation and validation workflow
- Prefer the repo's intended workflow: use the Copilot CLI orchestrator and assign specialist work by file scope instead of one large prompt.
- Do not stage, commit, or push changes; the learner controls Git operations through Copilot CLI prompts.
- Validate static content with repo conventions: `python3 -m json.tool .vscode/launch.json` for strict JSON, and check the app via the VS Code launch config rather than by running ad hoc servers.
- When modifying the runnable app, keep the launch config deterministic: `name: "Run Project Pulse Dashboard"`, `cwd: "${workspaceFolder}/app"`, `python3 -m http.server 5500`, and the browser should open `index.html` instead of a directory listing.

## Repo-specific patterns
- The app is plain HTML/CSS/JS; there is no React/Vite/Node app runtime to infer behavior from.
- The dashboard fetches JSON from `project-data.json` using Fetch; handle missing/invalid data with a clear error message rather than a blank screen.
- The `.devcontainer/postStart.sh` script launches Copilot CLI with `copilot --allow-all --enable-all-github-mcp-tools`; keep that pattern if you update any Codespace setup.
- The validation script at `scripts/validate-exercise.sh` encodes the exact acceptance checks for this exercise. If you are unsure whether a change is valid, check that script first.

## Files to read first
- `README.md`
- `docs/project-pulse-plan.md`
- `.github/project-pulse-brief.md`
- `app/index.html`
- `app/styles.css`
- `app/project-data.json`
- `.vscode/launch.json`
