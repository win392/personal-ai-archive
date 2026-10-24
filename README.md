# Personal AI Archive · 个人 AI 记忆档案

> 一个仓库，所有 AI 都能读；一次维护，全平台复用。

## 这是什么

本仓库是我的**跨 AI、跨设备个人记忆系统**。任何支持联网或文件读取的 AI（ChatGPT / Claude / Gemini / 本地 Agent）都能从这里读取我的身份、习惯、偏好与历史经验，在不同平台之间保持一致的理解，不必每次重新自我介绍。

设计约束：纯 Markdown、无私有格式、无构建步骤，任何编辑器或 AI 都能直接读改。

## 目录结构

| 目录 | 作用 | 读取优先级 |
| --- | --- | --- |
| identity/ | 我是谁：身份、职业、核心标签、目标 | P0 |
| workflow/ | 我怎么工作：习惯、工具、沟通风格、优先级规则 | P0 |
| memory/ | 我经历过什么：经验、决策记录、AI 交互偏好 | P1 |
| skills/ | 我会什么、要学什么、缺什么 | P1 |
| archive/ | 历史项目、旧文档、已完成任务索引 | P2 |

## AI 接入（30 秒版）

按以下顺序喂给 AI，先 P0 后 P1：

    1. identity/profile.md       我 是谁
    2. workflow/communication.md 我 要你怎么说话
    3. workflow/priority-rules.md 我 怎么排优先级
    4. identity/goals.md         我 要去哪
    5. memory/preferences.md     我 不喜欢什么

三种方式任选：

- **粘贴链接**（最省事）：把 raw 地址发给 AI，例如
  https://raw.githubusercontent.com/win392/personal-ai-archive/main/identity/profile.md
- **API 读取**（Agent 用）：见 ai-integration.md 的接口示例
- **克隆到本地**（离线用）：git clone https://github.com/win392/personal-ai-archive.git

## 文件标签约定

每个文件第一行是 AI 定位标签，决定 AI 的写入权限：

- `# AI-READONLY: <主题>` — 核心事实，AI 只能读；修改必须我本人操作
- `# AI-WRITABLE: <主题>` — AI 可以在这里追加内容（只能追加，不覆盖）

## 版本与回退

所有修改都是 Git 提交，天然可回退。查看历史：

    git log --oneline --graph

回退整个仓库到某个版本：

    git revert <commit-sha>        # 推荐：生成一个反向提交，不改历史
    git reset --hard <commit-sha>  # 仅本地，随后 force push（main 已开启保护，会被拒绝）

只回退单个文件：

    git checkout <commit-sha> -- memory/lessons.md

## 维护约定

- **提交信息格式**：`[模块] 动作 + 对象`，例如 `[identity] 更新职业为工艺工程师`
- **每周复盘**：花 5 分钟把本周的新经验补进 memory/lessons.md
- **冲突处理**：AI 与本人同时修改时，以本人手动提交为准
- **不做的事**：不放大段二进制、不放密钥与密码、不放他人隐私

## 安全提示

本仓库是**公开**的。请只写"愿意公开"的信息：不要填身份证号、手机号、家庭住址、公司内部未公开数据、他人姓名与联系方式。需要放敏感内容时，改用私有仓库或本地加密副本。

## 相关文件

- [ai-integration.md](ai-integration.md) — 各平台接入方式与自动更新规则
- [SETUP-REPORT.md](SETUP-REPORT.md) — 搭建完成报告
- [CHANGELOG.md](CHANGELOG.md) — 档案结构变更日志
