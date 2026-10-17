---
name: project-engineering-standards
description: "Profile a project's responsibility, runtime, data, and collaboration before setting its engineering baseline, then add databases, queues, services, CI, deployment, tests, or compatibility only when a real trigger exists. Use for new project setup, stack or architecture decisions, project reviews, and version-finish planning."
metadata:
  short-description: "Set project engineering by risk and real triggers"
---

# Project Engineering Standards

这套规范是一个决策工具，不是成熟度评级。核心判断：**责任与基础设施是两条独立轴**。外部用户、24 小时运行或数据重要，都不能单独证明需要 Postgres、Redis、队列或服务拆分。

## 先确认

在讨论技术栈之前，先填写 references/project-profile.md 的定位卡。至少确认：

1. **项目状态**：scaffold、prototype、active、frozen。
2. **责任面**：失败会造成什么后果。
3. **运行面**：单次、单机常驻、多实例。
4. **数据面**：可重建、需备份、强一致多写。
5. **协作面**：个人、小团队、公开协作。

scaffold 只定义目标、数据边界和下一次验证；不要先建数据库、队列、CI 或发布流水线。frozen 只保留运行、备份和恢复路径。

## 决策流程

1. 写定位卡，不先选工具。
2. 从最小基线开始：一个仓库、一个可部署进程、SQLite 或本地文件、一条 CI；只有真实消费者才升级。
3. 对每个高成本组件写清 **消费者 / 触发信号 / 退出或降级条件**；见 references/component-triggers.md。
4. 分开记录本地检查、CI、部署和真实环境验收；一层通过不能替代另一层。
5. 版本收尾时复核定位卡、组件清单和数据恢复路径；删除没有消费者的组件。
6. 需要校准判定时，读 references/portfolio-examples.md，不要把案例当成必须复制的模板。

## 硬边界

- 数据越不可恢复，备份、迁移前检查和恢复验证越重要；这与数据库品牌无关。
- 不为假想的旧客户端、旧数据或旧版本增加兼容层；只兼容真实存在的对象。
- 不把“外部用户”“常驻服务”“数据重要”直接等同于重型基础设施。
- 修改、提交、推送、部署、发布分别按用户授权执行；规范本身不授予这些动作。
- 保留用户已有改动；不要为了让规范整齐而重写已经工作的项目。
- 项目仍是脚手架或已冷冻时，不套用完整流程。

## 参考

- 定位卡与四维判据：references/project-profile.md
- 组件触发与退出条件：references/component-triggers.md
- 组合校准案例：references/portfolio-examples.md
