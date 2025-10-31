---
title: "IM 统一实时翻译插件（Slack + Teams）"
slug: "teams-slack-unified-translation"
date: 2025-10-31
author: ""
status: draft
tags: [tool-dev, civic-innovation]
impact_hypothesis: "统一跨 IM 平台翻译可覆盖 80%+ 企业协作场景，减少重复开发并提升 30%+ 跨语言沟通效率。"
scores: {impact: null, feasibility: null, novelty: null, urgency: null, alignment: null}
risk_flags: ["platform-api-diff", "model-size", "maintenance"]
next_step: "对比 Slack / Teams DOM 结构 + 调研轻量翻译模型浏览器端共用方案。"
issue: null
---

# IM 统一实时翻译插件（Slack + Teams）
跨平台输入框翻译方案：用母语输入，发送前自动翻译为目标语言；支持 Slack 与 Microsoft Teams，探索统一插件架构降低维护成本。

## 问题
多语言团队常用 Slack 或 Teams，需在不同平台重复配置翻译工具；独立开发两套插件成本高、功能不一致、用户学习曲线陡。

## 洞察
Slack 与 Teams 输入框交互模式相似（消息输入 → 发送按钮），可抽象统一逻辑层（翻译核心 + 配置管理），仅适配层处理平台差异（API / DOM 结构 / 权限）。

## 概念
架构分层：
- **核心层**（平台无关）：
  - **轻量级翻译模型**：NLLB-200-distilled / Opus-MT / 本地小模型（200MB-1GB）。
  - 翻译定制化：
    - **语气**：正式 / 友好 / 幽默风格。
    - **丰富度**：简洁 / 标准 / 详细。
    - **术语表**：产品名称、技术术语保持原文或映射。
  - 语言检测与目标语言配置。
  - 翻译缓存（避免重复翻译）。
  - 模式：纯替换（默认）。
- **适配层**（平台特定）：
  - Slack: 浏览器扩展拦截 DOM 输入框 / Electron 客户端 Hook。
  - Teams: 浏览器扩展 / Teams App（受限于官方 API）。
  - 统一接口：`getInputText()`, `setOutputText()`, `onSendBefore()`.
- **配置共享**：
  - 云端或本地同步用户偏好（源语言、目标语言、翻译质量预设、语气/丰富度）。

### 实现策略
1. **浏览器扩展优先**（Chrome/Edge/Firefox）：
   - 通过 Content Script 注入 Slack 与 Teams 页面。
   - DOM 选择器匹配输入框与发送按钮。
   - 核心逻辑共用，仅选择器配置差异化。
2. **桌面客户端备选**（Electron Hook）：
   - Slack 桌面版与 Teams 桌面版均基于 Electron。
   - 可通过注入脚本统一处理（需用户安装辅助工具）。

## 潜在影响
- 覆盖主流企业 IM 平台，降低用户切换成本。
- 减少 50%+ 重复开发（核心逻辑复用）。
- 统一用户体验与配置管理。
- 智能推荐回复可提升 50%+ 响应速度，且跨平台共用知识库降低维护成本。

## 可行性
- **技术**：浏览器扩展可访问 Slack / Teams Web 版 DOM；桌面版需额外 Hook 机制。
- **API 差异**：
  - Slack：无官方输入拦截 API，需扩展或 Hook。
  - Teams：Teams App 受限，扩展更灵活。
- **翻译模型部署**：
  - 本地轻量模型（200MB-1GB）：WASM / ONNX Runtime 浏览器端运行。
  - 远程推理服务：用户自建 / 插件提供的托管端点。
  - 延迟 <300ms，成本极低。
- **定制化实现**：
  - 语气/丰富度通过 prompt 模板或模型微调实现。
  - 术语表通过预处理替换或后处理校正。
- **隐私**：优先本地模型，消息内容不离开用户设备。
- **风险**：
  - 平台更新导致 DOM 结构变化。
  - 维护成本：两平台演进速度不同。
  - 轻量模型质量 vs 通用大模型需权衡（可提供质量档位选择）。

## 相关
- Slack 翻译 bot（被动触发）。
- Teams 内置翻译（消息后翻译，非输入时）。
- 浏览器通用翻译扩展（Grammarly 模式）。

## 演化
- 阶段1：浏览器扩展支持 Slack + Teams Web 版 + 轻量本地模型（NLLB-distilled）。
- 阶段2：语气/丰富度定制 + 术语表支持。
- 阶段3：桌面客户端支持（Electron Hook）。
- 阶段4：**智能推荐回复**：
  - 分析对话上下文（近期消息 + 频道主题）+ 用户知识库（常用回复 / 团队话术）。
  - 生成 3-5 条推荐回复（目标语言），用户点选即可发送。
  - 跨平台共用推荐引擎，减少重复训练成本。
- 阶段5：扩展至 Discord / Telegram（验证架构通用性）。
- 阶段6：团队协作翻译记忆库 + 质量反馈循环。

## 统一架构可行性评估
| 维度 | Slack | Teams | 共用可行性 |
|------|-------|-------|-----------|
| 输入框拦截 | DOM / Hook | DOM / Hook | 高（选择器配置化） |
| 官方 API | 无输入拦截 | 无输入拦截 | 中（均需扩展方案） |
| 桌面版 | Electron | Electron | 高（注入机制相似） |
| 配置同步 | 用户本地/云 | 用户本地/云 | 高（统一配置格式） |
| 维护成本 | DOM 变化风险 | DOM 变化风险 | 中（需双平台监控） |

推荐：优先浏览器扩展 + 核心逻辑共用，适配层配置化管理平台差异。

## 状态
当前：draft。

## 修订
- 2025-10-31: 初始创建，考虑 Slack + Teams 统一架构。
