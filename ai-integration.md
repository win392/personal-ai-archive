# AI-READONLY: 跨 AI 平台接入配置

> 本文件说明如何把本仓库接入各类 AI，以及 AI 自动更新档案的规则。
> 平台功能会变，具体菜单以平台当前版本为准；下面给的是稳定可行的通用路径。

## 一、核心原理

本仓库是纯 Markdown 的公开 Git 仓库，因此有三种通用读取方式：

1. **raw 直链**：`https://raw.githubusercontent.com/win392/personal-ai-archive/main/<路径>`
2. **GitHub API**：`https://api.github.com/repos/win392/personal-ai-archive/contents/<路径>`
3. **整体克隆 / 打包下载**：`https://github.com/win392/personal-ai-archive/archive/refs/heads/main.zip`

任何"能联网读网页"或"能上传文件"的 AI 都能用这三种方式之一。

## 二、按平台接入

### ChatGPT

- **Custom GPT / Project**：在知识库中上传本仓库文件，或把 raw 链接贴进说明
- **普通对话**：直接粘贴偏好文件（memory/preferences.md + workflow/communication.md）内容
- **数据用途**：让它在长任务开始前先读这两份文件，输出风格立刻对齐

### Claude

- **Projects**：新建项目，上传 identity/ 与 workflow/ 的文件作为项目知识
- **对话**：粘贴 raw 链接（Claude 可联网时直接读取）
- **提示词**：项目说明里写"先读 communication.md 再回答"

### Gemini

- **Gem（自定义 Gem）**：把模板文件上传为参考文件，或在指令里放 raw 链接
- **NotebookLM**：把仓库文件作为来源，用于检索式问答

### API / Agent 接入（通用）

用 GitHub Contents API 读取，示例：

    curl -H "Authorization: Bearer $GITHUB_TOKEN" \
         -H "Accept: application/vnd.github+json" \
         https://api.github.com/repos/win392/personal-ai-archive/contents/identity/profile.md

未认证也可读公开仓库（每小时 60 次限流）；认证后 5000 次/小时。

写入则用：

    PUT /repos/win392/personal-ai-archive/contents/<路径>
    body: { message, content(base64), sha(更新时必填), branch }

### 各类 Agent 平台（Meta Muse、OpenAI Dots 等）

这类平台通常提供两种扩展点：**自定义工具（function calling）** 或 **MCP 服务器**。通用接法：

1. 在平台里注册一个 `read_archive` 工具：入参 path，出参文件文本（内部调 Contents API 的 raw 模式）
2. 再注册一个 `append_archive` 工具：入参 path + 追加内容，内部调 PUT contents
3. 在系统提示里写：任务开始先调 `read_archive('workflow/communication.md')`

> 注：具体平台是否已开放公开 API，以其官方文档为准；本文件给的是不依赖特定平台的实现路径。

## 三、自动更新规则（AI 写完往哪存）

| 场景 | 写入文件 | 方式 |
| --- | --- | --- |
| 完成一个项目 | memory/lessons.md、archive/index.md | 追加 |
| 做了一个重要决定 | memory/decisions.md | 追加 |
| 发现我新的表达偏好 | memory/preferences.md | 追加 |
| 学会/用熟了新技能 | skills/skills.md | 追加 |
| 我换了岗位/目标 | identity/ 下对应文件 | **仅本人改** |

硬性约束：

- `# AI-READONLY` 文件一律不写，除非我明确说"可以改"
- 只追加到记录区末尾，不重写历史条目
- 每次写入必须带日期与来源（哪个 AI、什么任务）
- 一次提交只做一件事，commit message 用 `[模块] 动作 + 对象`

## 四、权限与安全

- 给 AI 用的 token 用 **fine-grained PAT**，只授权本仓库，权限只要 `Contents: Read and write`，有效期设 30–90 天
- 不要把 token 写进仓库、写进提示词长期保存
- 公开仓库里不要写入敏感个人信息（详见 README 安全提示）
- 建议定期检查提交历史，发现异常提交立即 revert

## 五、快速自检

接入后问 AI 三个问题，答对说明读取成功：

1. 我的职业是什么？（应能从 identity/profile.md 答出）
2. 我应该用多长的回答？（communication.md）
3. 遇到安全风险的事你会怎么做？（preferences.md）
