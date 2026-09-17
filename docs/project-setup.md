# 毕业设计 design 项目设置

## 采用记录

- 仓库：`lh0601423-png/-`，远端 `origin`，默认分支 `main`。
- 项目：AI 辅助模块化山体滑坡先遣救援机械，工业 / 产品设计毕业设计；面向民用通用应急救援单位，完成山体滑坡核心危险区域先遣救援的模块化无人救援机械系统概念设计。权威需求见 [需求书 v0.2](requirements/requirements-v0.2.md)。
- 当前处于需求定义与总体方案设计阶段，设计工具为 Rhino、Blender、KeyShot、Figma；正式 HUD 工程尚未初始化，其软件技术栈待定。下文的 Python、PyYAML、Bash、PowerShell 是仓库治理 / 验证工具。
- 采用日期：2026-09-17。
- 采用范围：README 快速采用方式 1（GitHub Template Repository / 完整模板）。
- 实际文件来源：`lh0601423-png/-@3699e67ba416d76f73182f3bfd035f06ba022b15`。
- 来源模板：`OasisSaber/TheMasterplan`；模板自报版本 `v5.0.0`，实际复制身份以上述完整 SHA 为准。
- VCS Profile：Git。Jujutsu 不适用，未初始化 `.jj`。
- 首次演练授权：用户在本次会话要求按 README 方式 1 启用，并确认在链接仓库及当前目录实施。
- 授权范围：项目配置、Codex 技能入口、本地验证、任务分支和 Draft PR 演练。
- 当前权威验证入口 `bash scripts/check.sh` 及 Windows 等价入口 `pwsh -NoProfile -File scripts/check.ps1` 已可运行，主要覆盖仓库治理模板、配置和文档；当前没有 HUD 的 lint / typecheck / build 命令或自动测试。
- HUD 或其他业务代码建立后，必须把项目真实的 lint / typecheck / test / build 接入 `scripts/check.sh`，再更新 `AGENTS.md` 中的技术栈和验证事实。
- CI 保留完整模板的本地 reusable workflow，调用方显式指定 `policy-ref: v5.0.0`，避免默认回退到冻结的 `v1`。
- 完整模板由项目维护，未使用 CLI 的受管安装事务；未创建 `.themasterplan/state.json`。
- 只读 `check-update` 实测返回 `NOT_ADOPTED`，表示没有 CLI 受管状态；完整模板的来源与 Profile 由本文件和 `AGENTS.md` 记录。

## 本地使用

需要 Git for Windows（含 Git Bash）、Python 3.12，以及 PowerShell 7。
首次检出后，在项目根目录使用 Python 3.12 建立隔离环境：

```powershell
python -m venv .venv
.venv\Scripts\python.exe -m pip install --disable-pip-version-check -r scripts/requirements.txt
pwsh -NoProfile -File scripts/check.ps1
```

若 `python --version` 不是 3.12，请把首条命令的 `python` 换成已安装的 Python 3.12
可执行文件。PowerShell 入口可通过 PATH 中的 Git 定位非默认安装目录下的 Git Bash。
验证脚本自动使用项目 `.venv`，无需修改系统 Python 或全局 PATH。

Git Bash 中的权威入口：

```bash
bash scripts/check.sh
```

Linux / macOS 使用 `python3 -m venv .venv` 和
`.venv/bin/python -m pip install -r scripts/requirements.txt` 后运行同一 Bash 入口。

Codex 项目技能位于 [SKILL.md](../.agents/skills/themasterplan/SKILL.md)，
只把工作路由到根部 [AGENTS.md](../AGENTS.md)，不复制整套治理规则。
可在下一轮任务中明确要求“使用 themasterplan”。

## 首次 smoke 记录

- 平台：原生 Windows、Git for Windows 2.55.0.windows.5、PowerShell 7.6.5。
- 本地验证 Python：3.12.14；依赖：PyYAML 6.0.3。
- 初始状态：`PARTIAL`。
- 初始检查：175 项单元测试中，Windows 创建符号链接缺少权限导致 1 项错误；其余技术检查通过。
- 适配：仅在 Windows 明确返回 `WinError 1314` 时将符号链接实测标记为跳过；Linux CI 继续执行该测试。
- `bash scripts/check.sh`：通过，175 项测试中 174 项通过、1 项因 Windows 符号链接权限跳过；四项技术检查全部通过。
- `pwsh -NoProfile -File scripts/check.ps1`：通过，同样执行完整权威检查，退出码 0。
- PR 与远端 CI：见本次采用 PR 的检查结果；合并前仍需通过 Linux CI 的符号链接测试。
- 状态保持 `PARTIAL`，直到完成远端 CI、由人类决定 Squash Merge，并验证合并后的 `main`。

## GitHub 设置

模板文件不会复制 GitHub 的服务器端保护。按 [仓库设置说明](repository-settings.md)
核对本项目：`main` 通过 PR 修改、要求实测 CI 检查通过、禁止 force push 与删除，
仅保留 Squash Merge 并禁用自动合并。上游 `v1` 兼容分支无需在本项目创建。
本次只读核对发现 `main` 尚未保护，仓库允许 Merge commit、Rebase 和 Squash，
auto-merge 已关闭。文件配置不等于服务器端保护已配置。
