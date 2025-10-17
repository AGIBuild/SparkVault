# SparkVault

> 创意是一束火花；在恰当的时间、资源与协作到来之前，需要被安全保存、逐步澄清与择优孵化。

## 1. 宗旨
SparkVault 用来：
- 捕捉尚未实现的工具、产品、系统或社会创新构想
- 给予最低结构（避免只剩一句口号）
- 让贡献者补充、批判、降风险（de-risk）
- 为未来挑选进入原型 / 试点阶段做准备

## 2. 适用范围
本仓库收录的多为：
- 暂未排入近期优先级
- 潜在高影响但资源尚不足
- 需要更清晰的表述与风险识别
- 具备未来原型或协作可能性

## 3. 仓库结构建议
```
/
├── ideas/                # 原始与迭代中的创意条目
├── prototypes/           # （可选）技术或流程的早期实验
├── pipeline/             # 评估/入选清单
├── docs/                 # 研究、通用方法、参考资料
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
└── IDEA-TEMPLATE.md
```

## 4. 创意文件模板
文件放在 `ideas/`，命名：`YYYY-MM-DD-short-slug.md`。

建议内容结构：
```
# 标题
一句话概述

## 问题（Problem）
要解决的真实痛点 / 系统性缺口及其重要性

## 核心洞见（Insight）
区别于常规方案的关键视角 / 杠杆点

## 概念描述（Concept）
核心机制、参与者、最小使用路径（MVP 叙事）

## 潜在影响（Potential Impact）
影响对象层次：个人 / 社区 / 行业 / 公共系统；可写假设式量化指标

## 可行性初探（Feasibility Notes）
技术栈猜测、必要条件、关键风险、资源缺口

## 关联（Related）
研究、法规、竞品、数据源、参考链接

## 演化思路（Evolution Ideas）
可拆分的验证实验 / 子模块 / 阶段性里程碑

## 状态（Status）
draft | exploring | ready-for-prototype | archived

## 修订记录（Revision Notes）
- YYYY-MM-DD: 更新说明
```

可选 front-matter：
```
---
tags: [tool-dev, civic-innovation]
status: draft
author: 你的名字
priority: low
impact_hypothesis: "如果做成，X 指标可能提升 Y%"
---
```

## 5. 标签建议
- tool-dev（工具 / 产品）
- civic-innovation（公共治理 / 公民参与）
- system-reform（制度 / 结构改进）
- data-platform（数据平台）
- ai-augment（AI 增强）
- sustainability（可持续）
- education（教育）
- experimental-policy（政策试验）
- protocol（协议 / 标准）
- speculative（前沿 / 假设性）

## 6. 演化流程
1. Capture（捕获）  
2. Enrich（充实背景、风险、对比）  
3. Score（打分：Impact / Feasibility / Novelty / Urgency / Alignment）  
4. Select（入选原型候选）  
5. Prototype（开发原型或流程试点）  
6. Archive（归档：已实现、过时、重复）  

## 7. 评估维度
| 维度 | 关键问题 | 提示 |
|------|----------|------|
| Impact（影响） | 能否显著改变现状或扩散价值？ | 广度 + 深度 |
| Feasibility（可行性） | 近期可被验证或构建吗？ | 资源 + 清晰度 |
| Novelty（新颖度） | 与现有方案差异多大？ | 独特性 |
| Urgency（紧迫性） | 现在验证是否比延后更具优势？ | 时间敏感度 |
| Alignment（一致性） | 是否符合“工具 + 社会改进”双主线？ | 使命贴合度 |

## 8. 贡献方式
- Fork + PR：新增创意文件或补充现有条目
- 评论聚焦：背景事实、可行性路径、风险识别、对比案例
- 保护动机：不要抹去原作者意图，可附加补充段落或 Revision Notes
- 提交实现提议时，请描述 MVE（最小可验证实验）步骤

## 9. 行为准则
鼓励：
- 基于证据的分析与挑战
- 明确区分事实 / 假设 / 推测
- 注重伦理与公共影响（隐私、公平、可访问性）
拒绝：
- 人身攻击
- 空泛或绝对化结论

建议采用 [Contributor Covenant](https://www.contributor-covenant.org/) 补充正式条款。

## 10. 路线图（草案）
- [ ] 初始化 5–10 条创意
- [ ] 简单评分脚本（GitHub Actions 或本地脚本）
- [ ] 公布首批 ready-for-prototype 清单
- [ ] 开启社区讨论（Discussions）
- [ ] 选择 1–2 条进入原型目录或独立仓库

## 11. 许可
建议：
- 内容（ideas / docs）：CC BY 4.0
- 代码 / 原型：MIT 或 Apache-2.0

## 12. 常见问答
Q: 我能直接去实现某个创意吗？  
A: 可以。请在 Issue 或 PR 中说明计划并链接源文件。

Q: 为什么不直接全部写成代码？  
A: 资源有限，结构化存储提高未来协作与复用效率，避免低效重复。

Q: 如何防止创意“腐烂”？  
A: 定期（季度）审查：更新状态，归档陈旧或已被外部实现的条目。

---

欢迎点亮第一批火花，让它们逐步成为现实。