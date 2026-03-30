---
name: godot-mcp-game-development
description: Use when building or modifying a Godot game, especially when MCP tooling is available (scene/node inspection, runtime logs, automated playthrough checks). Adapts Superpowers workflow for gameplay loops, scenes, signals, and performance-safe iteration.
---

# Godot MCP Game Development

## Purpose

Adapt the default Superpowers workflow to game development in Godot, with MCP-assisted verification.

Announce at start: "I'm using the godot-mcp-game-development skill to run a Godot-adapted workflow."

## Core Loop (Game-First)

Before writing code, force clarity on these 5 items:

1. **Core loop** - What does player do every 5-15 seconds?
2. **Win/lose state** - How does a run/session end?
3. **One MVP slice** - Smallest playable vertical slice.
4. **Input map** - Keyboard/controller actions and expected behavior.
5. **Acceptance checks** - What must be observable to call it done?

If any is missing, ask focused questions before implementation.

## Planning Rules

When using `writing-plans`, translate tasks to Godot units:

- Scene task (`.tscn`)
- Script task (`.gd` / C#)
- Autoload/singleton task
- UI task (`Control` tree)
- Data/save task
- Verification task

Each task should remain 2-10 minutes and end with a concrete verification step.

## Godot Architecture Defaults

- One scene = one clear responsibility.
- Prefer composition + signals over deep inheritance trees.
- Keep gameplay state explicit (state machine or clearly separated booleans/enums).
- Keep `_process` lightweight; use physics ticks for movement/collision logic where appropriate.
- Avoid global mutable state unless it's an intentional autoload.

## MCP-Driven Verification

Use MCP capabilities (if available) to replace hand-wavy "looks fine":

1. Launch project and target scene.
2. Read runtime logs and watch for errors/warnings.
3. Validate scene tree + required nodes exist.
4. Simulate minimal input path for the feature.
5. Capture evidence (log snippet/screenshot/video/text trace).

No "done" without evidence.

## Definition of Done (Godot)

A gameplay task is done only if all are true:

- Feature works in a real playable run.
- No new runtime errors in logs.
- Critical signal connections are verified.
- Scene and script names are consistent and discoverable.
- Regression checks pass for previous core loop behavior.

## PR/Review Checklist

- Is this change actually playable?
- Are scene references stable (no broken node paths)?
- Are physics/input updates in the correct tick path?
- Any accidental frame-time spikes or tight loops?
- Could this be split into smaller scene/script responsibilities?

## Anti-Patterns to Reject

- Implementing broad systems before a playable MVP slice.
- "Trust me" completion with no runtime verification.
- Massive script files handling unrelated responsibilities.
- Adding generic abstractions with no current gameplay need.
- Shipping with runtime warnings/errors because "it still runs".

## Recommended Superpowers Pairing

- `brainstorming` -> define gameplay slice
- `writing-plans` -> produce stepwise implementation plan
- `subagent-driven-development` or `executing-plans` -> implement by task
- `systematic-debugging` -> when behavior diverges from expected gameplay
- `verification-before-completion` -> final runtime proof
