# Project Overview

## High Concept
Replace this with the game's one-paragraph pitch.

## Core Loop
1. Enter gameplay state
2. Interact with a system
3. Resolve outcomes
4. Award progress
5. Return to hub, menu, or next state

## Design Principle
Each gameplay system should be understandable and expandable in isolation.

## Module Strategy
- Core systems provide stable infrastructure.
- Gameplay systems own rules and feature behavior.
- UI reflects state and sends intents.
- Integration wires modules together without hiding ownership.
