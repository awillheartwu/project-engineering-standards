---
name: project-engineering-standards
description: "Choose a project's engineering baseline by responsibility, runtime, data, and collaboration, then apply explicit triggers for databases, queues, services, CI, deployment, tests, documentation, security, compatibility, and pre-commit/pre-push privacy checks. Use for new projects, existing-project audits, daily development, version finish, and production operations."
metadata:
  short-description: "Project engineering by risk and real triggers"
---

# Project Engineering Standards

这套规范按项目风险选择工程基线，不是成熟度评级。核心判断：**责任与基础设施是两条独立轴**；外部用户、常驻运行或数据重要，不自动推出 Postgres、Redis、队列或服务拆分。

## 按场景选择

| 场景 | 先读 | 产出 |
| --- | --- | --- |
| **新项目** | [定位卡](references/project-profile.md)、[状态基线](references/project-baseline.md)、[生命周期](references/lifecycle.md)、[组件触发器](references/component-triggers.md) | 定位卡、最低基线、组件清单 |
| **存量项目审计** | [落地与审计](references/adoption.md)、[组合案例](references/portfolio-examples.md) | 当前状态、错配、例外、下一动作 |
| **日常改动** | [日常开发](references/daily-development.md)、[规模升降级](references/scaling.md)、[测试](references/testing.md)、[文档](references/documentation.md) | 局部改动、相关检查、证据 |
| **版本收尾** | [收尾流程](references/version-finish.md)、[测试](references/testing.md)、[文档](references/documentation.md)、[性能与 CI](references/performance-and-ci.md) | 清理、验收、合 main、交付 |
| **提交、推送或分发** | [隐私检查](references/operations.md#提交与推送前的隐私检查) | 检查范围、结果、阻塞项 |
| **运行与事故** | [安全与恢复](references/operations.md)、[性能与 CI](references/performance-and-ci.md) | 安全、备份、恢复、告警 |
| **判定校准** | [组合案例](references/portfolio-examples.md) | 对照案例，不照抄 |

## 核心规则

1. 先确认状态（scaffold / prototype / active / frozen）和四维（责任 / 运行 / 数据 / 协作），不先选技术栈。
2. 默认最小：一个仓库、一个可运行进程、SQLite 或本地文件；只有真实消费者才加数据库、队列、服务拆分或 CI。
3. 高成本组件写清 **消费者 / 触发 / 退出条件**；没有消费者就删除或冻结。
4. 测试是风险控制：日常不新增测试、不跑全量套件；收尾集中整理，只有数据、安全或高危 bug 做最小例外。
5. build 和 CI 按交付需要存在：有产物才构建，有共享或部署才上 CI；构建一次并复用产物。
6. 文档先搜索再新建，每份有读者和生命周期；清理文档、测试、空文件、空函数和孤儿代码是收尾的独立阶段。
7. 人工验收通过后再合 main；main 自动部署时，合 main 即部署，必须先授权。
8. 数据越不可恢复，备份与恢复越重要；D1/D2 必须有可执行的恢复路径。
9. 保留用户改动；修改、提交、推送、部署、发布分别授权；不为了规范重写已经工作的项目。
10. 性能与安全按需升级：长线运营先建性能预算；公网或分发项目做基本安全和恢复，不搞企业级体系。
11. 提交前检查暂存内容；推送前检查候选文件树、待推送历史和实际分发产物。按[隐私检查](references/operations.md#提交与推送前的隐私检查)处理个人信息、凭据、真实 IP 和机器路径；历史提交含敏感信息时，必须清除受污染的历史版本并复查，不能只删当前内容后继续推送。检查通过不等于获得提交、推送或发布授权。

## 何时停

- 脚手架或冷冻项目不套完整流程。
- 没有真实消费者、没有预算或没有交付，不提前引入重型组件。
- 事实不足时先只读审计，不直接重构。
