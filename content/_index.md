---
title: "OpenRoadBook"
description: "OpenRoadBook is an open interoperability format for rally and adventure roadbooks, combining a human-friendly schema with machine validation."
---

<section class="hero">
  <div class="container hero__inner">
    <div>
      <h1 class="hero__title">Adventure roadbooks, ready today</h1>
      <p class="hero__lead">
        OpenRoadBook publishes a simple adventure roadbook schema plus baseline tooling so teams
        can author, validate, and share routes without bespoke software. The roadmap extends toward
        FIA compliance, competitive rallies, and professional navigation systems.
      </p>
      <div class="hero__cta">
        <a class="btn" href="/format/">Explore the format</a>
        <a class="btn btn--secondary" href="/spec/">Read the specification</a>
      </div>
    </div>
    <aside class="hero__card">
      <picture>
        <source srcset="/assets/img/orb-wordmark-dark.svg" media="(prefers-color-scheme: dark)" />
        <img src="/assets/img/orb-wordmark.svg" alt="OpenRoadBook wordmark" />
      </picture>
      <h4>Roadmap</h4>
      <ul class="feature-list">
        <li><strong>Today:</strong> Adventure-focused schema with example stages and print layouts.</li>
        <li><strong>Today:</strong> CLI scripts to parse, validate, and export to PDF or GPX.</li>
        <li><strong>Next:</strong> FIA-aligned profiles, richer hazard taxonomies, scrutineering checks.</li>
        <li><strong>Next:</strong> Digital nav reference apps and integrations for pro rally teams.</li>
      </ul>
    </aside>
  </div>
</section>

<section id="overview" class="section section--surface">
  <div class="container split">
    <div>
      <div class="section__header">
        <h2>Why start with simple adventure roadbooks?</h2>
        <p>
          We want organizers and riders to create and test stages without pro-level infrastructure. Version 0
          captures distance, CAP, tulips, hazards, and attachments in plain YAML so you can print, export, and
          remix routes with minimal tooling.
        </p>
      </div>
      <ul class="feature-list">
        <li>Adventure-first YAML schema with JSON mirrors for automation.</li>
        <li>Baseline CLI validates entries, renders PDFs, and exports GPX handoffs.</li>
        <li>Example library covering weekend rides, training loops, and practice stages.</li>
        <li>Reserved extension slots so FIA and pro rally requirements land cleanly.</li>
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
      <h2>Interoperability pillars</h2>
      <p>
        These pillars make the adventure release usable today while keeping hooks open for FIA-grade,
        professional workflows as we evolve the spec.
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
      <h2>Who uses OpenRoadBook?</h2>
      <p>
        Today’s schema keeps weekend rides, training loops, and demo rallies consistent. As we add
        FIA-ready profiles, these same roles inherit pro-grade capabilities without reinventing
        their workflows.
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
      <h2>Get the documents</h2>
      <p>
        Start with the adventure-focused format, reference the draft specification, and track the
        roadmap that leads to FIA-ready, professional deployments.
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
      <h2>Where the community is heading</h2>
      <p>
        We’re moving from a lightweight adventure release toward professional rally operations.
        Contribute where you have expertise—symbols, validation, converters, or governance.
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
