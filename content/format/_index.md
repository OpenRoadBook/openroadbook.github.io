---
title: "Format Overview"
description: "Learn how the OpenRoadBook adventure format structures entries, symbols, and tasks while leaving room for FIA and competitive extensions."
---

<section class="hero">
  <div class="container hero__inner">
    <div>
      <h1 class="hero__title">OpenRoadBook format</h1>
      <p class="hero__lead">
        The current release centres on simple adventure roadbooks: lean YAML with matching JSON
        mirrors plus scripts to validate and export. Profiles in development extend that same
        structure toward FIA and professional rally operations.
      </p>
      <div class="hero__cta">
        <a class="btn" href="#data-model">See the data model</a>
        <a class="btn btn--secondary" href="#symbol-registry">Symbol registry</a>
      </div>
    </div>
    <aside class="hero__card">
      <h4>Key ingredients</h4>
      <ul class="feature-list">
        <li><strong>Today:</strong> Distance, CAP, tulip, notes, and hazard fields for adventure stages.</li>
        <li><strong>Today:</strong> CLI tooling plus templates to validate, print, and export to GPX.</li>
        <li><strong>Next:</strong> FIA-ready profiles with penalties, scrutineering, and timing metadata.</li>
      </ul>
    </aside>
  </div>
</section>

<section id="overview" class="section section--surface">
  <div class="container split">
    <div>
      <div class="section__header">
        <h2>Why the format exists</h2>
        <p>
          Adventure organizers juggle PDFs, GPX files, screenshots, and spreadsheets. OpenRoadBook
          gives them a single interoperable foundation today, while keeping a clear path to the
          richer data competitive rallies demand.
        </p>
      </div>
      <ul class="feature-list">
        <li>Author once, publish everywhere: print layouts, GPX handoffs, and dashboards.</li>
        <li>Maintain signage-inspired clarity, even after localization or automated conversion.</li>
        <li>Extend via profiles without breaking compatibility—today's adventure rides feed tomorrow's FIA events.</li>
      </ul>
    </div>
    <aside class="fact-card">
      <h3>Status snapshot</h3>
      <dl>
        <div>
          <dt>Current focus</dt>
          <dd>Adventure schema in YAML 1.2 with JSON mirrors for automation.</dd>
        </div>
        <div>
          <dt>Tooling shipped</dt>
          <dd>Validator CLI, GPX exporter, printable templates, and example sets.</dd>
        </div>
        <div>
          <dt>Registry</dt>
          <dd>Stable symbol IDs backed by open SVG artwork and metadata.</dd>
        </div>
        <div>
          <dt>Coming soon</dt>
          <dd>FIA profile, penalties, scrutineering metadata, and telemetry hooks.</dd>
        </div>
      </dl>
    </aside>
  </div>
</section>

<section id="data-model" class="section">
  <div class="container">
    <div class="section__header">
      <h2>Data model</h2>
      <p>
        Entries describe what competitors see and do on course—distance, tulip, CAP heading,
        notes, and any supporting metadata. Tools enforce types so navigation software and print
        workflows stay in sync.
      </p>
    </div>
    <div class="brand-grid">
      <article class="brand-card">
        <h3>Entry fields</h3>
        <ul>
          <li><strong>km</strong> · cumulative distance (float, kilometers)</li>
          <li><strong>tulip</strong> · symbolic ID for navigation diagram</li>
          <li><strong>cap</strong> · heading 0–359 (integer)</li>
          <li><strong>notes</strong> · free text instructions</li>
          <li><strong>symbols</strong> · array of registry IDs</li>
          <li><strong>waypoint</strong> · optional GPS coordinate pair</li>
          <li><strong>speed_limit</strong> · optional integer in km/h</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Profiles &amp; extensions</h3>
        <p>
          Profiles tailor the schema to different environments while preserving compatibility.
          Unknown fields are preserved for forward compatibility.
        </p>
        <ul>
          <li><strong>FIA profile:</strong> sticks to Appendix II requirements.</li>
          <li><strong>Adventure profile:</strong> adds <code>tip</code> and <code>landmark</code> text.</li>
          <li><strong>Custom profiles:</strong> append domain-specific metadata via extensions.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Sample entry</h3>
<pre><code>meta:
  format: OpenRoadBook
  version: 1.0
  event:
    name: Rally of Exampleland
    stage: SS1

