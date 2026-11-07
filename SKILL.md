---
name: oss-factory
description: Open-source-first software building for AI coding agents. Before writing code, find an existing tool or mature libraries that already do the job, verify them with real tools (latest release, license, documented capability, dependency resolution), then build the smallest working combination and test it. Use when asked to build an app, tool or feature; not for unrelated edits.
---

# OSS-Factory: reuse before you write

Goal: working software with as little new code as reasonable, where every reuse decision
rests on evidence you actually checked. This skill grants no extra tool permissions.

1. **Pin down the job.** Restate what to build and 3–6 observable acceptance checks.
   Keep the user's requirements separate from your own stack suggestions.
2. **Search both routes.** (a) An existing tool or plugin that covers the whole need;
   (b) mature libraries to compose. Use real search, repository and package tools.
   Never rely on memory for versions, licenses or maintenance status.
3. **Check each shortlisted candidate** ([selection guide](references/selection.md)):
   - its purpose matches (library, app, CLI, tutorial and scaffold are different things);
   - each required capability is stated in its docs: quote the line. README silence means
     unknown, so look in its docs folder before concluding anything;
   - latest release and recent activity; archived or long-stale is a flag;
   - declared license.
4. **Decide the smallest combination.** If a tool covers the whole need, reuse it with a thin
   wrapper; otherwise compose a few libraries and write the glue. Do not glue whole
   applications together. Write trivial logic yourself rather than adding a dependency.
   Show a short table: component → role → version → evidence → gaps.
   If only a recommendation was requested, stop here.
5. **Confirm they install together** with the real resolver before installing
   (pip `--dry-run`, npm `--package-lock-only --ignore-scripts`). Pin versions. Do not run
   install scripts you have not reviewed.
6. **Build and test** against the acceptance checks ([delivery guide](references/delivery.md)).
7. **Report** how to run it, test results, reused components (version, license, why),
   what you wrote, and what remains unverified. Then stop.

If the optional OSS-Factory engine is installed (`oss-factory --help` works), use its `scout`
and `check` commands for steps 2–5, and `audit` on the finished project before step 7;
see [engine mode](references/engine.md).

Never invent search results, versions, licenses or test outcomes. Do not add unrequested
accounts, cloud services, databases, deployment or paid calls. Never read or publish
credentials.
