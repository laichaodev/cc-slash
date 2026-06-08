---
name: cc-slash
description: 当用户在手动做某件事而内置斜杠命令可以直接完成时，或者用户问"怎么..."时，推荐对应的命令。也可通过 /cc-slash 按场景浏览命令。
---

# 斜杠命令速查

**核心规则：** 当用户描述某个任务时，先判断是否有内置斜杠命令可以直接完成。有就推荐，命令更快、更可靠，通常有快捷键。

## 场景匹配：用户说什么 → 推荐什么命令

### 会话管理
| 用户说... | 推荐命令 | 原因 |
|---|---|---|
| "上下文太长了"、"token 不够了" | **`/compact`** | 压缩历史，释放上下文窗口 |
| "看看 token 用量"、"还剩多少上下文" | **`/context`** | 可视化上下文消耗 |
| "开个新对话"、"重置" | **`/clear`** | 清空上下文，旧会话保留在 `/resume` |
| "回到那个会话"、"继续昨天的" | **`/resume`** | 会话选择器，支持搜索 |
| "分支这个对话"、"换个思路试试" | **`/branch`** | 分叉会话 |
| "派生一个后台子任务"、"交给子 agent 继续做" | **`/fork <指令>`** | 派生后台子 agent，继承对话处理任务 |
| "后台运行"、"我去干别的你继续" | **`/background`** | 转为后台 agent |
| "给这个会话改个名" | **`/rename`** | 重命名会话 |
| "回退到改之前" | **`/rewind`** | 回退到检查点 |
| "导出对话" | **`/export`** | 纯文本导出 |
| "复制上个回复" | **`/copy`** | 复制到剪贴板 |

### 模型与推理
| 用户说... | 推荐命令 | 原因 |
|---|---|---|
| "换模型"、"用 Opus"、"切到 Sonnet" | **`/model`** | 交互选模型，`s`=仅当前，`d`=全局默认 |
| "多想想"、"认真点"、"给多点算力" | **`/effort high`** | 调节推理深度 |
| "快点"、"加速" | **`/fast on`** 或 **`/effort low`** | 快速模式或低力度 |
| "先设计方案再写代码" | **`/plan`** | 计划模式 — 先设计，通过后再实现 |
| "让它自己搞定"、"一直做到完成" | **`/goal`** | 设定完成条件，Claude 自动跨轮次工作 |

### 代码审查
| 用户说... | 推荐命令 | 原因 |
|---|---|---|
| "审查我的改动有没有 bug" | **`/code-review`** | 正确性 + 清理审查 |
| "审查完自动修复" | **`/code-review --fix`** | 直接应用到工作区 |
| "只做清理优化，不查 bug" | **`/simplify`** | 只做复用/简化/效率优化 |
| "把审查意见贴到 PR 上" | **`/code-review --comment`** | 行内 PR 评论 |
| "深度云审查" | **`/code-review ultra`** | 多 agent 云端审查 |
| "审查这个 PR" | **`/review <PR>`** | 本地 PR 审查 |
| "安全审计"、"有没有漏洞" | **`/security-review`** | 扫描 diff 安全漏洞 |
| "看看改了什么" | **`/diff`** | 交互式 diff（j/k 翻页） |

### 运行验证
| 用户说... | 推荐命令 | 原因 |
|---|---|---|
| "能跑起来吗"、"启动一下" | **`/run`** | 启动并驱动项目应用 |
| "验证这个修复"、"确认改对了" | **`/verify`** | 构建→运行→观察 |
| "教 Claude 怎么跑这个项目" | **`/run-skill-generator`** | 生成项目专属运行 skill |

