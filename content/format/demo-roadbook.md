---
title: "Demo Roadbook"
description: "Work through the official OpenRoadBook demo file, download the sources, and validate them against the published schema."
slug: "demo-roadbook"
---

<section class="hero">
  <div class="container hero__inner">
    <div>
      <h1 class="hero__title">Montseny sample roadbook</h1>
      <p class="hero__lead">
        Use this demo to explore how a complete adventure-stage OpenRoadBook file is structured.
        Download the sources, inspect the metadata, and run validation against the canonical JSON Schema.
      </p>
      <div class="hero__cta">
        <a class="btn" href="/demos/demo.orb.yaml">Download demo.orb.yaml</a>
        <a class="btn btn--secondary" href="/schemas/orb.schema.json">View JSON Schema</a>
      </div>
    </div>
    <aside class="hero__card">
      <h4>Bundle contents</h4>
      <ul class="feature-list">
        <li>Adventure profile (<code>profile: adventure</code>).</li>
        <li>One main stage with optional branches.</li>
        <li>Extension blocks for analytics and rendering.</li>
        <li>Published schema reference (<code>$id: https://openroadbook.com/schemas/orb.schema.json</code>).</li>
      </ul>
    </aside>
  </div>
</section>

<section class="section section--surface">
  <div class="container split">
    <div>
      <div class="section__header">
        <h2>Quick metadata tour</h2>
        <p>
          The demo file represents a circular day route around the Montseny and Guilleries ranges.
          It demonstrates how to populate the <code>meta</code> block that every OpenRoadBook document requires.
        </p>
      </div>
      <ul class="feature-list">
        <li><code>meta.id</code> &mdash; <strong>orb-demo</strong>, unique identifier for the document.</li>
        <li><code>meta.title</code> &mdash; Human readable “Montseny i Guilleries”.</li>
        <li>
          <code>meta.units</code> &mdash; Distance in kilometres, headings in degrees, speed in km/h. Explicit units
          avoid ambiguity when tools interpret the data.
        </li>
        <li>
          <code>meta.extensions</code> &mdash; Sample blocks (<code>corbs.render</code>, <code>orb.analytics</code>) illustrate how partner
          tooling embeds previews and computed metrics.
        </li>
      </ul>
    </div>
    <aside class="fact-card">
      <h3>Meta snapshot</h3>
      <dl>
        <div>
          <dt>Profile</dt>
          <dd>adventure</dd>
        </div>
        <div>
          <dt>Labels</dt>
          <dd>demo, asphalt, montseny, circular</dd>
        </div>
        <div>
          <dt>Created</dt>
          <dd>2025-11-01</dd>
        </div>
        <div>
          <dt>Authors</dt>
          <dd>OpenRoadBook Team &lt;team@openroadbook.org&gt;</dd>
        </div>
      </dl>
    </aside>
  </div>
</section>

<section class="section">
  <div class="container">
    <div class="section__header">
      <h2>Inside the stage</h2>
      <p>
        The main stage (<code>montseny</code>) contains a trunk of sequential instructions and optional branches. Each
        instruction highlights a different facet of the schema: tulip symbols, road transitions, locations,
        timing metadata, and tags.
      </p>
    </div>
    <div class="brand-grid">
      <article class="brand-card">
        <h3>Trunk instructions</h3>
        <ul>
          <li>Cumulative <code>distance</code> values with ISO-8601 <code>time_stage</code>.</li>
          <li>Tulip symbols (<code>roundabout.exit_2</code>, <code>junction.turn_left</code>, etc.).</li>
          <li>Road transitions captured in <code>road.current</code> and <code>road.next</code>.</li>
          <li>Tags such as <code>[cyclists]</code> and <code>[photo]</code> for downstream tooling.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Branches</h3>
        <p>
          The <code>skip_guilleries</code> branch demonstrates how to deviate from the trunk and rejoin later,
          reusing the same instruction structure. Branches can be referenced via <code>alternatives</code>
          arrays on trunk instructions.
        </p>
      </article>
      <article class="brand-card">
        <h3>Locations</h3>
        <p>
          Each location supports coordinates, Plus Codes, and What3Words references. The demo mixes
          named POIs (e.g., <em>Coll de Sant Marçal</em>) with raw coordinates to show both options.
        </p>
      </article>
    </div>
  </div>
</section>

<section class="section section--surface-alt">
  <div class="container split">
    <div>
      <div class="section__header">
        <h2>Validate locally</h2>
        <p>
          The JSON Schema published at <code>https://openroadbook.com/schemas/orb.schema.json</code>
          is Draft 2020‑12 compliant. Most validator CLIs and libraries can fetch it directly via its <code>$id</code>.
          If you need a frozen revision, grab the versioned snapshot at
          <code>https://openroadbook.com/schemas/1.0/orb.schema.json</code>.
        </p>
      </div>
      <pre><code>npx ajv validate \
  -s https://openroadbook.com/schemas/orb.schema.json \
  -d demo.orb.yaml --spec=draft2020
</code></pre>
      <p>
        Substitute <code>demo.orb.yaml</code> with your own files to check conformance. Validation ensures
        headings stay within 0–359, distances are non-negative, and symbols point to known registry IDs.
      </p>
    </div>
    <aside class="fact-card">
      <h3>Schema coverage</h3>
      <dl>
        <div>
          <dt>Top level</dt>
          <dd>Requires <code>meta</code> and <code>stages</code>.</dd>
        </div>
        <div>
          <dt>Authors &amp; units</dt>
          <dd>Standardised via dedicated definitions.</dd>
        </div>
        <div>
          <dt>Instructions</dt>
          <dd>Validate headings, distances, tags, and tulip references.</dd>
        </div>
        <div>
          <dt>Extensions</dt>
          <dd>Permissive to allow vendor namespaces.</dd>
        </div>
      </dl>
    </aside>
  </div>
</section>

<section class="section">
  <div class="container split">
    <div>
      <h2>Use it as a template</h2>
      <p>
        Duplicate the demo file when drafting new stages: adjust the metadata, replace the route instructions,
        and keep the structure untouched for maximum compatibility. Running validation before sharing keeps your
        documents ready for tooling pipelines.
      </p>
    </div>
    <div>
      <a class="btn" href="/demos/demo.orb.yaml">Download demo.orb.yaml</a>
      <a class="btn btn--secondary" href="/schemas/orb.schema.json">Fetch the schema</a>
      <a class="btn btn--ghost" href="/schemas/1.0/orb.schema.json">Schema v1.0 snapshot</a>
      <a class="btn btn--ghost" href="/format/">Back to format overview</a>
    </div>
  </div>
</section>
