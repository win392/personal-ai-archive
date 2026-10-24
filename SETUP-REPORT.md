# 搭建完成报告

## 仓库

- 地址：https://github.com/win392/personal-ai-archive
- 可见性：公开
- 默认分支：main
- 结构：5 个核心目录 + 23 个 Markdown 文件

## 目录说明

| 目录 | 放什么 | 谁维护 |
| --- | --- | --- |
| identity/ | 身份、职业、标签、目标 | 本人（AI 只读） |
| workflow/ | 沟通风格、习惯、工具、优先级规则 | 本人，AI 可追加 |
| memory/ | 决策记录、经验教训、交互偏好 | AI 可追加，本人复核 |
| skills/ | 已掌握技能、学习计划、能力缺口 | 本人，AI 可追加 |
| archive/ | 历史项目索引 | AI 可追加 |

## AI 接入快速指南

1. 新平台第一次对话，发送这条：

       请先读取以下文件，再回答我的问题：
       https://raw.githubusercontent.com/win392/personal-ai-archive/main/identity/profile.md
       https://raw.githubusercontent.com/win392/personal-ai-archive/main/workflow/communication.md
       https://raw.githubusercontent.com/win392/personal-ai-archive/main/memory/preferences.md

2. 需要它写回时，给它一个只有本仓库 Contents 写权限的 fine-grained PAT
3. 定期看 https://github.com/win392/personal-ai-archive/commits/main 确认没有乱改

## 版本回退

    git log --oneline --graph          # 找到目标提交
    git revert <commit-sha>            # 生成反向提交（保留历史，推荐）

## 下一步建议

1. 先填 identity/profile.md 与 workflow/communication.md（这两份收益最大）
2. 一周后再补 memory/lessons.md，避免一开始就想写全
3. 敏感信息不要放进公开仓库