### 项目配置
| 用户说... | 推荐命令 | 原因 |
|---|---|---|
| "初始化项目" | **`/init`** | 生成 CLAUDE.md |
| "改权限"、"允许这个工具" | **`/permissions`** | 管理 allow/ask/deny 规则 |
| "添加权限"、"允许 npm 命令" | **`/update-config`** | 直接编辑 settings.json |
| "减少权限弹窗" | **`/fewer-permission-prompts`** | 扫描日志，自动添加 allowlist |
| "加个工作目录" | **`/add-dir`** | 添加额外目录 |
| "配置 MCP 服务器" | **`/mcp`** | MCP 管理 |
| "管理子 agent" | **`/agents`** | Agent 配置 |
| "安装插件" | **`/plugin`** | 插件管理 |
| "添加新 skill"、"自定义命令" | 写 `.claude/skills/<name>/SKILL.md` | 不是斜杠命令，是写文件 |
| "换主题"、"深色模式" | **`/theme`** | 主题选择器 |
| "改快捷键" | **`/keybindings`** | 打开 keybindings.json |
| "配置状态栏" | **`/statusline`** | 状态栏设置 |
| "配置终端快捷键" | **`/terminal-setup`** | Shift+Enter 等 |

### 自动化与批量
| 用户说... | 推荐命令 | 原因 |
|---|---|---|
| "全项目把 X 改成 Y" | **`/batch`** | 并行分拆到独立 worktree，各自提 PR |
| "每 5 分钟跑一次" | **`/loop 5m <prompt>`**（或 `/proactive`） | 定时重复执行 |
| "盯着我的 PR，CI 挂了自动修" | **`/autofix-pr`** | 监听 PR，失败自修 |
| "创建云端定时任务" | **`/schedule`** | 云端管理 routine |

### 研究
| 用户说... | 推荐命令 | 原因 |
|---|---|---|
| "深入研究这个"、"多源搜索" | **`/deep-research <question>`** | 多源搜索→交叉验证→生成引用报告 |
| "写个 Claude API 应用" | **`/claude-api`** | SDK 参考、模型迁移、managed agent |

### 诊断
| 用户说... | 推荐命令 | 原因 |
|---|---|---|
| "出了问题"、"诊断一下" | **`/doctor`** | 安装和配置审计（`f` 自动修） |
| "调试这个会话"、"怎么回事" | **`/debug`** | 会话调试日志 |
| "花了多少钱" | **`/usage`** | 费用和用量明细 |
| "报告 bug" | **`/feedback`** | 提交反馈（含会话上下文） |
| "看看版本"、"是不是最新的" | **`/status`** | 版本/模型/账号/连接状态 |
| "更新日志"、"有什么新功能" | **`/release-notes`** | 交互式 changelog |

### 快捷操作
| 用户说... | 推荐命令 | 原因 |
|---|---|---|
| "顺便问一下"、"旁注" | **`/btw <question>`** | 旁问题，不写入历史 |
| "回到那个后台会话" | **`/resume`**（找 `bg` 标记） | 后台会话标了 `bg` |
| "从 Web 端回到终端" | **`/teleport`** | 拉 Web 会话到本地 |
| "在手机上继续" | **`/remote-control`** | 远程控制，从 claude.ai 连 |

## 回复模式

当你发现用户在做的事有对应的斜杠命令时：

1. **一句话提醒**：💡 试试 `/xxx` — 它可以直接 [干什么]。
2. **不阻拦**：用户想手动做就继续。
3. **只说一次**：同一个建议不重复。

如果用户问"怎么..."或"有没有命令可以..."，直接从上面表格回答。

## 按分类速查（`/cc-slash` 浏览用）

```
会话    /clear /compact /context /resume /branch /fork /background /stop /rename /rewind /recap /export /copy
模型    /model /effort /fast /plan /ultraplan /goal /exit
审查    /code-review /simplify /review /security-review /diff /ultrareview
运行    /run /verify /run-skill-generator
配置    /init /config /permissions /memory /add-dir /mcp /agents /skills /hooks /ide
        /plugin /reload-skills /reload-plugins /keybindings /statusline /theme /color
        /scroll-speed /focus /tui /terminal-setup /update-config /fewer-permission-prompts
自动化  /batch /loop /autofix-pr /schedule /tasks /workflows
诊断    /doctor /debug /usage /usage-credits /insights /heapdump /help /release-notes /feedback /status
研究    /deep-research /claude-api
连接    /login /logout /setup-bedrock /setup-vertex /chrome /remote-control /remote-env
        /teleport /desktop /web-setup /install-github-app /install-slack-app /mobile
其它    /btw /sandbox /powerup /stickers /radio /passes /privacy-settings /upgrade
        /team-onboarding /voice
```
