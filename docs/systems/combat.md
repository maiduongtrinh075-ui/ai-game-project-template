# Combat System

## Purpose
Own the battle loop and outcome resolution for combat encounters.

## Current Scope
- turn order
- action selection
- damage resolution
- victory or defeat

## Planned Expansion
- skills
- buffs and debuffs
- enemy logic
- combat rewards

## Inputs
- actor stats
- action definitions
- battle configuration

## Outputs
- health changes
- combat events
- end-of-battle result

## Do Not Break
- combat start entry point
- combat end event contract
- stat input structure without a migration plan
