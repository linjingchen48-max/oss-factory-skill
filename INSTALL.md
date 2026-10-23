# 安装与验证

复制本目录全部内容，保留 `SKILL.md` 与相对目录结构。目标目录名为
`oss-factory`；不要把整个私有工程复制进去。不需要配置 API Key、hooks 或新 MCP。
已有同名 Skill 时先比较内容，不覆盖用户修改。新会话中检查发现与显式调用。

## Codex

项目级推荐位置：`<project>/.agents/skills/oss-factory/`。
个人级位置：`~/.agents/skills/oss-factory/`。优先项目级以避免影响其他项目。
例如在项目根目录执行以下 PowerShell 命令，按提示输入本包解压后的目录：

```powershell
$skillSource = (Resolve-Path -LiteralPath (Read-Host 'Skill 源目录')).Path
$skillTarget = Join-Path (Get-Location) '.agents/skills/oss-factory'
if (!(Test-Path -LiteralPath (Join-Path $skillSource 'SKILL.md'))) { throw '源目录缺少 SKILL.md' }
if (Test-Path -LiteralPath $skillTarget) { throw '目标已存在，请先人工比较；不会覆盖' }
New-Item -ItemType Directory -Force .agents/skills | Out-Null
Copy-Item -LiteralPath $skillSource -Destination $skillTarget -Recurse
```

若目标已存在，不直接执行复制命令。重新打开项目会话，输入 `$oss-factory`
或在 Skill 选择器选择它，并要求宿主报告实际读取的 Skill 文件。
使用已有项目时说明修改范围；新项目先建立空目录并从该目录启动 Codex。
实际工具权限、审批、联网和执行约束由宿主决定，安装不会授予额外权限。

描述可以供宿主自动匹配，但不能把文件存在或验证器通过当成自动触发证据。
当前测试情况见随交付的发布报告；没有观察到真实自动选择时保持未验证。

在新会话中复制以下最小调用，不开发软件、不安装依赖：

```text
使用 $oss-factory Skill，为简单个人记账网站提出最小开源复用方案：
收入支出、月度统计、简单图表、本地保存。只规划，不写代码、不联网安装。
请读取 SKILL.md 和选型参考文件，区分事实、建议、未知项，然后停止。
```

原生发现、读取与执行须以真实宿主记录核实，不能只依据模型声称已使用。
`CODEX_NATIVE_SKILL_LOAD = NOT_VERIFIED`；既有 CLI 在模型请求阶段超时，
不是已证实的 Skill 格式缺陷。本包未增加权限、修改宿主配置或反复重试。

## Claude Code（文档适配，未实机验收）

项目级复制到 `.claude/skills/oss-factory/`，个人级可用
`~/.claude/skills/oss-factory/`。新会话输入 `/oss-factory` 加需求。
沿用原有权限与工作区信任策略；不添加插件、hooks 或权限豁免。

## Cursor（文档适配，未实机验收）

项目级复制到 `.cursor/skills/oss-factory/` 或 `.agents/skills/oss-factory/`，
只安装一份。个人级可用 `~/.cursor/skills/oss-factory/`。
在 Agent 对话输入 `/` 搜索并选择该 Skill，再输入需求。权限仍由 Cursor 管理。
不启用云端同步或上传项目；本包未验证远程或云端模式。

## 官方文档核对

核对日期：2026-10-23。宿主升级可能改变发现行为，首次使用仍需实际验证。

- [Codex Skills](https://developers.openai.com/codex/skills)
- [Claude Code Skills](https://code.claude.com/docs/en/skills)
- [Cursor Skills](https://cursor.com/docs/skills)

## 发布前

本包已获 MIT 授权，版权为 VonEis。人工上传仍需复查敏感信息和文件清单；
发布流程见 [PUBLISH.md](PUBLISH.md)。
不要上传私有引擎、原始日志、`.env`、个人路径、测试数据库或鉴权信息。
