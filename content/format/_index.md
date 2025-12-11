---
title: Format Overview
description: Learn how the OpenRoadBook adventure format structures entries, symbols, and tasks while leaving room for FIA and competitive extensions.
hero:
  lead: "The OpenRoadBook standard establishes a file layout, core fields, and symbol registry to be used for roadbooks. The current release targets adventure and non-competitive events; profiles provide a path to other disciplines without changing the base structure."
  ctas:
    - text: "Usage guide"
      url: "/format/"
    - text: "Symbol registry"
      url: "#symbol-registry"
      style: "btn btn--secondary"
  card:
    title: "Key ingredients"
    list:
      - "**Today:** Distance, CAP, tulip, notes, and hazard fields for adventure stages."
      - "**Today:** CLI tooling plus templates to validate, print, and export to GPX."
      - "**Next:** FIA-ready profiles with penalties, scrutineering, and timing metadata."
---

## Quick start — the smallest valid ORB {#quick-start}

An OpenRoadBook (ORB) document is a YAML file with a `meta` block and one or more `stages` (or a top-level `entries`) list. The minimal, valid structure looks like:

```yaml
meta:
  format: OpenRoadBook
  version: 1.0

stages:
  - id: stage_1
    title: "Simple test"
    entries:
      - km: 0.0
        tulip: start
        notes: "Start here"
```

Save as `my-first.orb.yaml` and validate with the published JSON Schema at `/schemas/orb.schema.json`.

## Event metadata

Add human-friendly event metadata to `meta` so tools can surface and filter content:

```yaml
meta:
  format: OpenRoadBook
  version: 1.0
  id: orb-demo-001
  title: "Montseny Demo"
  date: 2025-11-01
  units: km
  profile: adventure
```

## Common entry fields

Build entries incrementally using the following fields:

- `km` — cumulative distance (float, in `meta.units`).
- `tulip` — symbolic navigation diagram ID.
- `cap` — compass heading (0–359).
- `notes` — human instructions.
- `symbols` — extra registry IDs such as hazards or services.
- `waypoint` — optional `{ lat, lon }` for mapping.

Example:

```yaml
entries:
  - km: 12.35
    tulip: turn_left
    cap: 270
    notes: "Gravel, caution rocks"
    symbols: [danger2, jump]
    waypoint: { lat: 41.12345, lon: 2.12345 }
```

## Branches & alternatives

Model optional routes using `alternatives` (inline) or `branches` (named blocks).

Inline skip-to alternative:

```yaml
- id: m10
  km: 88.8
  alternatives:
    - skip_to: m14
      tulip: { symbol: exit-left }
```

Named branch:

```yaml
branches:
  - id: scenic_route
    continue_to: m11
    instructions:
      - km: 90.1
        notes: "Twisty road"
      - km: 120.0
        notes: "Beautiful views"
```

## Time windows

Use `time` to provide arrival hints or constraints:

```yaml
time:
  earliest: "08:20"
  latest: "09:20"
```

Validators can treat `time` as guidance or strict constraints depending on the profile.

## Locations & coordinates

Locations can include names and multiple coordinate formats:

```yaml
location:
  name: "Coll de Sant Marçal"
  lat: 41.345
  lon: 2.345
  pluscode: "8FW4V+2V"
  what3words: "index.card.route"
```

## Extensions & vendor namespaces

Use namespaced blocks for renderer or analytics extensions. Validators should ignore unknown extension blocks unless a profile requires them.

```yaml
meta:
  extensions:
    corbs.render:
      preview: true
    orb.analytics:
      track: true
```

## Worked example (demo)

The official demo ORB (`/demos/demo.orb.yaml`) is the canonical worked example. Steps:

1. Inspect `meta` and confirm `profile: adventure` and `units: km`.
2. Find the stage trunk and identify `branches`/`alternatives`.
3. Validate with `ajv`:

```bash
npx ajv validate -s https://openroadbook.com/schemas/orb.schema.json -d demos/demo.orb.yaml --spec=draft2020
```

4. Make a small edit, revalidate, and render.

## References

- Schema: `/schemas/orb.schema.json`
- Demo ORB: `/demos/demo.orb.yaml`
- Specification: `/spec/`

Last updated: 2025-12-10

## Schema examples — concrete snippets for each definition

Below are focused examples that map directly to the JSON Schema definitions. Use them as copy-paste starting points when authoring ORB files.

### `meta` (document-level metadata)

```yaml
meta:
  format: OpenRoadBook
  version: 1.0
  id: montseny-2025
  title: "Montseny i Guilleries — Demo"
  date: 2025-11-01
  profile: adventure
  units: km
  authors:
    - name: "OpenRoadBook Team"
      email: team@openroadbook.org
  labels: [demo, montseny, circular]
  extensions:
    corbs.render:
      preview: true
```

Fields covered: `format`, `version`, `id`, `title`, `date`, `profile`, `units`, `authors`, `labels`, `extensions`.

### `symbol` registry entry

Registry entries describe a symbol and point to artwork.

