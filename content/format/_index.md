---
title: "Format Overview"
description: "Learn how the OpenRoadBook adventure format structures entries, symbols, and tasks while leaving room for FIA and competitive extensions."
---

<section class="hero">
  <div class="container hero__inner">
<div>
<h1 class="hero__title">Format overview</h1>
<p class="hero__lead">
        This OpenRoadBook standard establishes a file layout, core fields, and symbol registry to be used for roadbooks. The current release targets adventure and non-competitive events; profiles
        provide a path to other disciplines without changing the base structure.
</p>
<div class="hero__cta">
<a class="btn" href="#data-model">Data model</a>
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
<h2>Purpose</h2>
<p>
          Provide a single, unambiguous file format for describing stages and navigation
          instructions so authors and tools can interoperate. The format emphasises explicit units,
          stable symbol IDs, and a small set of well-defined fields.
</p>
</div>
<ul class="feature-list">
  <li>Single source of truth for printed roadbooks, GPS exports, and digital renderers.</li>
  <li>Readable by humans (YAML) and consumable by machines (JSON/validation).</li>
  <li>Profiles and extensions for different assurance levels without breaking existing files.</li>
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
      The data model describes an ordered sequence of entries (instructions) with well-typed
      fields. Authors supply distances, symbol references (tulips), headings (CAP), notes, and
      optional coordinates or metadata used by renderers and converters.
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
      The registry maps short IDs to pictograms, categories, and descriptions. Tools should use
      these IDs for rendering and validation. New symbols append to the registry; existing IDs
      are never reused.
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

<section class="section">
  <div class="container split">
<div>
<h2>Work through the demo</h2>
<p>
        Download the Montseny i Guilleries sample ORB file, validate it against the published schema, and
        use it as a template for your own stages.
</p>
</div>
<div>
<a class="btn" href="/format/demo-roadbook/">Open the demo walkthrough</a>
<a class="btn btn--secondary" href="/demos/demo.orb.yaml">Download the ORB file</a>
<a class="btn btn--ghost" href="/schemas/orb.schema.json">View the schema</a>
</div>
  </div>
</section>
