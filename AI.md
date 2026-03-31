# AI Working Guide

## Project Goal
This project is a game codebase organized for reliable AI-assisted iteration.
The main goal is to let an AI expand one module at a time without destabilizing unrelated systems.

## Tech Stack
- Engine: Flexible
- Language: Flexible
- UI: Flexible
- Data: Flexible
- Save: Flexible

## Collaboration Rules
- Default to the smallest working change.
- Only modify the module requested by the task.
- Do not refactor stable shared systems unless explicitly requested.
- Preserve public interfaces when possible.
- Prefer additive changes over broad rewrites.
- After each task, document what changed and what was intentionally left untouched.

## Stable Areas
- Save compatibility layer
- Global boot flow
- Shared core utilities

## Expandable Areas
- Gameplay modules
- UI screens and widgets
- Content definitions
- Encapsulated feature logic

## File Editing Boundaries
- Safe first targets: `src/gameplay/`, `src/ui/`, `docs/systems/`
- Use caution in: `src/core/`, `src/integration/`
- Avoid unrequested edits in: save format, external API contracts, persistence migrations

## Working Style
1. Read this file first.
2. Read the target module design doc.
3. Read the target module code and local README.
4. Keep changes scoped.
5. Verify behavior.
6. Record decisions if the task changes future expectations.
