## 问题
多技术栈团队定位慢查询、N+1、隐式事务等需依赖各自框架工具，信息分散。

## 洞察
ORM/驱动层存在可拦截点，统一抽取并标准化结构后可集中分析。

## 概念
多 ORM Hook → 本地聚合器 → 标准化事件行 `{ts, orm, framework, db_type, sql, params, duration_ms, rows, callsite}` → 面板按耗时/频率/重复度排序。支持采样与慢查询阈值。

## 影响
降低性能问题定位时间；减少跨语言协作沟通成本；促进查询治理。

## 可行性
主流 ORM 提供 listener/interceptor；初期支持 MySQL/PostgreSQL/SQLite/SQLServer；采样 + 阈值 控制开销。风险：参数泄露 / 性能影响。

## 演化
- P1: Node/Java/Python 最小 Hook
- P2: 面板与过滤
- P3: 采样与慢查询告警
- P4: N+1 模式检测
- P5: 基准 / 压测差异报告

## 风险
`orm-compat`, `overhead`, `security`

## 下一步
列出 ORM + DB 矩阵与 Hook 方式。

来源文件: `ideas/2025-10-24-cross-platform-sql-capture.md`