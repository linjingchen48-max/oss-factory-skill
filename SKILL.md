---
name: oss-factory
description: Plan and build software by reusing suitable open-source components, checking functional fit and integration evidence, then implementing the smallest working combination. Use for open-source-first development or component selection; not for unrelated edits or repository popularity lists.
---

# OSS-Factory

Deliver the user's requested software when implementation is authorized. For selection-only
requests, deliver the decision and stop. This skill grants no tool permissions.

1. Inspect existing code and clarify essential behavior, constraints and completion checks.
   Keep user requirements separate from suggested stack choices. For a small app, a short
   plan suffices; use an available BMAD workflow for substantial uncertainty, without
   installing it or inventing background host access.
2. Read [component selection](references/selection.md). Prefer the optional existing
   OSS-Factory engine when available; otherwise use the host's permitted search/read tools
   and package metadata. The public skill works without private source or services.
3. Review project purpose before quality. Distinguish a business app, library/SDK, CLI,
   development tool, example/tutorial and scaffold. Map evidence to required capabilities.
   README claims are declarations, not executed behavior. Missing evidence stays unknown.
4. Choose the smallest reasonable combination: one suitable project is enough; two or
   three independent libraries can be better. Do not glue whole applications together
   without interface, data ownership and dependency evidence. Reuse installed dependencies
   before adding new ones. Implement trivial business logic directly.
5. Present a short decision: component → role → source/version → fit → gaps → integration
   boundary → license/compatibility unknowns. Keep Fit, Ranking, confidence, security,
   dependency verification and compatibility independent. Never invent provider results.
6. If the user requested development, use the host's code tools to implement, integrate,
   test and fix within the approved workspace. Follow [delivery boundaries](references/delivery.md).
   Do not stop at recommendations when software was requested. If access is blocked,
   finish the permitted offline parts and state exactly what could not be verified.
7. Verify the original acceptance checks. Report actual commands/outcomes, runnable entry,
   reusable versus custom code and remaining unknowns. Stop once the requested version
   works and relevant checks pass; do not create a follow-on phase automatically.

Avoid adding unrequested SaaS features, services, queues, agents or databases. Do not
keep replacing providers merely because a noncritical dimension is unknown. No automatic
deployment, paid calls, unreviewed install scripts or candidate-source execution beyond
host/user permission. A skill is not an OS sandbox. Never read or publish credentials.

For an offline exercise, use [the small ledger request](examples/ledger-request.md).
For optional engine integration, read [engine mode](references/engine.md) only if available.
