---
title: "OpenRoadBook"
description: "OpenRoadBook is an open interoperability format for rally and adventure roadbooks, combining a human-friendly schema with machine validation."
---

<section class="hero">
  <div class="container hero__inner">
<div>
<h1 class="hero__title">Plot. Navigate. Validate. Standardize.</h1>
<p class="hero__lead">
        OpenRoadBook is the open standard for rally and adventure navigation. Built for clarity and interoperability, it defines a precise schema, signage-inspired marks, and robust validation for every stage.
</p>
<div class="hero__cta">
<a class="btn" href="/format/">Explore the Format</a>
<a class="btn btn--secondary" href="/spec/">View Specification</a>
</div>
</div>
    <aside class="hero__card hero__card--inset">
<div class="hero__card-visual">
        {{< hero_card_artwork >}}
</div>
<div class="hero__card-content">
<p class="hero__card-cta">
<a class="btn btn--secondary" href="/roadmap/">Check out the roadmap</a>
</p>
<ul class="feature-list">
<li><strong>Today:</strong> Adventure-ready schema, signage-based marks, and open validation tools.</li>
<li><strong>Next:</strong> FIA-aligned profiles, richer hazard taxonomy, digital nav integrations.</li>
<li><strong>Future:</strong> Partner dashboards, telemetry, and pro rally extensions.</li>
</ul>
</div>
</aside>
  </div>
</section>

<section id="overview" class="section section--surface">
  <div class="container split">
<div>
<div class="section__header">
<h2>What OpenRoadBook provides</h2>
<p>
          The project specifies a clear file structure, a symbol registry, and a validation surface so
          authors and tools can exchange roadbooks reliably. The current release targets adventure and
          non-competitive events while providing extension points for competitive profiles.
</p>
</div>
<ul class="feature-list">
  <li>Canonical YAML structure (with JSON equivalents) for human and machine use.</li>
  <li>Reference tooling and templates for validation, export, and rendering.</li>
  <li>Example roadbooks that serve as templates and test fixtures.</li>
  <li>Versioned extension points so higher-assurance profiles (e.g., FIA) can be added compatibly.</li>
</ul>
</div>
<aside class="fact-card" aria-labelledby="roadmap-heading">
<h3 id="roadmap-heading">Direction of travel</h3>
<dl>
<div>
<dt>Current scope</dt>
<dd>Adventure and overland events with lightweight, contributor-friendly toolchains.</dd>
</div>
<div>
<dt>Capabilities</dt>
<dd>Schema, validator CLI, print templates, GPX export, and sample datasets.</dd>
</div>
<div>
<dt>Next milestones</dt>
<dd>FIA-compliant profiles, hazard registry, scrutineering workflows, and richer metadata.</dd>
</div>
<div>
<dt>Long-term</dt>
<dd>Professional dashboards, telemetry pipelines, and partner integrations for competitive rallies.</dd>
</div>
</dl>
</aside>
  </div>
</section>

<section id="pillars" class="section">
  <div class="container">
<div class="section__header">
<h2>Design principles</h2>
<p>
        OpenRoadBook focuses on predictable structure, explicit units, and stable identifiers so
        data can be validated, rendered, and transformed by independent tools without losing
        meaning.
</p>
</div>
<div class="resource-grid">
<article class="resource-card">
<h3>Structured data model</h3>
<p>
          Define distance, CAP, tulips, hazards, and attachments with predictable types. Upcoming
          profiles add timing, penalties, and pro rally metadata without breaking compatibility.
</p>
<a class="btn btn--ghost" href="/format/#data-model">See data model</a>
</article>
<article class="resource-card">
<h3>Symbol registry</h3>
<p>
          Reference hazards, services, and surfaces by ID using open SVG assets. Roadmapped updates
          expand the registry for FIA sites, competitive hazards, and localization.
</p>
<a class="btn btn--ghost" href="/format/#symbol-registry">Browse symbols</a>
</article>
<article class="resource-card">
<h3>Validation &amp; tooling</h3>
<p>
          CLI tooling validates YAML, exports GPX, and renders printable layouts. The next wave adds
          scrutineering automation, conversion pipelines, and digital navigation sync.
</p>
<a class="btn btn--ghost" href="/spec/#validation">Validation guidance</a>
</article>
</div>
  </div>
