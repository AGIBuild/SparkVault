---
title: ".NET 自动诊断工具"
slug: "dotnet-auto-diagnostics"
date: 2025-10-24
author: ""
status: draft
tags: [tool-dev]
impact_hypothesis: "自动化捕获与分析 .NET 常见故障可降低 30% 以上排错时间，减少线上回溯成本。"
scores: {impact: null, feasibility: null, novelty: null, urgency: null, alignment: null}
risk_flags: ["perf-overhead", "false-positive", "platform-compat"]
next_step: "梳理目标问题类型与可用诊断 API (EventPipe / DiagnosticServer)。"
issue: 3
---

# .NET 自动诊断工具
跨平台运行（Windows/Linux/macOS），利用 Microsoft.Diagnostics 工具链或事件管道，对 .NET 应用常见问题自动探测与生成报告。

## 问题
内存泄漏、CPU 飙高、线程死锁、进程意外退出、卡死、慢方法定位等常见问题需要开发者在事后使用多种独立工具 (dotnet-trace / dotnet-dump / perf / pprof)，成本高、时效差。

## 洞察
.NET 运行时暴露了事件流 (EventPipe)、诊断协议 (DiagnosticServer)、GC/线程/Exception 指标，可统一采集；自动模式可在阈值触发时抓取快照并进行模式分析（如对象分配热点、锁竞争、异常瀑布）。

## 概念
常驻探针进程或 sidecar：
- 发现目标进程（PID 或自动扫描）。
- 订阅关键事件（GC、CPU、Exception、ThreadBlocking、RuntimeCounter）。
- 阈值规则：如 GC Gen2 频率、总分配速率、CPU > X 秒、线程阻塞>Y。
- 触发动作：采集 dump / trace 片段 / 堆快照。
- 分析模块：
  - 内存：大对象、频繁短命对象、泄漏可疑根。
  - CPU：Top 方法 + 调用栈聚合。
  - 死锁：线程等待图检测环。
  - 慢方法：Method执行时间分位统计。
- 生成结构化报告 (JSON + Markdown)。

## 潜在影响
- 缩短问题发现→原因定位路径。
- 减少人工临时抓取频率。
- 为性能基线建立历史趋势。
- 提升非专家开发者的故障处理效率。

## 可行性
- 技术：Microsoft.Diagnostics.Runtime (ClrMD)、EventPipe、dotnet-monitor 机制参考。
- 平台：.NET 6+ 支持跨平台事件与 dump；需区分权限（Linux ptrace）。
- 开销：采样/分段抓取控制；可动态关闭高成本分析。
- 风险：误报/过度追踪带来性能下降；需默认保守策略。

## 相关
- dotnet-monitor（提供诊断端点但侧重手动调用）。
- ClrMD 分析堆对象、线程、类型信息。
- Perf/ebpf 可辅助 CPU 采样（扩展阶段）。

## 演化
- 阶段1：事件订阅 + 简单阈值触发 dump/trace。
- 阶段2：堆与 CPU 基础统计 + Markdown 报告。
- 阶段3：死锁检测 + 慢方法分位图。
- 阶段4：趋势存储（SQLite / 文件）+ 告警（Webhook）。
- 阶段5：可视化前端 + 建议引擎（推荐优化方向）。

## 状态
当前：draft。

## 修订
- 2025-10-24: 初始创建。
- 2025-10-24: 关联 Issue #3。
