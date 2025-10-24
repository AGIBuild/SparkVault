## 问题
常见 .NET 故障（内存泄漏、CPU 高、死锁、慢方法、意外退出）需事后人工多工具组合定位。

## 洞察
利用 EventPipe / DiagnosticServer 统一订阅关键事件与指标，阈值触发自动抓取 dump/trace 并执行模式分析。

## 概念
常驻或 sidecar 探针：进程发现 → 事件订阅 (GC/CPU/Exception/ThreadBlocking) → 阈值规则 → 触发 dump/trace/堆快照 → 分析 (内存热点/锁竞争/Top 方法/死锁图) → 报告 (JSON + Markdown)。

## 影响
缩短发现到定位时间；减少人工介入；形成性能与故障趋势基线。

## 可行性
依赖 ClrMD, EventPipe, dotnet-monitor 机制；跨平台 .NET6+ 支持；需控制采样避免性能下降。风险：误报、权限（Linux ptrace）。

## 演化
- P1: 事件订阅 + 阈值触发 dump/trace
- P2: 基础堆 / CPU 统计 + 报告
- P3: 死锁检测 + 慢方法分位图
- P4: 趋势存储 + 告警
- P5: 前端可视化 + 优化建议

## 风险
`perf-overhead`, `false-positive`, `platform-compat`

## 下一步
列出问题类型与对应事件 / API。

来源文件: `ideas/2025-10-24-dotnet-auto-diagnostics.md`