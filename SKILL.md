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
3. 按项目状态选择最低基线；见 references/project-baseline.md。状态只决定必须做什么，不直接决定技术栈。
4. 按交付形态选择分支模型；见 references/lifecycle.md。部署、分发和数据关键不是同一件事。
5. 对每个高成本组件写清 **消费者 / 触发信号 / 退出或降级条件**；见 references/component-triggers.md。
6. 测试是风险控制，不是默认交付物；日常不新增测试、不跑全量套件，按 references/testing.md 处理复现和收尾。
7. 日常改动按 references/daily-development.md；代码、协作、运行、数据、交付或依赖规模变化时，按 references/scaling.md 升级或降级。
8. 新增文档前先搜索现有文档，优先更新或合并；文档必须有读者和生命周期，见 references/documentation.md。
9. 长线服务/应用在进入长期运营前定义性能预算；CI 一次构建、复用产物，见 references/performance-and-ci.md。
10. 交付前按 references/version-finish.md 执行版本收尾；版本收尾本身不授权发布。
11. 分开记录本地检查、CI、部署、分发和真实环境验收；一层通过不能替代另一层。
12. 版本收尾时复核定位卡、组件清单、文档和数据恢复路径；删除没有消费者的内容。
13. 需要校准判定时，读 references/portfolio-examples.md，不要把案例当成必须复制的模板。

## 硬边界

- 数据越不可恢复，备份、迁移前检查和恢复验证越重要；这与数据库品牌无关。
- 不为假想的旧客户端、旧数据或旧版本增加兼容层；只兼容真实存在的对象。
- 不把“外部用户”“常驻服务”“数据重要”直接等同于重型基础设施。
- 修改、提交、推送、部署、发布分别按用户授权执行；规范本身不授予这些动作。
- 保留用户已有改动；不要为了让规范整齐而重写已经工作的项目。
- 项目仍是脚手架或已冷冻时，不套用完整流程。
- build 与 CI 按交付需要存在；没有构建产物或共享部署时，不强迫补一层不存在的流程。

## 参考

- 定位卡与四维判据：references/project-profile.md
- 各状态最低基线：references/project-baseline.md
- 生命周期、分支与交付边界：references/lifecycle.md
- 日常开发规范：references/daily-development.md
- 规模升级与降级：references/scaling.md
- 文档规范与预算：references/documentation.md
- 性能与 CI/打包：references/performance-and-ci.md
- 测试策略与预算：references/testing.md
- 版本收尾与交付检查：references/version-finish.md
- 组件触发与退出条件：references/component-triggers.md
- 组合校准案例：references/portfolio-examples.md
