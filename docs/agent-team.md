# Agent team

We will use a coordinated custom agent team in GitHub Copilot CLI inside a Codespace to build Mona's Project Pulse dashboard. The team is defined under `.github/agents/` and each agent has a clear role in the workflow.

## Orchestrator
- Model: Claude Opus 4.7
- Definition: `.github/agents/orchestrator.agent.md`
- Responsibility: break the Project Pulse work into phases, delegate tasks to specialists, manage dependencies, and validate that the final dashboard fits together.

## Planner
- Model: Claude Opus 4.7
- Definition: `.github/agents/planner.agent.md`
- Responsibility: research the repo, identify requirements and risks, and create a practical implementation plan for the dashboard before coding begins.

## Designer
- Model: Gemini 3.1 Pro
- Definition: `.github/agents/designer.agent.md`
- Responsibility: shape the Project Pulse user experience, visual hierarchy, accessibility, and responsive dashboard styling so the result feels polished and product-ready.

## Coder
- Model: GPT-5.5
- Definition: `.github/agents/coder.agent.md`
- Responsibility: implement the dashboard files, support the runnable app, and validate that the dashboard works as expected with deterministic behavior.

## How the team works together
The Orchestrator coordinates the Planner, Designer, and Coder agents. The Planner creates the implementation strategy, the Designer defines the experience and styling direction, and the Coder builds the actual HTML/CSS/JS for the Project Pulse dashboard. The group works together in GitHub Copilot CLI to keep delivery focused, parallel where possible, and validated before handoff.
