# OSS-Factory Skill

Open-source-first software delivery: choose suitable components, integrate the smallest
working combination, test it, and stop when the user's scope is met.

面向 AI 编程宿主的开源优先软件开发工作流 Skill。优先复用成熟开源组件，
按接口和证据选择最小合理组合，不盲目拼接项目。目标是交付软件，而不是只列 GitHub 推荐。
它指导需求拆解、用途与功能匹配、许可证和依赖核对、最小组合、集成测试与交付。
小项目用短计划；复杂项目可复用已可用的 BMAD，不强制安装或启动其他框架。

## 使用

按 [安装说明](INSTALL.md) 将整个目录复制到宿主支持的 Skill 位置。
在 Codex 中显式输入：

```text
使用 $oss-factory，在当前项目制作个人记账工具：收入支出、月度统计、
简单图表、本地保存。优先复用已有依赖；不做账号、云服务或部署。
```

已有项目先检查代码和用户修改；新项目先指定独立目录。只要求选型时，Skill
停在选型结论；要求开发且有权限时，宿主继续编写、运行测试并交付可运行软件。
更多边界见 [最小示例](examples/ledger-request.md)。

## 公开版与私有引擎

公开版是工作流指令，不包含私有引擎源码、历史审计数据或服务凭据。
没有私有引擎时，宿主仍可用获准的搜索、仓库读取、包元数据、代码工具和测试
完成基础选型与开发；离线时优先验证已安装依赖，并如实记录无法查询的信息。

私有引擎是可选增强，可提供既有 Candidate Fit、Ranking、Compatibility
及专业供应商适配器；本目录不提供这些算法或一个可直接使用的公共服务。
引擎连接需使用者自己提供可用入口，详见 [可选模式](references/engine.md)。

功能匹配、质量、安全、依赖验证和兼容性分别判断。README 声明不等于运行验证，
Star 不证明功能，未知许可证和版本不由模型猜测。Skill 不提供操作系统隔离，
不扩大宿主工具权限；外部发布、付费、系统修改及不可信脚本仍受原审批约束。

## 内容

- `SKILL.md`：主流程、触发范围、完成条件。
- `references/`：选型、交付边界和可选引擎说明，按需读取。
- `examples/`：最小输入案例。
- `agents/openai.yaml`：Codex 显示与默认提示。
- `INSTALL.md`：跨宿主安装与验证；平台未实测时明确标注。
- `PUBLISH.md`：人工 GitHub 发布、安装与回滚步骤，建议首版 `v0.1.0`。
- `SHA256SUMS`：发布文件校验清单（不包含该清单自身）。

## 宿主支持与验证状态

以 Codex 为首个适配目标，安装方式见 [INSTALL.md](INSTALL.md)；同时提供
Claude Code 和 Cursor 的文档适配。状态分别保留为：

```text
CODEX_NATIVE_SKILL_LOAD = NOT_VERIFIED
CLAUDE_CODE_RUNTIME = NOT_VERIFIED
CURSOR_RUNTIME = NOT_VERIFIED
```

已验证：Skill 格式和离线包检查；当前 Codex 会话显式读取指令后完成的独立
记账集成示例。原生 CLI 测试进入 `turn.started` 后模型请求超时，没有证明
成功发现、读取和执行本 Skill；不能将超时直接归因于 Skill 缺陷。
自动匹配也未验证。文档适配不等于宿主运行通过。

## 发布状态与许可

本目录原创 Skill 文件采用 [MIT License](LICENSE)。
Copyright (c) 2026 VonEis

许可范围仅覆盖本公开包，详见 [LICENSE_NOTICE.md](LICENSE_NOTICE.md)，
不代表私有 OSS-Factory Core、审计记录或外部第三方内容开源。
当前为本地准备的 `v0.1.0`，未执行 GitHub 发布；可供人工上传，宿主运行兼容性尚待验证。
