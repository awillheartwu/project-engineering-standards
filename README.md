# Project Engineering Standards

给个人项目和 Codex agent 使用的一套工程决策规范：先判断项目的责任、运行、数据和协作形态，再决定是否需要数据库、队列、服务拆分、CI、测试、发布和运维。它不是技术栈模板，也不是“所有项目都必须做”的清单。

主要读者是维护这套规范的用户和 Codex agent，不是某个终端产品的用户。具体项目应按自己的主要读者调整 README 的重点。

## 为什么存在

AI 辅助开发很容易把“更多组件、更多测试、更多文档”当成更专业。这个仓库的方向相反：用真实消费者和触发条件约束复杂度。

- 责任与基础设施是两条独立轴。
- 默认一个仓库、一个可运行进程、SQLite 或本地文件。
- 高成本组件必须有消费者、触发和退出条件。
- 测试、清理、文档和验收围绕版本收尾，而不是每天堆。
- 人工验收通过后再合 main；自动部署时，合 main 就是生产变更。

## 快速开始

先读 [SKILL.md](SKILL.md)，按场景选择入口。

### 新项目

1. 填 [项目定位卡](references/project-profile.md)。
2. 用 [状态基线](references/project-baseline.md) 确定最低要求。
3. 用 [组件触发器](references/component-triggers.md) 判断是否需要数据库、队列或服务拆分。
4. 有正式交付时读 [生命周期](references/lifecycle.md)。

### 已有项目

1. 按 [项目落地与存量审计](references/adoption.md) 做只读审计。
2. 填写定位卡，记录错配、例外和下一次复核条件。
3. 只在自然重构点收敛，不为了整齐重写。

### 日常、收尾与运行

| 场景 | 入口 |
| --- | --- |
| 日常改动 | [日常开发](references/daily-development.md)、[规模升降级](references/scaling.md) |
| 测试与文档 | [测试策略](references/testing.md)、[文档规范](references/documentation.md) |
| 版本收尾 | [收尾流程](references/version-finish.md)、[性能与 CI](references/performance-and-ci.md) |
| 运行与事故 | [安全与恢复](references/operations.md) |

## 参考地图

| 主题 | 文件 |
| --- | --- |
| 项目定位与状态 | [project-profile.md](references/project-profile.md)、[project-baseline.md](references/project-baseline.md) |
| 组件与交付 | [component-triggers.md](references/component-triggers.md)、[lifecycle.md](references/lifecycle.md) |
| 日常与规模 | [daily-development.md](references/daily-development.md)、[scaling.md](references/scaling.md) |
| 测试与文档 | [testing.md](references/testing.md)、[documentation.md](references/documentation.md) |
| 收尾与运行 | [version-finish.md](references/version-finish.md)、[performance-and-ci.md](references/performance-and-ci.md)、[operations.md](references/operations.md) |
| 落地与案例 | [adoption.md](references/adoption.md)、[portfolio-examples.md](references/portfolio-examples.md) |

## 当前状态

- 状态：active，持续维护。
- 本仓库定位卡：[PROJECT_PROFILE.md](PROJECT_PROFILE.md)。
- 项目索引：[portfolio.md](portfolio.md)。
- 当前没有运行时、数据库、队列、构建或 CI；这是按交付形态裁剪的结果，不是缺失。
- 当前只有本地 Git 历史，尚无远端或 NAS 备份；安装为 Codex skill 也尚未完成。

## 维护

- 只有 main 分支；变更按 Conventional Commits 提交。
- 修改规则时同步检查 SKILL.md、相关 reference 和 README 的入口，避免同一事实多处漂移。
- 新增文档前先搜索现有文档；优先更新、合并或链接。
- 不把临时分析、任务总结或一次性报告放进仓库。
