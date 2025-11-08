---
title: "Quick start"
description: "A short, runnable introduction to authoring, validating, and exporting OpenRoadBook files."
---

# Quick start

A minimal, practical workflow you can follow in minutes: download the demo roadbook, validate it,
make a small edit, and run an export. These steps assume common CLI tooling (Node.js/npm or npx for
AJV). Adapt commands to your environment.

## Prerequisites

Install a JSON Schema validator (AJV CLI is shown) and any reference export tools you use for
GPX/PDF generation. Node.js (>=16) or a similar runtime is sufficient for the examples below.

- Node.js + npm (for `npx ajv`) or an equivalent JSON Schema validator.
- The published schema: `/schemas/orb.schema.json` (resolver-friendly).
- A copy of the demo ORB file: `/demos/demo.orb.yaml`.

## Step 1 — Download the demo

Copy the demo file into your working directory to use as a template or to run validation.

```bash
cp public/demos/demo.orb.yaml ./demo.orb.yaml
```

(If you are browsing the site directly, use the `/demos/demo.orb.yaml` link to download.)

## Step 2 — Validate the file

Run a JSON Schema validation to confirm the document meets the format rules. The schema
includes a stable `$id` so validators can resolve references.

```bash
npx ajv validate \
  -s https://openroadbook.com/schemas/orb.schema.json \
  -d demo.orb.yaml --spec=draft2020
```

A passing run returns with exit code 0. Fix reported errors (types, ranges, missing required
fields, or unknown symbol IDs) before exporting or sharing the file.

## Step 3 — Make a small edit

Update metadata or an entry. Example: set the document title and change an entry note.

```yaml
meta:
  id: "my-event-2025"
  title: "My Local Rally — SS1"

entries:
  - km: 0.00
    tulip: start
    notes: "Start here"
  - km: 2.35
    tulip: turn_left
    cap: 270
    notes: "Caution: loose gravel"
```

Save and re-run the validator to ensure the edits remain conformant.

## Step 4 — Export / render

Use your project's converter or the reference CLI to produce GPX or printable PDFs. Exact
commands depend on the tooling you adopt; the following are examples for common tasks.

### GPX

```bash
# example using a reference exporter script
node tools/export-gpx.js demo.orb.yaml -o demo.gpx
```

### PDF (print layout)

```bash
# example using a renderer script
node tools/render-pdf.js demo.orb.yaml -o demo.pdf
```

If you don't have reference tools locally, the repository's `tools/` folder documents
available converters and scripts. Add CI checks to run validation automatically when
publishing roadbooks.

## Troubleshooting & tips

- Units: the schema expects kilometres for distance unless the document's `meta.units` overrides this — keep units explicit.
- Symbol IDs: make sure every ID in `symbols` exists in the registry; unknown IDs fail validation.
- Profiles: validation rules change per profile (e.g., FIA may require additional fields). Pin schema versions for reproducible builds.

## Where to go next

Read the [format overview](/format/) for detailed field definitions, or the
[specification](/spec/) for normative validation and conformance requirements. If you'd like, I can add a runnable example (Makefile or NPM script) that wires the steps above into a single command.

