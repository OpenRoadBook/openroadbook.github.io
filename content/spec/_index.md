---
title: "Specification"
description: "Normative guidance for the OpenRoadBook adventure release, with a roadmap toward FIA-compliant, professional rally workflows."
---

<section class="hero">
  <div class="container hero__inner">
    <div>
      <h1 class="hero__title">Specification (draft)</h1>
      <p class="hero__lead">
        The specification defines normative schema rules, profile behaviour, and validation
        requirements. Use this document to determine whether a file, tool, or workflow is compliant
        with the OpenRoadBook format.
      </p>
      <div class="hero__cta">
        <a class="btn" href="#introduction">Introduction & scope</a>
        <a class="btn btn--secondary" href="#validation">Validation</a>
      </div>
    </div>
    <aside class="hero__card">
      <h4>Specification goals</h4>
      <ul class="feature-list">
        <li><strong>Today:</strong> Normative rules for the adventure schema and validator behaviour.</li>
        <li><strong>Today:</strong> Open registry governance and baseline compliance checklist.</li>
        <li><strong>Next:</strong> FIA profiles, penalties, telemetry, and pro tooling guidance.</li>
      </ul>
    </aside>
  </div>
</section>

<section id="introduction" class="section section--surface">
  <div class="container split">
    <div>
      <div class="section__header">
        <h2>Introduction &amp; scope</h2>
        <p>
          This document describes the normative expectations for files claiming conformance to the
          OpenRoadBook format. It covers required fields, allowed values, profile semantics, and the
          validation behaviour that tools must implement.
        </p>
      </div>
      <ul class="feature-list">
        <li><strong>Purpose:</strong> Keep roadbooks open, human-readable, and machine-validated.</li>
        <li><strong>Current scope:</strong> Adventure and training stages with baseline metadata.</li>
        <li><strong>Next:</strong> FIA profiles, penalties, and telemetry through transparent RFCs.</li>
        <li><strong>Out of scope:</strong> Proprietary visuals, closed tooling, or vendor lock-in.</li>
      </ul>
    </div>
    <aside class="fact-card">
      <h3>Key concepts</h3>
      <dl>
        <div>
          <dt>Adventure release</dt>
          <dd>Current normative scope covering simple adventure roadbooks.</dd>
        </div>
        <div>
          <dt>Profile</dt>
          <dd>Schema subset or extension (e.g., Adventure today, FIA in development).</dd>
        </div>
        <div>
          <dt>Registry</dt>
          <dd>Authoritative symbol IDs, metadata, and SVG artwork shared across releases.</dd>
        </div>
        <div>
          <dt>Validator</dt>
          <dd>JSON Schema + CLI tooling that enforce compliance before publishing.</dd>
        </div>
      </dl>
    </aside>
  </div>
</section>

<section id="goals" class="section">
  <div class="container">
    <div class="section__header">
      <h2>Goals</h2>
      <p>
        The specification aims to make roadbooks predictable and verifiable across authoring,
        validation, rendering, and exchange. It must enable independent implementations to produce
        consistent outputs from the same inputs.
      </p>
    </div>
    <div class="resource-grid">
      <article class="resource-card">
        <h3>Standardized schema</h3>
        <p>Entries follow a predictable structure, enabling automation and machine validation.</p>
      </article>
      <article class="resource-card">
        <h3>Human readability</h3>
        <p>YAML is canonical so authors can understand the data without specialized tools.</p>
      </article>
      <article class="resource-card">
        <h3>Extensibility</h3>
        <p>Profiles and registry additions expand capabilities without breaking existing roadbooks.</p>
      </article>
      <article class="resource-card">
        <h3>Conversion-ready</h3>
        <p>Designed for rendering into FIA-style PDFs, GPX/KML, and digital dashboards.</p>
      </article>
      <article class="resource-card">
        <h3>Validation-first</h3>
        <p>JSON Schema or equivalent ensures data quality before competitors see it.</p>
      </article>
      <article class="resource-card">
        <h3>Open governance</h3>
        <p>Community-driven updates with transparent releases and versioning.</p>
      </article>
    </div>
  </div>
</section>

<section id="requirements" class="section section--surface-alt">
  <div class="container">
    <div class="section__header">
      <h2>Data requirements</h2>
      <p>
        Files that declare `meta.format: OpenRoadBook` and the matching `meta.version` must meet the
        structural and field-level constraints specified here. The JSON Schema provides the
        machine-readable contract; this document explains intent and edge cases.
      </p>
    </div>
    <div class="brand-grid">
      <article class="brand-card">
        <h3>File structure</h3>
        <ul>
          <li><strong>Format declaration:</strong> <code>meta.format: OpenRoadBook</code></li>
          <li><strong>Version:</strong> <code>meta.version</code> follows semantic versioning.</li>
          <li><strong>Event metadata:</strong> name, date, stage, organizer, regulations.</li>
          <li><strong>Entries array:</strong> ordered list of navigation steps.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Entry schema</h3>
        <ul>
          <li><code>km</code> (number) &mdash; cumulative distance in km.</li>
          <li><code>tulip</code> (string) &mdash; ID referencing the tulip registry.</li>
          <li><code>cap</code> (integer) &mdash; compass heading 0–359.</li>
          <li><code>notes</code> (string) &mdash; human-readable guidance.</li>
          <li><code>symbols</code> (array) &mdash; registry IDs for hazards/services.</li>
          <li>
            Optional: <code>speed_limit</code> (integer km/h), <code>waypoint</code> (lat/lon),
            adventure <code>tip</code> and <code>landmark</code>.
          </li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Symbol registry</h3>
        <ul>
          <li>IDs grouped by navigation, hazards, road/surface, services/controls.</li>
          <li>Adventure appendix defines extra IDs (<code>camp</code>, <code>water</code>, etc.).</li>
          <li>Each record includes ID, name, category, SVG filename, description.</li>
          <li>Registries must remain stable; new symbols append without reusing IDs.</li>
        </ul>
      </article>
    </div>
  </div>
