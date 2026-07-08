# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A single-file, static HTML/CSS/JS **prototype** (`prototype.html`) exploring how a SOAR-style
"Automation" module (workflow list + workflow builder canvas) could be added to Motadata's
existing AIOps product. There is no build system, package manager, server, or test suite —
it's opened directly in a browser.

Three reference-screenshot folders (never edit, only read for design reference):
- `motadata_reference_screenshots/` — the real Motadata product's existing look (dark navy
  theme, top bar, left icon rail, alert dashboards). Highest priority for visual consistency.
- `datadog_reference_screenshots/` — Datadog's Workflow Automation / Bits Agent Builder product,
  used as the primary feature/UX reference for the workflow list, analytics dashboard, and the
  workflow-builder canvas (nodes, side panel, variable picker, action catalog).
  Screenshots are timestamped sequentially (filename = capture time); browsing them in order
  usually follows one user click-through flow, so check neighboring timestamps for context.
- `canvas_reference_screenshots/` — closeups of Datadog's workflow canvas/builder specifically
  (node config panel, Configure/Outputs/Context Variables tabs, connections, the "All Actions"
  catalog modal).

Design intent (from prior conversation with the user, not written elsewhere): borrow Datadog's
*information architecture* (tabs, panel structure, variable/parameter model) but keep the visual
language distinct — Motadata's dark navy/coral palette, thin accent-bar section dividers instead
of Datadog's full-width purple bands, a compact floating rail instead of a full icon column, and
only "necessary" features per iteration rather than full parity (e.g. Datadog's 2.7k-action
catalog is intentionally reduced to a handful of curated Motadata actions + integrations).

## Working with `prototype.html`

There is nothing to build or install. To view changes:

```bash
xdg-open prototype.html        # or: google-chrome prototype.html
```

To verify a change without a display, render headlessly and screenshot (this is the pattern
used throughout this project's history — copy the file, inject a small `<script>` before
`</body>` that calls the page's own functions (e.g. `setActivePanel('builder')`,
`.click()` on a tab/button) to drive it into the state you want to check, then screenshot):

```bash
google-chrome --headless=new --disable-gpu --screenshot=out.png \
  --window-size=1600,1000 --run-all-compositor-stages-before-draw \
  --virtual-time-budget=2000 "file:///path/to/copy.html"
```

Always sanity-check the inline script after editing it (extract the `<script>...</script>` body
and run `node --check` on it) — there is no linter or test runner in this repo to catch syntax
errors otherwise.

When adding charts/stat tiles/analytics visuals, use the `dataviz` skill (categorical/status
color choices in this file were derived and validated that way — see the `--chart-*` CSS custom
properties in `:root`) rather than picking colors ad hoc.

## Architecture of `prototype.html`

Everything lives in one file: `<style>` in `<head>`, all markup in `<body>`, all behavior in one
`<script>` at the end. Roughly in order:

