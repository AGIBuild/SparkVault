---
title: "IM 统一实时翻译插件（Slack + Teams）"
slug: "teams-slack-unified-translation"
date: 2025-10-31
author: ""
status: draft
tags: [tool-dev, civic-innovation]
impact_hypothesis: "统一跨 IM 平台翻译可覆盖 80%+ 企业协作场景，减少重复开发并提升 30%+ 跨语言沟通效率。"
scores: {impact: null, feasibility: null, novelty: null, urgency: null, alignment: null}
risk_flags: ["platform-api-diff", "privacy", "maintenance"]
next_step: "对比 Slack / Teams 输入拦截机制与共用插件架构可行性。"
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
  - 翻译引擎适配（DeepL / Azure / 本地模型）。
  - 语言检测与目标语言配置。
  - 翻译缓存与术语表。
  - 模式切换（纯替换 / 双语 / 预览确认）。
- **适配层**（平台特定）：
  - Slack: 浏览器扩展拦截 DOM 输入框 / Electron 客户端 Hook。
  - Teams: 浏览器扩展 / Teams App（受限于官方 API）。
  - 统一接口：`getInputText()`, `setOutputText()`, `onSendBefore()`.
- **配置共享**：
  - 云端或本地同步用户偏好（源语言、目标语言、翻译服务、快捷键）。

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

## 可行性
- **技术**：浏览器扩展可访问 Slack / Teams Web 版 DOM；桌面版需额外 Hook 机制。
- **API 差异**：
  - Slack：无官方输入拦截 API，需扩展或 Hook。
  - Teams：Teams App 受限，扩展更灵活。
- **翻译**：DeepL / Azure 统一接口；本地模型（MarianMT）可选。
- **风险**：
  - 平台更新导致 DOM 结构变化。
  - 隐私：翻译数据是否上云需明确策略。
  - 维护成本：两平台演进速度不同。

## 相关
- Slack 翻译 bot（被动触发）。
- Teams 内置翻译（消息后翻译，非输入时）。
- 浏览器通用翻译扩展（Grammarly 模式）。

## 演化
- 阶段1：浏览器扩展支持 Slack + Teams Web 版 + DeepL API。
- 阶段2：桌面客户端支持（Electron Hook）。
- 阶段3：本地模型选项 + 术语表自定义。
- 阶段4：扩展至 Discord / Telegram（验证架构通用性）。
- 阶段5：团队协作翻译记忆库 + AI 优化建议。

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
