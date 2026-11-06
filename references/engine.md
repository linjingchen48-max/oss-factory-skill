# Optional private engine

The private OSS-Factory application is not bundled or granted a license by this skill.
Do not assume it exists. Use it only when the user says it is installed or `oss-factory --help`
(or `python -m oss_factory --help` in the user's engine environment) succeeds. Do not search
user directories for .env, tokens or private audits.

## Command-line mode (engine v1.1+)

The engine gathers tool facts; you (the host) do the understanding and the decision.

1. Translate the user's need into one component at a time: `component_id`, `purpose`,
   required/optional `capabilities` with 1–10 search `keywords` each (include English terms
   if READMEs are English), up to three GitHub search `queries`, and up to five
   `repositories` you already suspect fit. Run `oss-factory template` for an example and
   `oss-factory schema scout` for the exact contract. Keep the user's words in `need`.
2. `oss-factory scout request.json --out <evidence dir>` performs read-only GitHub searches
   through the user's `gh` login, pins each candidate to a full commit SHA, reads root
   README/LICENSE/manifests, shows the latest GitHub release, and queries deps.dev for the
   package's version, declared license and advisories. When the README does not mention a
   capability, it reads a few pinned doc files whose path names that capability. It prints
   a Markdown card per candidate and writes JSON evidence. A capability is "claimed" only by
   an exact pinned line (description, README or docs, with a link); "unknown" is not
   "absent". The engine never selects. Exit code 4 means no candidate was found.
3. Decide with the cards: purpose first, then declared capabilities, license, maintenance,
   language/runtime and dependency surface. Read more of a shortlisted repository with your
   own tools when a required capability stays unknown. Scout both an existing tool/plugin
   and building-block libraries when either could fit: reuse a tool that covers the whole
   need with a thin wrapper, otherwise compose libraries; do not glue whole applications.
4. `oss-factory check --ecosystem python|node --require "<pkg spec>" ... --out <dir>`
   asks the real resolver (pip dry-run binary-only for the engine's interpreter, or npm
   lock-only without scripts for the local Node) whether the chosen packages resolve
   together, and evaluates each resolved package's declared license against `--allow`
   (default MIT, Apache-2.0, BSD-2/3-Clause, ISC). Nothing is installed. A different target
   runtime version returns unknown rather than a guess.
5. Then implement, install into the project's own environment, and test as in
   [delivery](delivery.md). Cite the evidence files in the final report.
6. Before delivering, run `oss-factory audit <project dir> --out <dir>`. It checks every direct
   dependency in the root manifests against registry data: missing from the registry (a typo
   or invented name), known advisories for the version used, very new packages, stale or
   deprecated ones, non-registry sources and licenses outside the allow-list. Exit code 6
   means a critical finding: fix it, or report it to the user, before calling the work done.

Neither command clones, builds or runs candidate code. Network failures and missing data are
reported as issues/unknown; do not fill them in from memory.

## Workbench mode

An available v1 workbench can import a PlanningResult or SkillSubmission and run its fixed,
budgeted discovery and single-candidate ranking. Its automatic query profile covers a narrow
set of component types; use command-line mode for other needs. Preserve provider errors,
unknowns and review_required. An engine report does not authorize executing candidate code.

Without the engine, follow the public selection reference using the host's available
tools. Do not fabricate numeric Ranking/Scorecard values or claim private analysis ran.
Small projects may use installed-package evidence and an offline working integration.