entries:
  - km: 12.35
    tulip: turn_left
    cap: 270
    notes: "Gravel, caution rocks"
    symbols: [danger2, jump]
    waypoint: { lat: 41.12345, lon: 2.12345 }</code></pre>
      </article>
    </div>
  </div>
</section>

<section id="symbol-registry" class="section section--surface-alt">
  <div class="container">
    <div class="section__header">
      <h2>Symbol registry</h2>
      <p>
        Symbols keep instructions glanceable under rally pacing. The adventure release ships core
        hazards and services now, and the registry stays stable so FIA and competitive additions
        can land without breaking existing roadbooks.
      </p>
    </div>
    <div class="resource-grid">
      <article class="resource-card">
        <h3>Navigation / Direction</h3>
        <p>Core tulips such as <code>start</code>, <code>finish</code>, <code>turn_left</code>, <code>roundabout</code>.</p>
      </article>
      <article class="resource-card">
        <h3>Hazards</h3>
        <p>Graduated warnings: <code>danger1</code>, <code>danger2</code>, <code>danger3</code>, plus <code>jump</code>, <code>ford</code>, <code>cliff</code>.</p>
      </article>
      <article class="resource-card">
        <h3>Road &amp; surface</h3>
        <p>Surface cues such as <code>tarmac</code>, <code>gravel</code>, <code>sand</code>, <code>offtrack</code>, <code>gate</code>.</p>
      </article>
      <article class="resource-card">
        <h3>Services &amp; controls</h3>
        <p>Logistics touchpoints: <code>fuel</code>, <code>service</code>, <code>speed_limit</code>, <code>neutralization</code>, <code>cp</code>, <code>wp</code>.</p>
      </article>
      <article class="resource-card">
        <h3>Adventure extensions</h3>
        <p>
          Optional IDs like <code>camp</code>, <code>water</code>, <code>food</code>, <code>scenic</code>, <code>border</code>, and <code>town</code> enrich overland journeys.
        </p>
      </article>
      <article class="resource-card">
        <h3>Registry file</h3>
        <p>
          Symbol metadata ships in YAML: ID, display name, category, SVG filename, and description.
        </p>
<pre><code>symbols:
  - id: danger2
    name: "Danger (2 exclamations)"
    category: hazard
    svg: danger2.svg
    description: "Serious hazard, reduce speed"</code></pre>
      </article>
    </div>
  </div>
</section>

<section id="roadmap" class="section">
  <div class="container">
    <div class="section__header">
      <h2>Implementation roadmap</h2>
      <p>
        Focus areas that help the community publish and adopt the format. Track progress in the
        public roadmap or spin up working groups for your specialty.
      </p>
    </div>
    <div class="brand-grid">
      <article class="brand-card">
        <h3>Open symbol registry</h3>
        <ul>
          <li>Commission or crowdsource clean-room SVGs.</li>
          <li>Release assets under permissive licenses (CC0/CC-BY).</li>
          <li>Host registry YAML + artwork in a public repository.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Schema validation</h3>
        <ul>
          <li>Publish JSON Schema to validate YAML/JSON inputs.</li>
          <li>Ensure fields use correct types and registry IDs.</li>
          <li>Automate checks in CI before releasing roadbooks.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Reference converters</h3>
        <ul>
          <li>Produce FIA-style PDF output from OpenRoadBook entries.</li>
          <li>Ship GPX/KML converters for GPS devices.</li>
          <li>Demonstrate digital dash integrations.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Governance &amp; versioning</h3>
        <ul>
          <li>Adopt semantic versioning for schema and registry.</li>
          <li>Publish release notes and changelogs transparently.</li>
          <li>Form a working group of organizers, developers, riders.</li>
        </ul>
      </article>
      <article class="brand-card">
        <h3>Documentation &amp; examples</h3>
        <ul>
          <li>Maintain the specification and quick-start guides.</li>
          <li>Share sample YAML roadbooks with rendered PDFs.</li>
          <li>Highlight community toolchains (CORBS, editors, viewers).</li>
        </ul>
      </article>
    </div>
  </div>
</section>

<section class="section section--surface">
  <div class="container split">
    <div>
      <h2>What’s next?</h2>
      <p>Format overview &middot; Last updated 29 Oct 2025</p>
    </div>
    <div>
      <a class="btn" href="/spec/">Continue to the specification</a>
    </div>
  </div>
</section>
