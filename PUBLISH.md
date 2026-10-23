# 人工发布 v0.1.0

本说明不会自动执行发布。仓库名建议 `oss-factory-skill`。
只发布本目录的原创 Skill 文件，不发布同级或上层的私有 Core、运行目录或审计记录。
本包采用 MIT，Copyright (c) 2026 VonEis。宿主运行兼容性尚待验证，
发布说明必须保留 README 中的 NOT_VERIFIED 状态。

## 1. 上传前检查

把本公开目录单独复制到一个新的空目录，再从该目录打开终端。
确认根目录只有 `SHA256SUMS` 列出的文件及该清单自身，并检查隐藏文件。
核对每个文件 SHA256：`Get-FileHash -Algorithm SHA256 -LiteralPath <文件>`。
ZIP 的 SHA256 由交付清单另行提供；`SHA256SUMS` 不递归包含自身或 ZIP。

确认没有 `.env`、凭据、私有源码、运行日志/数据库、审计 proof、缓存或未知第三方内容。
不要把测试环境或整个 OSS-Factory 工作区作为仓库根目录。

## 2. 仅在独立公开副本初始化本地 Git

以下命令仅供人工执行。若已位于任何 Git 工作树中立即停止，先核对仓库边界。

```powershell
if (!(Test-Path -LiteralPath SKILL.md) -or !(Test-Path -LiteralPath LICENSE)) { throw '不在公开包根目录' }
git rev-parse --show-toplevel 2>$null
if ($LASTEXITCODE -eq 0) { throw '当前目录属于现有 Git 仓库；停止并检查边界' }
git init -b main
git status --short --untracked-files=all
git check-ignore --no-index .env .env.local probe.log probe.sqlite3
git add -- .gitignore LICENSE LICENSE_NOTICE.md README.md INSTALL.md PUBLISH.md SKILL.md SHA256SUMS agents/openai.yaml references/selection.md references/delivery.md references/engine.md examples/ledger-request.md examples/ledger-result.md
git diff --cached --name-only
git diff --cached --check
git diff --cached
```

逐文件审阅暂存内容，确认只有上述公开文件，再执行：

```powershell
git commit -m "Prepare OSS-Factory Skill v0.1.0"
```

若 Git 要求身份信息，由发布者自行配置；不要照搬他人的姓名/邮箱。
本任务没有自动初始化、暂存或提交 Git。

## 3. 创建 GitHub 仓库与上传（须人工执行）

1. 在 GitHub 页面选择 New repository，名称 `oss-factory-skill`，选择 Public。
2. 若准备推送本地仓库，创建空仓库，不另生成 README、LICENSE 或 gitignore。
3. 最后再次审阅本地暂存/提交的文件范围，确认公开的是 Skill 独立副本。
4. 按 GitHub 页面提供的地址设置 origin，人工执行上传：

```powershell
git remote add origin https://github.com/YOUR_ACCOUNT/oss-factory-skill.git
git remote -v
git push -u origin main
```

将 `YOUR_ACCOUNT` 替换为实际账户，不把 Token 写在 URL 或命令里。
需要认证时使用 GitHub 官方流程。确认远端文件正确后，可人工建立 `v0.1.0`
标签/Release，附当前公开 ZIP 和校验值；不要把运行未验证写成全部平台通过。

## 4. 发布后安装与验证

从仓库取得审核过的 `v0.1.0`，按 [INSTALL.md](INSTALL.md) 复制到
项目 `.agents/skills/oss-factory/`。新开 Codex 会话，显式调用 `$oss-factory`，
执行 INSTALL 的只规划提示。观察真实发现、SKILL.md/参考读取及方案输出；
记录失败阶段。Claude Code、Cursor 同样需要独立实机验证。

## 5. 回滚错误发布

- 普通内容错误：人工 `git revert <错误提交>`，检查后推送修正，并更正/撤下错误 Release。
- 若误公开私有内容：立即停止分发，按需将仓库设为私有或撤下，通知相关人员。
  若涉及凭据，先撤销/轮换，再按 GitHub 的敏感数据移除流程处理历史和派生副本。
- 删除文件、Release 或仓库不能保证互联网副本消失；不要把回滚视为撤回泄露的保证。
- 不默认强推或重写历史；此类动作应由发布者单独确认。本任务不执行任何远程操作。
