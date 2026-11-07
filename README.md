# OSS-Factory Skill

**Make your AI coding agent show its work when it picks dependencies.**

With this skill, the agent checks existing tools and libraries before writing code. It verifies
every candidate with real tools, not memory: latest release, license, documented capability,
and whether the packages install together. Then it builds the smallest working combination
and reports why each dependency is there.

[中文说明](#中文说明)

## What it changed in a controlled test

We gave the same 4 small CLI tasks (2 Python, 2 Node) to fresh agent runs, with and without the
skill. The model and machine were the same; the only difference was one sentence telling the
agent to follow the skill. The results were graded afterwards: each project's own tests rerun,
dependencies audited against registry data, and every tool run on tricky inputs prepared
before the runs. [Full write-up and caveats](examples/ab-eval-2026-11.md).

| | Without skill | With skill |
|---|---|---|
| Tools correct on the shared tricky inputs | 4/4 | 4/4 |
| Critical dependency problems | 0 | 0 |
| Own (non-test) code written | 458 lines | **346 lines (−24%)** |
| Alternatives compared, with reasons, written down | 0/4 | **4/4** |
| Install-ability checked before installing (pip/npm dry-run) | 0/3 | **4/4** |
| Licenses recorded | 0/3 | **4/4** |
| Tokens / wall time | 292k / 21.5 min | 326k (+11%) / 24.1 min (+12%) |

The 0/3 means one task in that group used no dependencies, so the item did not apply.

**What this does and does not show.** On small, well-trodden tasks, a current model already picks
sensible libraries without help: the skill did not make the software better. What it reliably
added was a paper trail (which candidates were considered, why, and under what license) and
somewhat leaner code, for roughly 10% more time. Each cell ran once, so treat this as an
illustration, not a statistic. Larger or murkier projects are untested.

## What the agent does with it

1. Writes down what to build and a few checks that prove it is done.
2. Searches both routes: a ready-made tool that covers the whole job, and libraries to compose.
3. Checks candidates with real tools: latest release, license, and whether the docs actually state
   the needed capability.
4. Picks the smallest combination and shows a short decision table.
5. Confirms the packages install together (pip/npm dry-run) before installing anything.
6. Builds, tests, and reports what was reused, what was written, and what is still unverified.

## Install

Claude Code (personal, all projects):

```bash
git clone https://github.com/linjingchen48-max/oss-factory-skill ~/.claude/skills/oss-factory
```

Codex: clone into `~/.agents/skills/oss-factory` (or `<project>/.agents/skills/oss-factory`).
Cursor: `~/.cursor/skills/oss-factory`. Details: [INSTALL.md](INSTALL.md).
No API keys, hooks or extra permissions.

## Verification status

```text
CLAUDE_CODE_SKILL_DISCOVERY = VERIFIED (Claude Code 2.1.309, project-level, 2026-11-03)
CLAUDE_CODE_RUNTIME = NOT_VERIFIED
CODEX_NATIVE_SKILL_LOAD = NOT_VERIFIED
CURSOR_RUNTIME = NOT_VERIFIED
```

In the controlled test, the agents read the skill because the prompt told them to. A host
discovering and triggering it on its own, end to end, has not been verified yet.

## Optional engine

A separate, not-yet-public command-line engine automates the evidence work. `scout` searches
GitHub, pins commits, quotes the docs and fetches deps.dev facts. `check` runs the real resolvers.
`audit` produces a dependency report card for a finished project: invented package names, known
advisories, stale or deprecated versions. The skill works fully without it.
See [engine mode](references/engine.md).

## License

MIT, see [LICENSE](LICENSE) and [LICENSE_NOTICE.md](LICENSE_NOTICE.md).

---

## 中文说明

**让 AI 编程助手在选依赖时，把理由摆出来。**

装上这个 Skill 后，AI 写代码之前会先看有没有现成的工具和库，并用真实工具核查每个候选：
最近一次发布时间、许可证、文档里是否明确写了所需功能、几个包能否装在一起。
然后做出最小可用的组合，并说明每个依赖为什么在那里。

**对照测试结果**：4 个小型命令行任务（Python 和 Node 各 2 个），分别让全新的 AI 在装和不装 Skill 的情况下完成。

- **软件质量没有差别**：两组做出的工具在统一的刁钻输入上都 4/4 正确，都没有严重的依赖问题。
- **装 Skill 后自写代码少 24%**：458 行降到 346 行。
- **选型有据可查**：4/4 写明了比较过的候选、放弃理由和许可证，安装前都先确认依赖能装上；不装 Skill 时这些都没有记录。
- **代价**：多用约 11% 的 token 和约 12% 的时间。

如实说明：在这类小任务上，现在的模型不装 Skill 也能选对库。Skill 带来的主要是透明和精简，而不是更好的软件。
每个格子只跑了一次，没有统计意义；更大的项目还没测过。

安装（Claude Code，对所有项目生效）：

```bash
git clone https://github.com/linjingchen48-max/oss-factory-skill ~/.claude/skills/oss-factory
```

Codex、Cursor 的安装方式见 [INSTALL.md](INSTALL.md)。不需要 API Key，也不会扩大权限。