</section>

<section id="validation" class="section">
  <div class="container split">
    <div>
      <div class="section__header">
        <h2>Validation</h2>
        <p>
          Validation verifies types, ranges, and registry references. Implementations should use the
          published JSON Schema as the primary validator and follow the profile-specific rules for
          mandatory or restricted fields. Validation failures must be reported with clear, actionable
          messages.
        </p>
        <p>
          The authoritative schema is published at
          <a href="/schemas/orb.schema.json">https://openroadbook.com/schemas/orb.schema.json</a>,
          matching the `$id` embedded in the JSON Schema for automatic resolver support. Immutable
          snapshots live under versioned paths such as
          <a href="/schemas/1.0/orb.schema.json">https://openroadbook.com/schemas/1.0/orb.schema.json</a>
          so tooling can pin to a specific release.
        </p>
      </div>
      <ul class="feature-list">
        <li>Check that <code>km</code> is numeric and non-negative.</li>
        <li>Ensure <code>cap</code> is an integer in the range 0–359.</li>
        <li>Verify every ID in <code>symbols</code> exists in the registry.</li>
        <li>Require mandatory fields per profile; optional fields may be present.</li>
      </ul>
    </div>
    <aside class="fact-card">
      <h3>Reference tooling</h3>
      <dl>
        <div>
          <dt>Schema</dt>
          <dd>JSON Schema draft with profile-specific clauses.</dd>
        </div>
        <div>
          <dt>Converters</dt>
          <dd>PDF (FIA layout), GPX/KML, digital dash exports.</dd>
        </div>
        <div>
          <dt>Preservation</dt>
          <dd>Unknown fields must be retained for forward compatibility.</dd>
        </div>
      </dl>
    </aside>
  </div>
</section>

<section id="versioning" class="section section--surface">
  <div class="container">
    <div class="section__header">
      <h2>8. Versioning &amp; governance</h2>
      <p>
        Semantic versioning keeps the ecosystem predictable. Community governance ensures changes
        reflect real-world needs.
      </p>
    </div>
    <div class="brand-grid">
      <article class="brand-card">
        <h3>Semantic versioning</h3>
        <ul>
          <li><strong>MAJOR</strong> &mdash; breaking changes to schema or registry.</li>
          <li><strong>MINOR</strong> &mdash; additive changes, new fields, new symbols.</li>
          <li>Each release documents changes in a public changelog.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Governance</h3>
        <ul>
          <li>Community-driven working group with organizers, developers, riders.</li>
          <li>Proposals discussed openly (e.g., GitHub issues / RFCs).</li>
          <li>Transparent approvals and roadmap tracking.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Updates</h3>
        <ul>
          <li>Publish releases with accompanying schema files and assets.</li>
          <li>Tag registry revisions; never delete or repurpose IDs.</li>
          <li>Document migration steps for breaking changes.</li>
        </ul>
      </article>
    </div>
  </div>
</section>

<section id="compliance" class="section">
  <div class="container">
    <div class="section__header">
      <h2>10. Compliance checklist</h2>
      <p>
        A tool or dataset may be advertised as OpenRoadBook-compliant when it satisfies the
        following conditions.
      </p>
    </div>
    <div class="resource-grid">
      <article class="resource-card">
        <h3>Parse &amp; validate</h3>
        <p>Accept OpenRoadBook YAML and execute schema validation with error reporting.</p>
      </article>
      <article class="resource-card">
        <h3>Render or export</h3>
        <p>Output roadbooks using the official symbol registry (PDF, digital, or hybrid).</p>
      </article>
      <article class="resource-card">
        <h3>Preserve forward compatibility</h3>
        <p>Retain unrecognized fields to avoid breaking future minor releases.</p>
      </article>
    </div>
  </div>
</section>

<section id="profiles" class="section section--surface-alt">
  <div class="container">
    <div class="section__header">
      <h2>Profiles</h2>
      <p>
        Profiles tailor the baseline schema for each discipline. The adventure profile ships today;
        FIA and additional competitive variants are in development with the community.
      </p>
    </div>
    <div class="brand-grid">
      <article class="brand-card">
        <h3>FIA profile</h3>
        <ul>
          <li>Draft in progress aligning with FIA Appendix II requirements.</li>
          <li>Restricts symbols to FIA-recognized pictograms and hazard grading.</li>
          <li>Requires compliance with FIA formatting, penalties, and timing rules.</li>
          <li>Targets competitive rally raid and cross-country events.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Adventure profile</h3>
        <ul>
          <li>Ships today with additional symbols like <code>camp</code>, <code>water</code>, <code>food</code>.</li>
          <li>Supports optional fields <code>tip</code> and <code>landmark</code> for storytelling.</li>
          <li>Ideal for non-competitive navigation, training stages, and community rides.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Future profiles</h3>
        <ul>
          <li>Encourage proposals for new disciplines (e.g., TSD rallies, cycling).</li>
          <li>Must specify allowed extensions and registry subsets.</li>
          <li>Should reference validation updates in the JSON Schema.</li>
        </ul>
      </article>
    </div>
  </div>
</section>

<section class="section section--surface">
  <div class="container split">
    <div>
      <h2>Stay aligned</h2>
      <p>Specification v1.0 (draft) &middot; Last updated 29 Oct 2025</p>
    </div>
    <div>
      <a class="btn" href="/format/">Back to the format overview</a>
    </div>
  </div>
</section>
