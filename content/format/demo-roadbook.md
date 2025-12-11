---
title: "Demo Roadbook"
description: "Work through the official OpenRoadBook demo file, download the sources, and validate them against the published schema."
slug: "demo-roadbook"
---
hero:
  lead: "A complete example roadbook that demonstrates meta blocks, stages, entries, and extensions. Use it as a template or test fixture: validate it against the published JSON Schema and adapt the structure for your event."
  ctas:
    - text: "Download demo.orb.yaml"
      url: "/demos/demo.orb.yaml"
      style: "btn"
    - text: "View JSON Schema"
      url: "/schemas/orb.schema.json"
      style: "btn btn--secondary"
  card:
    title: "Bundle contents"
    list:
      - "Adventure profile (`profile: adventure`)."
      - "One main stage with optional branches."
      - "Extension blocks for analytics and rendering."
      - "Published schema reference (`$id: https://openroadbook.com/schemas/orb.schema.json`)."
## Metadata

The `meta` block declares format, version, units, and event-level details. Keep these fields accurate: tools use them for validation, unit interpretation, and rendering.

- `meta.id` — **orb-demo**, unique identifier for the document.
- `meta.title` — Human readable “Montseny i Guilleries”.
- `meta.units` — Distance in kilometres, headings in degrees, speed in km/h. Explicit units avoid ambiguity when tools interpret the data.
- `meta.extensions` — Sample blocks (`corbs.render`, `orb.analytics`) illustrate how partner tooling embeds previews and computed metrics.

### Meta snapshot

- **Profile:** adventure
- **Labels:** demo, asphalt, montseny, circular
- **Created:** 2025-11-01
- **Authors:** OpenRoadBook Team <team@openroadbook.org>

## Stage structure

A stage contains an ordered trunk of instructions (entries). Each entry references a symbol ID, a cumulative distance, and optional fields such as heading, waypoint coordinates, or tags. Branches or alternatives reuse the same entry shape and can be named and rejoined.

### Trunk instructions

- Cumulative `distance` values with ISO-8601 `time_stage`.
- Tulip symbols (e.g., `roundabout.exit_2`, `junction.turn_left`).
- Road transitions captured in `road.current` and `road.next`.
- Tags such as `[cyclists]` and `[photo]` for downstream tooling.

### Branches

The `skip_guilleries` branch demonstrates how to deviate from the trunk and rejoin later, reusing the same instruction structure. Branches can be referenced via `alternatives` arrays on trunk instructions.

### Locations

Each location supports coordinates, Plus Codes, and What3Words references. The demo mixes named POIs (e.g., *Coll de Sant Marçal*) with raw coordinates to show both options.

## Validation

Use the published JSON Schema to check conformance before sharing. The schema is resolver-friendly (it includes a `$id`) and versioned snapshots are available for pinning builds. Validation catches type errors, out-of-range values, and unknown symbol IDs.

```bash
npx ajv validate \
  -s https://openroadbook.com/schemas/orb.schema.json \
  -d demo.orb.yaml --spec=draft2020
```

Substitute `demo.orb.yaml` with your own files to check conformance. Validation ensures headings stay within 0–359, distances are non-negative, and symbols point to known registry IDs.

### Schema coverage

- **Top level:** Requires `meta` and `stages`.
- **Authors & units:** Standardised via dedicated definitions.
- **Instructions:** Validate headings, distances, tags, and tulip references.
- **Extensions:** Permissive to allow vendor namespaces.

## Using the demo

Copy the demo as a starting point when authoring new stages. Edit `meta` and `entries`, run schema validation, and publish the resulting file alongside any custom extensions or renderer settings.

- [Download demo.orb.yaml](/demos/demo.orb.yaml)
- [Fetch the schema](/schemas/orb.schema.json)
- [Schema v1.0 snapshot](/schemas/1.0/orb.schema.json)
- [Back to format overview](/format/)