```yaml
symbols:
  - id: danger2
    name: "Danger (2 exclamations)"
    category: hazard
    svg: danger2.svg
    description: "Serious hazard — reduce speed"
```

Fields covered: `id`, `name`, `category`, `svg`, `description`.

### `stages` and `entries` (trunk): basic entry

```yaml
stages:
  - id: ss1
    title: "Stage 1"
    entries:
      - id: e1
        km: 0.00
        tulip: start
        notes: "Start line"
      - id: e2
        km: 12.35
        tulip: turn_left
        cap: 270
        notes: "Gravel; caution rocks"
        symbols: [danger2, jump]
        speed_limit: 50
        waypoint:
          lat: 41.12345
          lon: 2.12345
```

Fields covered: `id` (entry), `km`, `tulip` (string), `cap`, `notes`, `symbols` (array), `speed_limit`, `waypoint` (object lat/lon).

### `tulip` as an object (advanced tulip references)

Some schema variants allow a structured tulip object with `symbol` and `mirror`/`variant` hints.

```yaml
entries:
  - id: e10
    km: 42.0
    tulip:
      symbol: junction.turn_left
      variant: sharp
    notes: "Sharp left at the junction"
```

Fields covered: `tulip` as object with `symbol` and optional properties.

### `branches` (named alternative routes)

```yaml
branches:
  - id: scenic_route
    note: "Scenic unpaved alternative"
    impact:
      distance: 248
      time: PT4H27M
      pros: [scenic]
      cons: [time, distance]
    instructions:
      - km: 100.0
        notes: "Dirt track"
      - km: 348.0
        notes: "Rejoin"
```

Fields covered: `branches` id, `note`, `impact` (distance/time/pros/cons), `instructions` array.

### `alternatives` (inline alternative references)

```yaml
entries:
  - id: m10
    km: 88.8
    alternatives:
      - skip_to: m14
        tulip: { symbol: exit-left }
      - branch: scenic_route
        note: "If early, take the scenic route"
```

Fields covered: `alternatives` with `skip_to` or `branch` references and `note`.

### `time` (earliest/latest or duration)

```yaml
entries:
  - id: t1
    km: 50.0
    time:
      earliest: "08:20"
      latest: "09:20"
```

Fields covered: `time.earliest`, `time.latest` (also support ISO durations in some profiles).

### `location` (multiple coordinate systems)

```yaml
entries:
  - id: loc1
    km: 12.1
    location:
      name: "Coll de Sant Marçal"
      lat: 41.345
      lon: 2.345
      pluscode: "8FW4V+2V"
      what3words: "index.card.route"
```

Fields covered: `location.name`, `lat`, `lon`, `pluscode`, `what3words`.

### `road` transitions and surface

```yaml
entries:
  - id: r1
    km: 23.5
    notes: "Transition to gravel"
    road:
      current: tarmac
      next: gravel
```

Fields covered: `road.current`, `road.next` and surface hints.

### `tags` / `labels` / `flags`

```yaml
entries:
  - id: e-tag
    km: 5.0
    notes: "Photo stop"
    tags: [photo, scenic]
```

Fields covered: `tags`/`labels` arrays to annotate entries.

### `authors` block example (document-level)

```yaml
meta:
  authors:
    - name: "Jane Rider"
      email: jane@example.org
      organisation: "Adventure Club"
```

### `extensions` examples (vendor namespaces)

```yaml
meta:
  extensions:
    corbs.render:
      preview: true
      layout: "compact"
    orb.analytics:
      telemetry: true
```

Extensions are free-form and namespaced; validators typically ignore unknown keys.

### `speed_limit` and safety fields

```yaml
entries:
  - id: sl1
    km: 77.7
    notes: "Entering town — reduce speed"
    speed_limit: 50
    symbols: [speed_limit]
```

### `meta.units` and unit conversions

Always set `meta.units` when distances are not kilometres. Example using miles:

```yaml
meta:
  units: miles
```

### Putting it all together — a full minimal stage

```yaml
meta:
  format: OpenRoadBook
  version: 1.0
  title: "Demo"
  units: km

stages:
  - id: demo
    title: "Demo Stage"
    entries:
      - id: start
        km: 0.0
        tulip: start
        notes: "Stage start"
      - id: e2
        km: 8.2
        tulip: turn_right
        notes: "Turn right after bridge"
        waypoint: { lat: 41.2, lon: 2.2 }
      - id: e3
        km: 12.0
        tulip:
          symbol: junction.turn_left
          variant: slight
        notes: "Slight left"
        alternatives:
          - branch: scenic_route
            note: "Detour for views"

branches:
  - id: scenic_route
    instructions:
      - km: 14.0
        notes: "Scenic track"

symbols:
  - id: danger2
    name: "Danger"
    category: hazard
    svg: danger2.svg

extensions:
  corbs.render:
    preview: true
```

If you want, I can now scan `schemas/orb.schema.json` and generate a one-to-one example for every named definition (definitions/subschemas). Tell me if you prefer a single combined file with all examples, or split examples into separate pages per schema section.
        Last updated: 2025-12-10
