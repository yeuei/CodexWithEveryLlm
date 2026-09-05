# CodexWithEveryLlm

让人类用户、ChatGPT Web 和本地 Agent 通过 GitHub 安全地协作交接。

## 这是什么

这是一个总仓库，负责说明各组件如何组合，以及怎样从一次交接项目开始使用。它本身不复制各组件的全部实现，而是提供统一入口、版本组合和使用文档。

## 给人类用户

1. 先阅读 [用户指南](docs/用户指南.md)，了解一次交接如何开始。
2. 按 [快速开始](docs/快速开始.md) 创建或选择交接仓库。
3. 在 Dashboard 中确认仓库、项目、PR 和绑定的对话。
4. 需要排查时查看 [工作原理](docs/工作原理.md)。

完整安装、启动和一次配对步骤见 [快速开始](docs/快速开始.md)。运行时不会把 token、浏览器 profile 或本机命令写入本仓库。

## 给 Agent 和开发者

组件职责、协议、路由绑定和发布方式见 [组件与版本](docs/组件与版本.md) 和 [开发者指南](docs/开发者指南.md)。

### 三条真实入口

- 总仓库（当前页面）：用户入口、架构、文档和组合版本。
- [Local Agent skill 调度说明](docs/开发者指南.md#dashboard-调度)：从 [yeuei/agent-github-project-executor-skills](https://github.com/yeuei/agent-github-project-executor-skills) 安装；该仓库承载 Local Agent skill 与 Dashboard 部署子能力。
- [真实交接项目](https://github.com/yeuei/gpt---github---codex) 与 [协议模板](https://github.com/yeuei/template_chatgpt_github_codex)：分别保存运行事实和通用协议。

## 组件关系

| 组件 | 职责 | 维护方式 |
| --- | --- | --- |
| Local Agent skill | 执行本地任务，并调度 Dashboard | [skill 说明](docs/开发者指南.md#dashboard-调度) |
| GitHub handoff project | 保存事件、PR、任务历史和 Dashboard runtime | [yeuei/gpt---github---codex](https://github.com/yeuei/gpt---github---codex) |
| Protocol template | 提供通用任务、报告和绑定协议模板 | [yeuei/template_chatgpt_github_codex](https://github.com/yeuei/template_chatgpt_github_codex) |
| 本总仓库 | 面向用户的入口、架构说明和版本组合 | 本仓库 |

三个组件继续独立发布；本仓库用版本清单和链接组合它们，不使用 git submodule。这样用户可以直接阅读和安装，组件也不会产生重复副本。

一次配对的最短路径是：ChatGPT Web 为真实仓库/分支/PR 创建一次性邀请 → Local Agent 核对并 claim → 返回 confirm token 完成 active 绑定 → Dashboard 只消费该 route 的事件。任何目标不匹配、过期或竞争绑定都进入人工处理。

## 当前状态

本仓库当前用于建立总入口和文档结构。正式发布时，请在 [组件与版本](docs/组件与版本.md) 中填写各组件的稳定 tag 或 commit，并在发布说明中记录兼容组合。