**CSS** — one `:root` block of design tokens (`--bg-*`, `--text-*`, `--accent`, `--chart-*`),
then component styles grouped by comment headers (topbar/sidebar, dashboard cards, alerts table,
Automation page tabs/blueprint grid, workflow-table + KPI/analytics components, and a large
`/* Workflow Builder (canvas) */` section for the builder's canvas/rail/catalog/side-panel).

**Markup** — a fixed shell (`.topbar` + `.sidebar` + `.content`) containing sibling `<section
class="panel" id="panel-*">` elements, one per top-level nav destination:
- `panel-dashboards`, `panel-alerts` — mostly static placeholder content.
- `panel-automation` — tabs: **All Workflows** (blueprint banner + search + "My workflows"
  toggle + table rendered by `renderWfList()` from the `WORKFLOWS` registry: star, status dot,
  status pill, trigger icons, owner, tags, last execution), **Blueprints** (category sidebar +
  search + integration filter + sort chips + card grid, all rendered from `BLUEPRINTS` +
  `WORKFLOWS`), **Analytics** (the "Workflows Overview" dashboard — KPI row, two SVG axis
  charts with gridlines/nice ticks, donut, split cards, ownership bars and four tables, all
  rendered by `renderAnalytics()` from the single `ANALYTICS` data object so the numbers
  can't drift apart: daily execs sum to the Runs KPI, which equals the donut total and the
  Top-Workflows column; `fails` sums to the Failed-Runs KPI and both failure tables. Change
  numbers in `ANALYTICS`, not in markup; chart colors are the validated `--chart-*` tokens
  — run the `dataviz` skill's validator before introducing new ones).
- `panel-soar` — **Security Workflows (SOAR)** gallery (Datadog's SOAR page): search +
  integration filter + Most viewed/Newest/Most actions sort chips + card grid rendered by
  `renderSoar()` from `SOAR_BLUEPRINTS` (18 entries; reuses the Blueprints tab's `.bp-*` CSS).
  Every card maps to a real `WORKFLOWS` canvas — 6 hand-built, 12 generated by
  `genSoarWorkflow()` (trigger → Get Security Signal → mid steps → Slack notify), all
  `listed:false` so they don't pollute the All Workflows table. Card click opens the builder
  preview with `{from:'soar'}`; "Go to Workflow Automation" jumps to the All Workflows tab.
- `panel-builder` — the workflow canvas (see below).
- `panel-generic` — a catch-all placeholder for any other left-nav item.

Floating layers live at the end of `<body>`: `#toast`, `#varPopover`, `#nodeMenu` (per-step
Run/Duplicate/Delete), `#paramModalBackdrop` (Edit Input/Output Parameter + Variable dialogs),
and `#catalogBackdrop` (the "All Actions" catalog modal).

The left sidebar's items are generated at runtime from the `NAV` array and wired to
`setActivePanel(id)`, which shows `#panel-<id>` or falls back to `panel-generic`.

**JS — data model.**
- `STEP_LIB` is the single library of every trigger/logic/action/integration step:
  `kind` (trigger|logic|action), `group`, `name/label/sub/desc`, `conn` (stored-connection name,
  renders the Connection row), `schema` (fields; drives both the catalog detail pane and the
  Configure tab, which `stepConfigHTML()` generates as contenteditable `.chip`s whose edits
  persist per-node in `node.cfg`), `outputs`, and `featured`/`isNew` flags for catalog sections.
- `WORKFLOWS` is the multi-workflow registry (nodes/edges/notes + `params.inputs/variables/
  outputs` + list metadata: status/owner/tags/lastModified/lastExec/execs/starred/`listed`).
  Two are full demos (`restart`, `aws` — the Compromised AWS Access Key Containment flow);
  the rest are small canvases that exist so every blueprint card previews something real.
  `BLUEPRINTS` maps registry ids to category/stats/integrations for the Blueprints tab;
  `SOAR_BLUEPRINTS` does the same for the SOAR page (its `actions` count is computed from the
  workflow's non-trigger node count, so it stays honest if a canvas changes).
- `loadWorkflowIntoBuilder(id, mode, opts)` points the canvas at a registry entry (live
  references, so edits persist for the session). `mode:'preview'` is the blueprint view: a
  "Create From Blueprint" button replaces Save/Run/Publish, and the rail, ports, kebabs,
  note-delete and executions bar are hidden (`preview-mode` class + conditional rendering).
  `opts.from` ('automation' | 'soar') sets `builderFrom`, which drives the crumb
  (`Automation / Blueprints /` vs `SOAR / Security Workflows /`), the back button target/title,
  and which nav item stays highlighted while the builder is open. Create From Blueprint
  deep-clones into a new listed draft and switches to edit mode (origin resets to Automation,
  where the copy now lives).

**JS — canvas engine.** Hand-rolled pannable/zoomable node-and-edge canvas:
- `renderCanvas()` rebuilds nodes/notes from the model; `redrawEdges()` recomputes SVG beziers +
  True/False edge labels. Every non-trigger node renders **two dual-nature port buttons** —
  `button.port-in` (top) and `.port.port-out` (bottom; triggers get out only). **Click** opens
  the catalog ("add after" from the bottom port, "add before" from the top one); **drag** draws
  a live dashed `path.temp-edge` — dropping on another node creates the edge directly
  (`finishConnect`: rejects self/duplicate/into-a-trigger, auto-labels condition out-edges
  True/False), dropping on empty canvas opens the catalog carrying the drop position so
  `addStep(tpl, parentId, ctx)` places the new step there pre-wired (`ctx.mode`
  'after'|'before', `ctx.pos`). Node headers render a kebab that opens `#nodeMenu`
  (Run step / Duplicate / Delete; delete also removes touching edges).
- Pan/zoom/drag all go through one `mousedown`/`mousemove`/`mouseup` state machine on
  `#canvasWrap` (ports/kebab/note-delete are intercepted before drag starts); wheel pans,
  ctrl/cmd+wheel zooms toward the cursor, `fitView()` frames the graph, and the rail's
  auto-layout button (`autoLayout()`) BFS-levels the tree and re-centers rows.
- Notes are sticky annotations: created empty (placeholder via `.note-text:empty::before`),
  double-click to edit, × to delete. The rail note button creates one and opens it for editing.
- **Run** follows Datadog's input-parameter semantics: `runWorkflow()` opens the
  `#runModalBackdrop` form when the workflow defines inputs (required unless a default exists;
  defaults prefilled; an `allowed` list renders a select), then `executeRun(inputVals)` walks
  the graph breadth-first, flashes `.running`/`.done`, and prepends an exec row carrying
  `inputs` and — because the run succeeded — `outputs` (the workflow's output parameters).
  The Executions bar renders Inputs/Outputs columns; failed rows show "not populated" since
  output parameters only exist after a successful completion. Publish toggles draft/published
  and syncs the pill, button label and list row.
- **Input/Output parameter model** (Datadog semantics): inputs are immutable workflow
  arguments read anywhere as `{{ Trigger.<name> }}` — the IVO rows show that reference, a
  required/optional pill (default value ⇒ optional) and an immutable lock; outputs are return
  values whose rows show `← <value ref>`. `contextTreeHTML()` lists a "Trigger (input
  parameters)" group built from `params.inputs`. The Save button scans node bodies/`cfg` and
  output values for `{{ Trigger.x }}` references that aren't defined inputs
  (`findUndefinedTriggerRef`) and opens the input modal prefilled to make them explicit —
  the implicit→explicit flow.
- The right `#sidePanel` has two modes: `renderSideDefault()` — workflow name/description plus
  the Inputs / Variables / Outputs panel, whose + / row-click / trash actions open the working
  parameter modals (`openParamModal(kind, index, preset)` — the Edit Input Parameter dialog
  carries Display Name + "Use custom display name", Data Type, Description, optional Default
  Value and Allowed Values list, plus a live `{{ Trigger.<name> }}` reference preview) — and
  `renderSideNode(node)` (Configure / Context Variables / Output tabs). `contextTreeHTML()`
  builds the variable tree dynamically from the current workflow (input params, trigger
  outputs, step outputs, custom variables) and is reused by `#varPopover`, which writes into
  the preceding chip **or** modal input.
- The catalog modal (`openCatalog(parentId, section, hint, ctx)`) is a Datadog-style three-pane
  dialog: section sidebar (All Actions / Featured / New / AI / Datastore / Saved Actions /
  Triggers + a "Request Action" link), searchable item list (Triggers shows Featured Triggers +
  All Triggers), and a detail pane with description, Connection, Configuration schema, Outputs
  and an Add/"Use this trigger" button. AI, Datastore and Saved Actions are deliberate empty
  states. Adding a trigger places it beside existing triggers (multiple triggers per workflow
  are supported); adding after a condition auto-labels the edge True, then False.
- Anything still not wired calls `showToast(message)` — the convention for "not implemented in
  this iteration, but the affordance exists."

## Conventions specific to this project

- Keep new UI additions minimal per request rather than building full Datadog feature parity;
  when a Datadog capability is deliberately deferred, prefer a `showToast(...)` stub or an
  explicit empty state over leaving the control dead or removing it.
- Mock data across the Automation tabs is cross-referential (the 4 listed workflows —
  "Auto-Restart Failed Service", "Compromised AWS Access Key Containment", "Escalate
  Unacknowledged Critical Alert", "Suppress Flapping Trap Storm" — recur in the list,
  blueprints and analytics). Keep new mock data consistent with these.
- Action/step config panels that call an external system show a "Connection" row (dot + name +
  "Manage" link) — actions require a stored integration credential, distinct from steps that
  only read Motadata's own data.
- Config fields must accept real values: chips are contenteditable and persist to `node.cfg`;
  modal fields are real inputs validated on save (required-name, unique-name, required-value).
