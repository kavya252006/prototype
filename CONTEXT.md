# Session Context — Motadata SOAR / Automation Prototype

This file is a narrative handoff of everything done so far, for picking the work back up after
a restart or a new session. For file-by-file architecture (how the canvas engine works, where
`WORKFLOW_STEPS` lives, etc.) see **`CLAUDE.md`** instead — this file is the "why" and "what
happened", that one is the "how it's built".

## The goal

`prototype.html` is a static, single-file HTML/CSS/JS mockup exploring how a SOAR-style
**Automation** module (a workflow list + a visual workflow builder) could be bolted onto
Motadata's existing AIOps product. It is a prototype for internal review/pitching, not a real
app — there is no backend, no persistence; everything is mock data wired up with just enough JS
to feel real when clicked through.

The three `*_reference_screenshots/` folders are design references the user captured themselves,
in priority order:
1. **`motadata_reference_screenshots/`** — the real Motadata product's existing visual language
   (dark navy theme, top bar, left icon rail, alert dashboards with donut charts). This is what
   the prototype's overall chrome must stay visually consistent with.
2. **`datadog_reference_screenshots/`** — Datadog's "Workflow Automation" / "Bits Agent Builder"
   product. Used as the main *feature and UX* reference (what a workflow list looks like, what
   an Analytics/notebook dashboard looks like, how the canvas builder's side panel, variable
   picker, and action catalog work). Filenames are capture timestamps — browsing sequentially
   usually replays one click-through session, so neighboring timestamps give context.
3. **`canvas_reference_screenshots/`** — closeups specifically of Datadog's canvas/builder (node
   config panel, Configure/Outputs/Context Variables tabs, the "All Actions" catalog modal,
   connections).

Explicit user direction throughout: borrow Datadog's **information architecture**, not its visual
skin — keep Motadata's navy/coral palette, use a differentiated look (e.g. thin accent-bar
section dividers instead of Datadog's full-width purple bands, a compact floating rail instead of
a full icon column), and add only the "necessary" subset of features per iteration rather than
full Datadog parity. Ask before assuming which reference screenshot applies when ambiguous.

## What's been built, in order

1. **Automation → All Workflows tab**: was an empty placeholder; became a search box + table of
   3 mock workflows (name/trigger, status pill, last modified, created by), each row clickable
   (one opens the real builder demo, the others toast "later iteration").

2. **Automation → Analytics tab (v1, minimal)**: added as a third tab next to All Workflows /
   Blueprints. Started as a simple 4-KPI-card row + one "Most Active Workflows" table.

3. **Workflow builder canvas — made dynamic**: replaced the old hardcoded/static node layout and
   fixed-position "+" popover with a real pannable/zoomable canvas engine:
   - Click-drag empty canvas to pan, scroll to pan, ctrl/cmd+scroll to zoom toward the cursor,
     +/−/fit controls.
   - Nodes and sticky notes are draggable; edges are SVG bezier curves that redraw live as you
     drag; notes are double-click-to-edit.
   - A floating left rail (Add step / Triggers / Add note) replaced Datadog's full icon column.
   - A slide-in **step catalog drawer** (search + grouped Triggers/Logic/Motadata
     Actions/Integrations) replaced Datadog's giant "All Actions" modal — this is one of the
     intentional differentiators.
   - Clicking a leaf node's "+" opens the catalog in "add after this step" context and wires the
     new node's edge automatically.
   - Extended `WORKFLOW_STEPS` with real Configure-tab content for the new step types (Acknowledge
     Alert, Run NCCM Command, Block IP, Send Email, Create ITSM Ticket, HTTP Request, Set
     Variable, Wait, For Each), each with a "Connection" field where the step calls an external
     system, modeling the real product concept that actions need a stored integration credential.

4. **Variables/parameters made real** (this was explained to me at length by the user, sourced
   from their own research conversation with Datadog's AI — context variables vs. step-output
   variables vs. source-object variables vs. custom mutable variables, and confirmation that
   Datadog "actions" are just parameterized API calls with no hidden runbook engine behind them):
   - Added a **Variables** section to the workflow-level side panel (between Input and Output
     Parameters), matching Datadog's Inputs/Variables/Outputs grouping.
   - Made the `{ }` insert-variable buttons functional: clicking one opens a popover
     (`#varPopover`) listing the grouped context-variable tree; clicking a variable inserts its
     `{{ ... }}` token into the field and closes the popover. (Previously this was a toast stub.)