</section>

<section id="audience" class="section section--surface-alt">
  <div class="container">
<div class="section__header">
<h2>Intended audience</h2>
<p>
        The format is intended for event organizers, competitors, software developers, and tool
        builders who need a shared, machine-validated description of stages and instructions.
        Profiles let the same base format meet different assurance and compliance needs.
</p>
</div>
<div class="audience-grid">
<article>
<h3>Organizers</h3>
<p>
          Publish adventure stages with predictable layouts, symbols, and exports now—then adopt
          scrutineering data, penalties, and timing as the FIA profile lands.
</p>
</article>
<article>
<h3>Competitors</h3>
<p>
          Practice on legible, signage-inspired roadbooks today and stay aligned with the future
          competitive format when you step into pro events.
</p>
</article>
<article>
<h3>Software developers</h3>
<p>
          Parse structured entries, export GPX, and integrate with basic dashboards now—then plug
          into telemetry, scoring, and compliance services as the schema expands.
</p>
</article>
<article>
<h3>Tool builders</h3>
<p>
          Align dashboards, printers, and visualization tools to one file today, and extend to
          pro-grade digital nav and partner integrations tomorrow.
</p>
</article>
</div>
  </div>
</section>

<section id="resources" class="section">
  <div class="container">
<div class="section__header">
<h2>Primary resources</h2>
<p>
        Start with the format overview to learn the file layout and symbol registry. Use the
        specification for normative rules and validation requirements, and the demo roadbook as a
        working template.
</p>
</div>
<div class="resource-grid">
<article class="resource-card">
<h3>Format overview</h3>
<p>
          Symbols, schema anatomy, and implementation notes for the current adventure release.
</p>
<a class="btn" href="/format/">Explore the format</a>
</article>
<article class="resource-card">
<h3>Quick start</h3>
<p>
          A runnable walkthrough: download the demo file, validate it, edit, and export. Ideal for getting started.
</p>
<a class="btn btn--ghost" href="/quick-start/">Try the quick start</a>
</article>
<article class="resource-card">
<h3>Specification</h3>
<p>
          Draft requirements, profile hooks, and compliance guidance as we grow toward FIA support.
</p>
<a class="btn btn--secondary" href="/spec/">Read the spec</a>
</article>
<article class="resource-card">
<h3>Demo roadbook</h3>
<p>
          Explore a sample roadbook, download the ORB file, and validate it against the
          published schema.
</p>
<a class="btn btn--ghost" href="/format/demo-roadbook/">View the walkthrough</a>
</article>
<article class="resource-card">
<h3>Community roadmap</h3>
<p>
          Priorities for validation tooling, hazard registry expansion, and competitive rally features.
</p>
<a class="btn btn--ghost" href="/format/#roadmap">View initiatives</a>
</article>
</div>
  </div>
</section>

<section id="assets" class="section section--surface">
  <div class="container">
<div class="section__header">
<h2>Contributing & governance</h2>
<p>
        The project is community-driven. Contributions that improve the registry, validation
        coverage, converters, or documentation are welcome. Governance and versioning policies
        are documented in the repository.
</p>
</div>
<div class="resource-grid">
<article class="resource-card">
<h3>Publish open symbols</h3>
<p>
          Crowdsource clean-room SVGs, license them openly, and grow the registry so adventure and
          FIA events share the same icon language.
</p>
</article>
<article class="resource-card">
<h3>Ship validation</h3>
<p>
          Expand JSON Schema coverage, wire it into CI, and block releases until entries, CAPs,
          hazards, and partner data validate.
</p>
</article>
<article class="resource-card">
<h3>Build converters</h3>
<p>
          Extend CORBS-style tools that turn OpenRoadBook YAML into FIA-style PDFs, GPX/KML exports,
          and digital dashboards.
</p>
</article>
<article class="resource-card">
<h3>Document examples</h3>
<p>
          Publish sample roadbooks, rendered outputs, and quick-start guides so new organizers adopt
          the schema with confidence.
</p>
</article>
<article class="resource-card">
<h3>Coordinate stewardship</h3>
<p>
          Form a working group that keeps versioning transparent, reviews proposals, and aligns
          adoption with adventure and competitive rally needs.
</p>
</article>
</div>
  </div>
</section>
