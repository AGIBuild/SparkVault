---
title: "跨平台 SQL 抓取工具"
slug: "cross-platform-sql-capture"
date: 2025-10-24
author: ""
status: draft
tags: [tool-dev]
impact_hypothesis: "统一抓取与分析主流 ORM 生成的实时 SQL 可降低 20% 以上性能诊断时间。"
scores: {impact: null, feasibility: null, novelty: null, urgency: null, alignment: null}
risk_flags: ["orm-compat", "overhead", "security"]
next_step: "列出现有 ORM + 数据库矩阵与最小可行 hook 方式。"
issue: 2
---

# 跨平台 SQL 抓取工具
捕获主流 ORM 在运行期生成并实际执行的 SQL，聚合展示与分析，支持多数据库类型。

## 问题
多技术栈团队在定位慢查询、冗余 N+1、隐式事务等问题时，需要分别在不同语言/框架中使用各自工具，碎片化且难以统一审计。

## 洞察
ORM 层或驱动层存在可拦截点（事件/中间件/代理），统一抽取后标准化输出结构（SQL + 参数 + 源模型/调用栈），可跨语言集中分析。

## 概念
提供轻量探针库或代理：
- 针对每类 ORM 提供最小 Hook（如中间件、listener、拦截器、插件）。
- 将捕获信息发送到本地聚合器（或轻量代理服务）。
- 聚合器统一格式：{timestamp, orm, framework, db_type, sql, params, duration_ms, rows, callsite}。
- 前端简洁面板：按耗时、频率、重复度、潜在风险（N+1）标记。

## 潜在影响
- 加速性能与查询问题定位（统一视图）。
- 降低多语言团队认知成本。
- 促进治理：基于统计数据设定慢查询基线与告警。

## 可行性
- ORM Hook：较多已提供事件接口（Hibernate、TypeORM、Sequelize、ActiveRecord、Django ORM、SQLAlchemy）。
- 数据库覆盖：MySQL/PostgreSQL/SQLite/SQLServer 初期；后续可扩展 Oracle。
- 传输：本地 UDP/HTTP 批量；或直接写入队列。
- 开销控制：采样模式 + 慢查询阈值过滤。
- 风险：安全（参数泄露）、性能（过度拦截）。

## 相关
- 现有 APM：NewRelic / Datadog（更重, 商业）。
- 开源慢查询日志分析工具。
- 各 ORM 官方事件/拦截器文档。

## 演化
- 阶段1：Node + Java + Python 三框架最小 Hook，控制台聚合输出。
- 阶段2：前端面板 + 基础过滤/排序。
- 阶段3：采样策略 + 慢查询阈值与告警。
- 阶段4：调用栈折叠与重复模式检测（N+1 提示）。
- 阶段5：与性能基准/压测集成，自动差异报告。

## 状态
当前：draft。

## 修订
- 2025-10-24: 初始创建。
- 2025-10-24: 关联 Issue #2。