5. **Automation → Analytics tab (v2, full rebuild)**: after finding the actual Datadog
   "Workflows Overview" analytics dashboard in the screenshots (it opens in a separate
   notebook-style page, reachable via the Analytics tab's external-link icon), rebuilt the tab to
   mirror its section order: KPI summary → Execution Count per Day (bar chart) + Successful vs
   Failed Executions (stacked bar chart) → **Workflow Executions** band (Trigger Source Breakdown
   donut + two Successful-vs-Failed stat cards) → **Workflow Ownership** band (creator count +
   per-creator horizontal bars) → **Top Workflows** band (two tables with inline mini-bars) →
   **Top Actions** band (same, per action). All chart colors were chosen and validated with the
   `dataviz` skill against this app's actual dark card surface (`#101d33`) — see the `--chart-*`
   custom properties in `:root`. Mock numbers are deliberately cross-referential (e.g. "Failed
   Runs (7d): 10" agrees with the Top Failing Workflows table and the stacked-bar chart).

6. **`CLAUDE.md`** was written, documenting the architecture (canvas engine internals, panel
   structure, `NAV`-array-driven sidebar, conventions like the `showToast(...)` stub pattern for
   deferred features).

7. **Big "production-ready" pass (10 user-numbered changes at once)** — the user asked to port
   the remaining Datadog details from the screenshots and make everything actually work:
   - **Multi-workflow registry** (`WORKFLOWS`): the canvas now loads any of 7 workflows.
     New full demo: **Compromised AWS Access Key Containment** (Security-Signal trigger →
     Get Security Signal → AWS Identity Type → IAM User or Role → Update Access Key / policy
     branches → Send Slack Message), replicated from the Datadog blueprint screenshots.
   - **Workflow-level Inputs / Variables / Outputs** side panel with fully working
     **Edit Input Parameter** (Display Name + "Use custom display name", Data Type, Description,
     optional Default Value with the "optional at run time" note, Allowed Values list with
     "Allow extra values") and **Edit Output Parameter** (Value with `{ }` variable insert,
     Data Type, Default Value) and **Variable** modals — all real fields with validation.
     Variables section header carries the "$.Helpers.setVariable()" hover tooltip.
   - **Catalog rebuilt as the Datadog-style "All Actions" modal** (this deliberately replaced
     the earlier slide-in-drawer differentiator at the user's explicit request): section
     sidebar (All/Featured/New/AI/Datastore/Saved Actions/Triggers + Request Action), search,
     Featured Triggers / All Triggers, right-hand detail pane with configuration schema
     (Schedule shows "RRule Expression* — RRule expression for the trigger") and Add buttons.
     AI/Datastore/Saved are explicit empty states, not dead links.
   - **Connection ports on every node** (bottom-center + that grows on hover) opening the
     catalog in "add after" context; **per-step kebab menu** (Run step / Duplicate / Delete);
     **multiple triggers per workflow**; condition out-edges auto-label True then False.
   - **Notes fixed**: new notes start empty with a "Double-click to add text" placeholder and
     immediately editable; × deletes them.
   - **Rail** kept deliberately smaller than Datadog's (no Edit-with-AI, no Agent): Add step,
     Add trigger, Add note, and a working **Apply auto layout** (BFS levels + fit view).
   - **Run** simulates an execution (nodes flash running/done) and writes into the collapsible
     **Executions** bottom bar; **Publish/Unpublish** toggles state and syncs the list.
   - **All Workflows tab** rebuilt Datadog-style: Start-with-Blueprints banner, search by
     name/tag/owner, My-workflows toggle, favorites star, status dot, trigger icons, owner
     avatar, tag pills, last-execution cell.
   - **Blueprints tab** rebuilt: category sidebar with counts, search, Filter-by-Integration,
     Most-viewed/Newest/Most-actions sort chips, thumbnail cards with view/action stats and a
     hover "View Blueprint" overlay. Every card opens a real read-only **blueprint preview**
     (crumb `/ Blueprints /`, Create From Blueprint button) and **Create From Blueprint**
     deep-clones into a new editable draft in the list — the small blueprint-only canvases
     (Isolate Compromised Host, Block Suspicious IP, SLA Breach…) exist to make that work.
   - **New Workflow** opens an empty canvas with the trigger catalog pre-opened.
   - Step Configure chips are contenteditable everywhere and persist per-node (`node.cfg`);
     the variable popover writes into chips and modal inputs alike.
   - Everything was headless-tested (23 driver pages, ~100 assertions — list filters, modals,
     ports, kebab actions, notes, auto layout, run, publish, preview/clone, catalog sections,
     search, navigation) plus screenshot review of each surface.

8. **SOAR section (Security Workflows page)** — replicated Datadog's Security Workflows (SOAR)
   gallery (screenshots 14-08-37/14-08-41) as a new top-level **SOAR** nav item (NEW tag):
   - Page head ("Security Workflows (SOAR)" + "Go to Workflow Automation ›" which jumps to the
     All Workflows tab), search by name/category/integration, Filter-by-Integration select,
     Most viewed / Newest / Most actions sort chips, count line, and an 18-card grid reusing
     the Blueprints tab's card CSS.
   - The 18 security workflows are the ones named in the screenshots (AWS WAF IP blocking,
     Compromised AWS Access Key Containment, CVE detection, Cloudflare/GreyNoise/AbuseIPDB IP
     handling, Okta suspend/revoke, AWS IAM disable, Azure Entra containment, S3 encryption
     audit + Block Public Access, Jira security ticket, CrowdStrike kill process, SentinelOne
     isolate, key triage…). Every card opens a real canvas: 3 reuse existing demos
     (aws/isolate/blockipbp), 3 are hand-built (iamdisable, oktasuspend, keytriage — the last
     with a True/False condition branch), 12 are generated by a `genSoarWorkflow()` helper
     (Security-Signal trigger → Get Security Signal → 1–2 mid steps → Slack notify). All are
     `listed:false` so the All Workflows table still shows exactly its 4 rows.
   - Two new catalog actions with full schemas/outputs/connections (marked NEW): Disable IAM
     User (AWS IAM) and Suspend Okta User (Okta), plus 12 new integration icons.
   - Builder origin tracking (`builderFrom`): previews opened from SOAR show crumb
     `SOAR / Security Workflows /`, keep the SOAR nav item highlighted, and the back arrow
     returns to SOAR; Create From Blueprint still lands the editable copy in Automation.
   - View counts/categories mirror the screenshots (1.3K → 34 views); action counts are
     computed from each workflow's actual nodes. Headless-tested with 4 driver pages
     (~45 assertions: render/counts/badges, search/filter/sort/empty-state, preview chrome +
     back, clone + regressions on list/blueprints/catalog) + screenshot review.

9. **Ports v2 + Analytics rebuild + the input/output parameter model** (three user asks):
   - **Dual-nature ports on both ends of every step**: every non-trigger node now has a +
     port on top *and* bottom (triggers: bottom only). Click still opens the catalog ("add
     after" from the bottom, "add before" from the top — before-mode wires new→step);
     **dragging** a port draws a live dashed connection line — drop on another node to create
     that edge directly (self/duplicate/into-a-trigger rejected with explanatory toasts,
     condition out-edges auto-label True/False, hovered valid targets highlight), drop on
     empty canvas to open the catalog and create the chosen step at the drop point, pre-wired
     in the right direction. This closes the long-deferred "manual edge drawing" item.
   - **Analytics tab rebuilt formally**: all charts are now real SVG axis charts rendered by
     `renderAnalytics()` from one `ANALYTICS` data object (per-day executions and outcome
     stacks with y-axis gridlines and nice 0–25 tick scales, peak labels, hover tooltips on
     every mark; an SVG donut with center total and count+% legend; run/step outcome split
     cards; ownership h-bars; four top/failing tables with computed mini-bars). Numbers are
     structurally cross-referential — the same object feeds every KPI/chart/table, so
     128 runs / 10 failures / 78-14-6-2% agree everywhere. Palette re-validated with the
     dataviz skill's validator against the card surface (categorical tokens pass; good/bad
     are status colors, always paired with labels + gaps). Deliberately *not* a copy of
     Datadog's notebook layout (per the user's instruction) — kept Motadata's banded sections.
   - **Input/Output parameters per the Datadog model the user pasted**: inputs are immutable
     run-time arguments referenced as `{{ Trigger.<name> }}` — the side panel shows the
     reference under each row plus a required/optional pill (default ⇒ optional) and an
     immutable padlock; the variable tree gained a "Trigger (input parameters)" group; the
     input dialog previews the reference live. **Run** now opens a "Run Workflow" form when
     inputs exist (required-field validation, defaults prefilled, allowed-values as a select)
     and the Executions bar gained Inputs/Outputs columns — outputs are recorded only on
     successful runs, failed rows show "not populated" (matching "empty if the workflow
     failed"). Saving detects implicit `{{ Trigger.x }}` references typed into steps and
     opens the Add-Input-Parameter dialog prefilled to make them explicit. The Auto-Restart
     demo now exercises the whole loop (alertId input → run form → {{ Trigger.alertId }} on
     the canvas → result output ← Steps.Restart_Service.status).
   - Tested with 3 new driver pages (55 assertions) + SOAR/preview regressions re-run green.

## Conventions / house rules established during this session

- Prefer editing `prototype.html` directly; there's nothing to build/install.
- Verify UI changes by rendering headlessly with Chrome and screenshotting — copy the file,
  inject a small `<script>` before `</body>` that calls the page's own functions
  (`setActivePanel(...)`, `.click()` on a button/tab, or synthetic `MouseEvent`s for drag testing)
  to drive it into the state being checked, screenshot, then delete the temp copy. This has been
  the verification method for every feature so far (list table, analytics tab, canvas pan/zoom,
  node drag, add-step flow, variable insertion).
- Always `node --check` the extracted inline `<script>` after edits — there's no linter here.
- When a Datadog feature is deliberately out of scope for now, leave the affordance in place but
  wire it to `showToast('...comes in a later iteration.')` rather than removing it or leaving it
  dead. Match the existing toast copy style.
- Keep mock data consistent across tabs — the same 3 example workflows ("Auto-Restart Failed
  Service", "Escalate Unacknowledged Critical Alert", "Suppress Flapping Trap Storm") recur
  everywhere; new mock numbers should agree with existing KPIs rather than be invented fresh.
- Use the `dataviz` skill before adding any chart/stat-tile/visualization — don't pick chart
  colors ad hoc.
- At the end of a feature pass, report back which Datadog features were incorporated vs.
  deliberately deferred, since the user tracks that trade-off explicitly.

## Deferred features (raised explicitly, not yet built)

Edge *re*connecting/deleting by dragging an existing edge (drawing new edges between arbitrary
nodes now works via port drag; removing one still means deleting a node),
node rename, error paths (Datadog's orange lasso port), a canvas minimap, the workflow settings
popup (tags/notifications/owner/services on title click), rate limits / mention handles on
triggers, the full multi-integration action catalog (Datadog has 2.7k actions — ours is
intentionally a curated ~27), an AI Agent step type (AI catalog section is an empty state),
Datastores (empty state), Saved Actions content (empty state), GUI/JSON toggle per config
field, live "Test" of a single step against real data, per-field "Advanced" settings
(wait-until-condition, retries), version history / rollback, per-step Permissions tab, and
Private Action Runners for on-prem targets.

Built in pass 7 (previously deferred): node delete/duplicate, multiple triggers per workflow,
auto layout, the Executions bottom bar, Publish state, and the blueprint → editable-copy flow.
Built in pass 9 (previously deferred): manual edge drawing between arbitrary nodes (drag from
either port), add-step-above, run-time input forms, and output-population semantics.

## How to resume

1. Read `CLAUDE.md` for the technical map of the file.
2. Read this file for the narrative/decisions.
3. Open `prototype.html` in a browser (or headless-screenshot it, see above) to see current state.
4. If picking a "next" item, the Deferred list above is the backlog the user has been working
   through one iteration at a time — ask which one before assuming.
