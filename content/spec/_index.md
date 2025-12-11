---
title: "Specification"
description: "OpenRoadBook formal specification (v1.0)"
hero:
  lead: |-
    The specification defines normative schema rules, profile behaviour, and validation requirements. Use this document to determine whether a file, tool, or workflow is compliant with the OpenRoadBook format.
  ctas:
    - text: "Introduction & scope"
      url: "#introduction"
      style: "btn"
    - text: "Validation"
      url: "#validation"
      style: "btn btn--secondary"
  card:
    title: "Specification goals"
    list:
      - |-
        **Today:** Normative rules for the adventure schema and validator behaviour.
      - |-
        **Today:** Open registry governance and baseline compliance checklist.
      - |-
        **Next:** FIA profiles, penalties, telemetry, and pro tooling guidance.
---

<!-- The full spec is included below -->

# OpenRoadBook specification v1.0 (Draft)

## 1. Introduction

### 1.1 Purpose

OpenRoadBook defines an **open, human‑friendly, machine‑readable format** for roadbooks. It is designed for both **competitive rally events** (FIA‑style) and **non‑competitive adventure travel** (motorbike, 4x4, overland). It enables interoperability between peers, organizers, competitors, and software tools, while remaining easy to author and validate.

### 1.2 Goals

- Provide a **standardized schema** for roadbook data.
- Ensure **human readability** (YAML as canonical format).
- Support **machine validation** and conversion into FIA‑style PDFs, GPX/KML, and digital formats.
- Define a **stable symbol registry** aligned with FIA pictograms.
- Enable **extensibility** without breaking compatibility.

## 2. Scope

This specification applies to:

- **Organized competition** (where FIA compliance is required).
- **Independent adventure navigation** (where GPS may be unavailable or undesired).

It covers:

- Event metadata.
- Roadbook entries (distances, tulips, notes, symbols).
- Symbol definitions for navigation, hazards, services, and adventure travel.

It does not prescribe:

- Exact rendering (fonts, layouts).
- Proprietary extensions beyond the defined schema.

## 3. Terminology

- **Entry**: A single row in a roadbook, typically containing a tulip diagram, distance, and notes.
- **Tulip**: A symbolic representation of a navigation instruction.
- **Symbol**: A standardized pictogram representing hazards, services, or controls.
- **Registry**: The authoritative list of symbol IDs and metadata.
- **Profile**: A defined subset or extension of the specification for a particular use case (e.g., FIA, Adventure).

GPS fields (`waypoint`) are optional. Roadbooks may be fully usable without GPS coordinates, relying solely on distances, tulips, and notes.

## 4. Data Model

### 4.1 File Format

- Canonical authoring format: **YAML 1.2**.
- Alternative representations, such as JSON or XML, are not supported; tools and authors MUST use YAML as the canonical format.
- Files must declare `meta.format: OpenRoadBook` and `meta.version`.

### 4.2 Structure Example

```yaml
meta:
  format: OpenRoadBook
  version: 1.0
  event:
    name: Rally of Exampleland
    date: 2025-10-23
    stage: SS1
    organizer: Example Rally Club
    regulations: FIA Cross-Country Rally Appendix II

entries:
  - km: 0.00
    tulip: start
    cap: 90
    notes: "Start of stage"
    symbols: [start]
    waypoint: { lat: 41.12345, lon: 2.12345 }

  - km: 12.35
    tulip: turn_left
    cap: 270
    notes: "Gravel, caution rocks"
    symbols: [danger2, jump]
    speed_limit: 50
```

### 4.3 Field Definitions

- **km**: cumulative distance (float, km).
- **tulip**: symbolic ID for tulip diagram.
- **cap**: compass heading (0–359).
- **notes**: free text.
- **symbols**: array of symbol IDs from the registry.
- **speed_limit**: optional integer (km/h).
- **waypoint**: optional `{lat, lon}` object.
- **tip** (Adventure profile): optional free text with practical advice.
- **landmark** (Adventure profile): optional free text describing a visible landmark.

## 5. Symbol Registry

### 5.1 Purpose

