# AI Game Project Template

This is a stack-agnostic template for building games with AI in a modular, iterative way.

Use this template when you want to:
- grow one gameplay system at a time
- keep AI edits contained
- document module boundaries
- make handoffs between different AI sessions more stable

## Start Here
- Read `AI.md`
- Read `.ai/context/project-overview.md`
- Read `.ai/context/current-status.md`
- Open the relevant file under `docs/systems/`

## Suggested Workflow
1. Pick one module to expand.
2. Create a task in `tasks/in-progress/`.
3. Give the AI the task plus the module doc.
4. Limit edits to the module and its immediate UI or data dependencies.
5. Record decisions if the scope or rules changed.
