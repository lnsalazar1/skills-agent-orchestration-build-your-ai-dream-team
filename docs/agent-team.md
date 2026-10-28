# Agent team

For Mona's Project Pulse dashboard, I am using a four-agent custom team defined under `.github/agents/` and orchestrated through GitHub Copilot CLI in a Codespace.

- Orchestrator — Model: Claude Opus 5.5 (copilot). Responsibility: breaks the project into phases, delegates work to the specialist agents, coordinates file ownership, and verifies that the final dashboard hangs together. Definition: `.github/agents/orchestrator.agent.md`
- Planner — Model: Claude Opus 5.5 (copilot). Responsibility: researches the repository, maps dependencies, identifies risks and edge cases, and produces an implementation plan with clear step ordering and validation expectations. Definition: `.github/agents/planner.agent.md`
- Designer — Model: Gemini 3.7 Flash (copilot). Responsibility: focuses on UX, accessibility, layout hierarchy, responsive design, and the visual polish of the Project Pulse dashboard. Definition: `.github/agents/designer.agent.md`
- Coder — Model: GPT-5.5 (copilot). Responsibility: implements the static app, dashboard data wiring, and any necessary support files such as the run configuration for the dashboard preview. Definition: `.github/agents/coder.agent.md`

This setup mirrors the exercise flow: the Orchestrator coordinates the work, the Planner shapes the plan, the Designer guides the experience, and the Coder builds the final app while the learner uses GitHub Copilot CLI in the Codespace to manage orchestration instead of one large prompt.