The registry defines a **stable vocabulary** of symbol IDs. Each ID maps to metadata and an SVG/PNG asset.

### 5.2 Example Entry

```yaml
symbols:
  - id: danger2
    name: "Danger (2 exclamations)"
    category: hazard
    svg: danger2.svg
    description: "Serious hazard, reduce speed"
```

### 5.3 Core Categories

- **Navigation**: `start`, `finish`, `turn_left`, `turn_right`, `straight`, `roundabout`, `junction`
- **Hazards**: `danger1`, `danger2`, `danger3`, `jump`, `ford`, `bridge`, `railroad`, `cliff`, `rocks`, `animals`

This document is a living specification. For changes to the registry or profiles, consult the project governance documents and follow the contribution guidelines.
---
title: "Specification"
description: "OpenRoadBook formal specification (v1.0)"
hero:
  lead: "The specification defines normative schema rules, profile behaviour, and validation requirements. Use this document to determine whether a file, tool, or workflow is compliant with the OpenRoadBook format."
  ctas:
    - text: "Introduction & scope"
      url: "#introduction"
      style: "btn"
    - text: "Validation"
      ---
      title: "Specification"
      description: "OpenRoadBook formal specification (v1.0)"
      hero:
        lead: |-
          The specification defines normative schema rules, profile behaviour, and validation requirements. Use this document to determine whether a file, tool, or workflow is compliant with the OpenRoadBook format.
        ctas:
          - text: "Introduction & scope"
            url: "#introduction"
            style: "btn"
          ---
          title: "Specification"
          description: "OpenRoadBook formal specification (v1.0)"
          hero:
            lead: |-
              The specification defines normative schema rules, profile behaviour, and validation requirements. Use this document to determine whether a file, tool, or workflow is compliant with the OpenRoadBook format.
            ctas:
              - text: "Introduction & scope"
                url: "#introduction"
                style: "btn"
              - text: "Validation"
                url: "#validation"
                style: "btn btn--secondary"
            card:
              title: "Specification goals"
              list:
                - |-
                  **Today:** Normative rules for the adventure schema and validator behaviour.
                - |-
                  **Today:** Open registry governance and baseline compliance checklist.
                - |-
                  **Next:** FIA profiles, penalties, telemetry, and pro tooling guidance.
          ---

          <!-- The full spec is included below -->

          # OpenRoadBook specification v1.0 (Draft)

          ## 1. Introduction

          ### 1.1 Purpose

          OpenRoadBook defines an **open, human‑friendly, machine‑readable format** for roadbooks. It is designed for both **competitive rally events** (FIA‑style) and **non‑competitive adventure travel** (motorbike, 4x4, overland). It enables interoperability between peers, organizers, competitors, and software tools, while remaining easy to author and validate.

          ### 1.2 Goals

          - Provide a **standardized schema** for roadbook data.
          - Ensure **human readability** (YAML as canonical format).
          - Support **machine validation** and conversion into FIA‑style PDFs, GPX/KML, and digital formats.
          - Define a **stable symbol registry** aligned with FIA pictograms.
          - Enable **extensibility** without breaking compatibility.

          ## 2. Scope

          This specification applies to:

          - **Organized competition** (where FIA compliance is required).
          - **Independent adventure navigation** (where GPS may be unavailable or undesired).

          ## 3. Terminology

          - **Entry**: A single row in a roadbook, typically containing a tulip diagram, distance, and notes.
          - **Tulip**: A symbolic representation of a navigation instruction.
          - **Symbol**: A standardized pictogram representing hazards, services, or controls.
          - **Registry**: The authoritative list of symbol IDs and metadata.
          - **Profile**: A defined subset or extension of the specification for a particular use case (e.g., FIA, Adventure).

          GPS fields (`waypoint`) are optional. Roadbooks may be fully usable without GPS coordinates, relying solely on distances, tulips, and notes.

          ## 4. Data Model

          ### 4.1 File Format

          - Canonical authoring format: **YAML 1.2**.
          - Alternative representations, such as JSON or XML, are not supported; tools and authors MUST use YAML as the canonical format.
          - Files must declare `meta.format: OpenRoadBook` and `meta.version`.

          ### 4.2 Structure Example

          ```yaml
          meta:
            format: OpenRoadBook
            version: 1.0
            event:
              name: Rally of Exampleland
              date: 2025-10-23
              stage: SS1
              organizer: Example Rally Club
              regulations: FIA Cross-Country Rally Appendix II

          entries:
            - km: 0.00
              tulip: start
              cap: 90
              notes: "Start of stage"
              symbols: [start]
              waypoint: { lat: 41.12345, lon: 2.12345 }

            - km: 12.35
              tulip: turn_left
              cap: 270
              notes: "Gravel, caution rocks"
              symbols: [danger2, jump]
              speed_limit: 50
          ```

          ### 4.3 Field Definitions

          - **km**: cumulative distance (float, km).
          - **tulip**: symbolic ID for tulip diagram.
          - **cap**: compass heading (0–359).
          - **notes**: free text.
          - **symbols**: array of symbol IDs from the registry.
          - **speed_limit**: optional integer (km/h).
          - **waypoint**: optional `{lat, lon}` object.
          - **tip** (Adventure profile): optional free text with practical advice.
          - **landmark** (Adventure profile): optional free text describing a visible landmark.

          ## 5. Symbol Registry

          ### 5.1 Purpose

          The registry defines a **stable vocabulary** of symbol IDs. Each ID maps to metadata and an SVG/PNG asset.

          ### 5.2 Example Entry

          ```yaml
          symbols:
            - id: danger2
              name: "Danger (2 exclamations)"
              category: hazard
              svg: danger2.svg
              description: "Serious hazard, reduce speed"
          ```

          ### 5.3 Core Categories

          - **Navigation**: `start`, `finish`, `turn_left`, `turn_right`, `straight`, `roundabout`, `junction`
          - **Hazards**: `danger1`, `danger2`, `danger3`, `jump`, `ford`, `bridge`, `railroad`, `cliff`, `rocks`, `animals`

          This document is a living specification. For changes to the registry or profiles, consult the project governance documents and follow the contribution guidelines.

          - **speed_limit**: optional integer (km/h).
          - **waypoint**: optional `{lat, lon}` object.
          - **tip** (Adventure profile): optional free text with practical advice.
          - **landmark** (Adventure profile): optional free text describing a visible landmark.

          ## 5. Symbol Registry

          ### 5.1 Purpose

          The registry defines a **stable vocabulary** of symbol IDs. Each ID maps to metadata and an SVG/PNG asset.

          ### 5.2 Example Entry

          ```yaml
          symbols:
            - id: danger2
              name: "Danger (2 exclamations)"
              category: hazard
              svg: danger2.svg
              description: "Serious hazard, reduce speed"
          ```

          ### 5.3 Core Categories

          - **Navigation**: `start`, `finish`, `turn_left`, `turn_right`, `straight`, `roundabout`, `junction`
          - **Hazards**: `danger1`, `danger2`, `danger3`, `jump`, `ford`, `bridge`, `railroad`, `cliff`, `rocks`, `animals`

          This document is a living specification. For changes to the registry or profiles, consult the project governance documents and follow the contribution guidelines.


## 1. Introduction

### 1.1 Purpose

OpenRoadBook defines an **open, human‑friendly, machine‑readable format** for roadbooks. It is designed for both **competitive rally events** (FIA‑style) and **non‑competitive adventure travel** (motorbike, 4x4, overland). It enables interoperability between peers, organizers, competitors, and software tools, while remaining easy to author and validate.

### 1.2 Goals

- Provide a **standardized schema** for roadbook data.
- Ensure **human readability** (YAML as canonical format).
- Support **machine validation** and conversion into FIA‑style PDFs, GPX/KML, and digital formats.
- Define a **stable symbol registry** aligned with FIA pictograms.
- Enable **extensibility** without breaking compatibility.

## 2. Scope

This specification applies to:

- **Organized competition** (where FIA compliance is required).
- **Independent adventure navigation** (where GPS may be unavailable or undesired).
- `water` — potable water source
