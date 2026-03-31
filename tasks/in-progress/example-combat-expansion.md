# Module Expansion Task

## Module
combat

## Goal
Add three player skills and simple enemy action selection without changing the save format.

## Must Keep Stable
- combat entry and exit flow
- existing stat model names
- reward handoff event

## Allowed Scope
- `src/gameplay/combat/`
- `src/ui/battle/`
- related docs

## Acceptance Criteria
- player can pick one of three skills
- enemy acts automatically on its turn
- battle can still end normally

## Verification Notes
- test one win case
- test one loss case
- verify UI still displays action choices
