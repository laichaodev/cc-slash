# Claude Code 内置命令完整汇总

> 当前版本：**v2.1.160** (2026-06-02)
> 来源：[Claude Code Commands](https://code.claude.com/docs/en/commands)

---

## 目录

- [会话管理](#会话管理)
- [模型与推理](#模型与推理)
- [代码审查](#代码审查)
- [项目配置](#项目配置)
- [自动化与并行](#自动化与并行)
- [工具与诊断](#工具与诊断)
- [AI/API 开发](#aiapi-开发)
- [研究](#研究)
- [权限优化](#权限优化)
- [集成与连接](#集成与连接)
- [其他](#其他)

---

## 会话管理

| 命令 | 类型 | 功能 |
|---|---|---|
| `/clear [name]` | 内置 | 清空上下文，开始新对话（旧对话保留在 `/resume`） |
| `/compact [instructions]` | 内置 | 压缩对话历史，释放 token 空间 |
| `/context [all]` | 内置 | 可视化上下文用量（彩色网格），显示优化建议 |
| `/resume [session]` | 内置 | 恢复之前的会话（按 ID/名称/PR URL） |
| `/branch [name]` | 内置 | 分支当前对话，保留原会话 |
| `/background [prompt]` | 内置 | 将会话转为后台 agent 运行 |
| `/stop` | 内置 | 停止当前后台会话 |
| `/rename [name]` | 内置 | 重命名当前会话 |
| `/rewind` | 内置 | 回退对话/代码到检查点 |
| `/recap` | 内置 | 生成当前会话一行摘要 |
| `/export [filename]` | 内置 | 导出对话为纯文本 |
| `/copy [N]` | 内置 | 复制最近回复到剪贴板 |

## 模型与推理

| 命令 | 类型 | 功能 |
|---|---|---|
| `/model [model]` | 内置 | 切换模型（`s` 当前会话 / `d` 全局默认） |
| `/effort [level\|auto]` | 内置 | 推理力度：`low` `medium` `high` `xhigh` `max` `ultracode` |
| `/fast [on\|off]` | 内置 | 切换快速模式 |
| `/plan [description]` | 内置 | 进入计划模式 |
| `/ultraplan <prompt>` | 内置 | 云端并行规划 |
| `/goal [condition\|clear]` | 内置 | 跨轮次自动完成目标 |
| `/exit` | 内置 | 退出 CLI（后台会话中则 detach） |

## 代码审查

| 命令 | 类型 | 功能 |
|---|---|---|
| `/review [PR]` | 内置 | 本地审查 Pull Request |
| `/security-review` | 内置 | 安全审查：扫描 diff 找注入、认证、数据泄露等漏洞 |
| `/diff` | 内置 | 交互式 diff 查看器（键盘滚动） |
| `/code-review [level] [--fix] [--comment]` | Bundled Skill | 审查 diff：bug + 复用/简化/效率；`ultra` 云端审查 |
| `/simplify [target]` | Bundled Skill | 仅清理优化（不查 bug），自动修复 |
| `/ultrareview [PR]` | 内置 | `/code-review ultra` 的别名 |

## 项目配置

| 命令 | 类型 | 功能 |
|---|---|---|
| `/init` | 内置 | 生成项目 CLAUDE.md |
| `/config` | 内置 | 打开设置界面（主题、模型、输出风格等） |
| `/permissions` | 内置 | 管理工具权限规则（allow/ask/deny） |
| `/memory` | 内置 | 编辑 CLAUDE.md 记忆文件，管理自动记忆 |
| `/add-dir <path>` | 内置 | 添加额外工作目录 |
| `/mcp` | 内置 | 管理 MCP 服务器连接和 OAuth |
| `/agents` | 内置 | 管理 subagent 配置 |
| `/skills` | 内置 | 列出可用 skill（`t` 按 token 排序） |
| `/hooks` | 内置 | 查看 hook 配置 |
| `/ide` | 内置 | 管理 IDE 集成状态 |
| `/plugin` | 内置 | 管理插件 |
| `/reload-skills` | 内置 | 不重启重载 skill 目录（≥v2.1.152） |
| `/reload-plugins` | 内置 | 不重启重载插件 |
| `/update-config` | Bundled Skill | 直接编辑 settings.json，管理权限和环境变量 |
| `/keybindings` | 内置 | 打开键盘快捷键配置文件 |
| `/statusline` | 内置 | 配置终端状态栏 |
| `/theme` | 内置 | 切换颜色主题（含色盲友好主题） |
| `/color [color]` | 内置 | 设置提示栏颜色（无参则随机） |
| `/scroll-speed` | 内置 | 调节鼠标滚轮速度 |
| `/focus` | 内置 | 切换专注视图 |
| `/tui [default\|fullscreen]` | 内置 | 设置终端 UI 渲染器 |
| `/terminal-setup` | 内置 | 配置终端快捷键（Shift+Enter 等） |

## 自动化与并行

| 命令 | 类型 | 功能 |
|---|---|---|
| `/tasks` | 内置 | 列出和管理后台任务 |
| `/workflows` | 内置 | 查看 Dynamic Workflow 运行（≥v2.1.154） |
| `/batch <instruction>` | Bundled Skill | 批量修改：分解为 5-30 个独立单元，并行执行，各自 PR |
| `/loop [interval] [prompt]` | Bundled Skill | 定时重复执行 |
| `/autofix-pr [prompt]` | Bundled Skill | 监听 PR 的 CI 失败/评论，自动推送修复 |
| `/run` | Bundled Skill | 启动并驱动项目应用（≥v2.1.145） |
| `/verify` | Bundled Skill | 构建→运行→观察，确认代码生效（≥v2.1.145） |
| `/run-skill-generator` | Bundled Skill | 为项目编写 `/run` / `/verify` 的启动脚本 |
| `/schedule [description]` | 内置 | 创建云端定时任务 |

## 工具与诊断

| 命令 | 类型 | 功能 |
|---|---|---|
| `/doctor` | 内置 | 诊断安装和配置问题（按 `f` 自动修复） |
| `/debug [description]` | 内置 | 启用调试日志，分析会话问题 |
| `/usage` | 内置 | 会话费用、用量上限、分类统计 |
| `/usage-credits` | 内置 | 配置用量点数 |
| `/insights` | 内置 | 分析会话模式的报告 |
| `/heapdump` | 内置 | JS 堆快照用于诊断高内存 |
| `/help` | 内置 | 显示帮助和可用命令 |
| `/release-notes` | 内置 | 查看 changelog（交互式版本选择器） |
| `/feedback [report]` | 内置 | 提交反馈、报告 bug、分享对话 |
| `/status` | 内置 | 显示版本、模型、账号、连接状态 |

## AI/API 开发

| 命令 | 类型 | 功能 |
|---|---|---|
| `/claude-api [migrate\|managed-agents-onboard]` | Bundled Skill | 加载 Claude API 参考；`migrate` 迁移版本；`managed-agents-onboard` 创建 Managed Agent |

## 研究

| 命令 | 类型 | 功能 |
|---|---|---|
| `/deep-research <question>` | Bundled Workflow | 深度研究：多源搜索 → 交叉验证 → 生成引用报告 |

## 权限优化

| 命令 | 类型 | 功能 |
|---|---|---|
| `/fewer-permission-prompts` | Bundled Skill | 扫描日志，自动添加常用只读命令到 allowlist |

## 集成与连接

| 命令 | 类型 | 功能 |
|---|---|---|
| `/login` | 内置 | 登录 Anthropic 账号 |
| `/logout` | 内置 | 登出 |
| `/setup-bedrock` | 内置 | 配置 Amazon Bedrock |
| `/setup-vertex` | 内置 | 配置 Google Vertex AI |
| `/chrome` | 内置 | 配置 Claude in Chrome |
| `/remote-control` | 内置 | 开启远程控制（从 claude.ai 继续） |
| `/remote-env` | 内置 | 配置 Web 会话远程环境 |
| `/teleport` | 内置 | 拉取 Web 会话到终端 |
| `/desktop` | 内置 | 转到 Claude Code Desktop 应用 |
| `/web-setup` | 内置 | 连接 GitHub 到 Claude Code Web |
| `/install-github-app` | 内置 | 安装 Claude GitHub Actions |
| `/install-slack-app` | 内置 | 安装 Claude Slack App |
| `/mobile` | 内置 | 显示移动端下载二维码 |

## 其他

| 命令 | 类型 | 功能 |
|---|---|---|
| `/btw <question>` | 内置 | 快速旁问题（不增加对话历史） |
| `/sandbox` | 内置 | 切换沙盒模式 |
| `/powerup` | 内置 | 交互式功能探索课程 |
| `/stickers` | 内置 | 订购 Claude Code 贴纸 |
| `/radio` | 内置 | 打开 Claude FM lo-fi 电台 |
| `/passes` | 内置 | 分享免费试用周 |
| `/privacy-settings` | 内置 | 隐私设置 |
| `/upgrade` | 内置 | 升级订阅计划 |
| `/team-onboarding` | 内置 | 生成团队上手指南 |
| `/voice [hold\|tap\|off]` | 内置 | 语音输入切换 |

---

## 命令分类速查

```
SESSION   /clear /compact /context /resume /branch /background /stop /rename /rewind /recap /export /copy
MODEL     /model /effort /fast /plan /ultraplan /goal /exit
REVIEW    /code-review /simplify /review /security-review /diff /ultrareview
RUN       /run /verify /run-skill-generator
CONFIG    /init /config /permissions /memory /add-dir /mcp /agents /skills /hooks /ide
          /plugin /reload-skills /reload-plugins /keybindings /statusline /theme /color
          /scroll-speed /focus /tui /terminal-setup /update-config /fewer-permission-prompts
AUTOMATE  /batch /loop /autofix-pr /schedule /tasks /workflows
DIAGNOSE  /doctor /debug /usage /usage-credits /insights /heapdump /help /release-notes /feedback /status
RESEARCH  /deep-research /claude-api
CONNECT   /login /logout /setup-bedrock /setup-vertex /chrome /remote-control /remote-env
          /teleport /desktop /web-setup /install-github-app /install-slack-app /mobile
MISC      /btw /sandbox /powerup /stickers /radio /passes /privacy-settings /upgrade
          /team-onboarding /voice
```

## 类型说明

| 类型 | 含义 | 存放位置 |
|---|---|---|
| **内置** | 硬编码在 Claude Code 二进制中的命令 | CLI 二进制 |
| **Bundled Skill** | 打包在二进制中的 SKILL.md，运行时按需解压 | 二进制 → `/tmp/claude-<UID>/bundled-skills/` |
| **Bundled Workflow** | 打包在二进制中的多 agent 工作流 | 二进制 → 运行时解压 |

三者对用户无区别，都通过 `/` 调用。Bundled Skill 和自定义 Skill（`.claude/skills/`）机制完全相同。

## 统计

| 分类 | 数量 |
|---|---|
| 硬编码内置命令 | ~65 |
| Bundled Skill | ~12 |
| Bundled Workflow | 1 |
| **合计** | **~78** |

## 命令发布时间线

| 时间 | 引入命令 |
|---|---|
| 2025.02 (v0.2.x) | `/help` `/clear` `/config` `/init` `/compact` |
| 2025.04 (v0.2.30+) | `/mcp` `/permissions` `/add-dir` |
| 2025.05 (v1.0.0) | `/review` `/context` `/model` `/rename` `/branch` `/diff` `/doctor` |
| 2025.06 (v1.0.17+) | `/agents` `/tasks` |
| 2025.07-08 (v1.0.28+) | `/background` `/statusline` `/feedback` `/sandbox` **`/security-review`** |
| 2025.09 (v2.0.0) | `/usage` `/export` `/release-notes` |
| 2025.10 (v2.0.20+) | `/skills` `/plugin` `/theme` `/login` |
| 2025.11 (v2.0.51) | `/effort` `/insights` `/memory` |
| 2026.01 (v2.1.0) | **`/plan`** **`/keybindings`** |
| 2026.02 (v2.1.63) | **`/batch`** **`/simplify`** |
| 2026.04 (v2.1.108+) | `/recap` **`/fewer-permission-prompts`** `/ultrareview` |
| 2026.05 (v2.1.139+) | **`/goal`** `/scroll-speed` **`/run`** **`/verify`** **`/code-review`** `/reload-skills` **`/workflows`** |
| 2026.06 (v2.1.160) | `/effort`（新增 `ultracode` 级别） |
