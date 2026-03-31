# CLAUDE Project Guide

## Project Goal
This repository is organized for modular AI-assisted game development.
Claude should expand one system at a time while keeping unrelated systems stable.

## First Files To Read
1. `CLAUDE.md`
2. `docs/systems/<module>.md`
3. `src/<module>/README.md` or nearest module README
4. `tasks/in-progress/<task>.md`

## Collaboration Rules
- Prefer the smallest useful change.
- Default to editing only the requested module.
- Preserve public interfaces unless the task explicitly allows changes.
- Do not change save contracts without documenting the change first.
- Update docs when a feature changes long-term behavior.

## Stable Areas
- save compatibility
- boot flow
- shared core utilities

## Expandable Areas
- gameplay systems
- module-local UI
- content and definitions

## Default Workflow
1. Read the relevant system docs.
2. Identify boundaries and do-not-break contracts.
3. Implement the smallest working version.
4. Verify the target flow still works.
5. Record durable decisions if needed.
