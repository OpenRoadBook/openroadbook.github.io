---
title: "Format guide — examples"
description: "User-focused guide with examples showing common patterns: skip_to, branches, and time constraints."
---

# Quick guide: Alternatives & Time constraints

This page is an example-driven walk-through showing how to use `alternatives` and `time` in OpenRoadBook documents. The formal specification is published on the site at `/spec/` and in the repository under `spec/format.md`.

## Skip-to example (simple shortcut)

Use a `skip_to` when the action is to jump forward to another instruction:

```yaml
- id: milestone_8
  distance: 88.8
  time:
    latest: "09:20"
  location:
    name: Milestone 8
  alternatives:
    - skip_to: milestone_14
      next_road: C-25
      tulip: { symbol: exit-left }
```

This means "if you choose this alternative, continue from the instruction with id `milestone_14`".

NOTE: The consumer should not recompute stage totals; `skip_to` is a navigation hint.

## Branch reference example (use a branch object)

If an alternative needs a series of instructions, define a stage-level branch and reference it from the instruction:

```yaml
- id: milestone_10
  distance: 88.8
  time:
    earliest: "08:20"
    latest: "09:20"
  alternatives:
    - branch: scenic_route
      note: If you're early, take this detour

# later in the same stage
branches:
  - id: scenic_route
    note: Scenic route off milestone 10
    continue_to: milestone_11
    instructions:
      - distance: 90.1
        location: { name: "Twisty road" }
      - distance: 120.0
        location: { name: "Beautiful views" }

An optional `impact` object can provide summary information about a branch to help user interfaces display alternatives:

```yaml
branches:
  - id: B1
    note: "Scenic unpaved shortcut"
    impact:
      time: PT4H27M
      distance: 248
      pros:
        - scenic
      cons:
        - time
        - distance
    instructions:
      - distance: 100.0
        location: { name: "Dirt track" }
      - distance: 348.0
        location: { name: "Rejoin point" }
```
```

`branch` entries can supply full instruction lists (and optionally `continue_to` to signal where they rejoin the trunk).

## Time constraints (practical)

Two common patterns:

- `time` as shorthand latest:

```yaml
time:
  latest: "19:35"
```

- `time` as a window:

```yaml
time:
  earliest: PT1H30M
  latest: "19:35"
```

Treat these as hints: an organiser may decide they are soft (help renderers show expected arrival) or hard (used to apply penalties).

## Where to start

- Use the `skip_to` pattern for simple skip-ahead options.
- Use `branch` definitions for multi-step alternatives.
- Use `time` windows when you want flexible bounds; prefer `earliest`/`latest` when both matter.

For the formal definition, see the spec: [/spec/](/spec/).
