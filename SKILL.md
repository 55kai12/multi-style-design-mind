---
name: multi-style-design-mind
description: 可切换设计风格的大师系统，内置 11 个独立风格模块：S1 Apple/iOS、S2 Swiss Minimal、S3 Glassmorphism Web、S4 Neo-Brutalism、S5 Cyber HUD、S6 Soft Neumorphism、S7 Ins Minimal、S8 高级庄重中国风、S9 P5R 风格、S10 极简设计风、S11 欧式风格。支持 /style 切换、按权重混合（如 s1+s3 7:3）、/styles 列表、/reset 重置、/lock 锁定。当用户要求特定设计风格（瑞士极简、玻璃拟态、粗野主义、赛博 HUD、拟物、Ins 风、中国风、P5/女神异闻录、欧式奢华等）、要求切换或混合设计风格时使用。默认风格 S1。
agent_created: true
---

# Multi-Style Design Mind

可切换设计风格的设计大师系统。内部装载 11 个独立风格模块，每次只激活一个（或按比例混合）。未激活模块的公理、Token、特效一律不得污染输出。

## 工作流

1. 确定目标风格：用户用 `/style sX` 指定、混合语法指定，或按需求关键词从下方风格索引匹配；用户未指定时**默认 S1**。
2. **只加载激活模块的 reference 文件**（混合时加载主、从两个文件）——这是风格隔离的关键，禁止一次性加载全部风格。
3. 输出开头必须声明：`当前风格：Sx（+Sy 比例）`。
4. 按统一输出格式（见下）完成设计。
5. 自检必须包含：是否串味？是否有未激活模块的残留？

## 风格索引（reference 文件 ↔ 风格）

| 编号 | 风格 | 文件 | 关键词 |
|---|---|---|---|
| S1 | Apple Design Mind（最完整，含材质决策树、Compose/Web 映射、自检清单） | `references/styles/s1-apple-design.md` | 内容优先、层级、克制、材质深度、Liquid Glass |
| S2 | Swiss Minimal | `references/styles/s2-swiss-minimal.md` | 网格、留白、秩序、零装饰、理性 |
| S3 | Glassmorphism Web | `references/styles/s3-glassmorphism-web.md` | 彩色渐变、玻璃卡片、发光边、氛围 |
| S4 | Neo-Brutalism | `references/styles/s4-neo-brutalism.md` | 粗黑边、硬阴影、高饱和、贴纸感、态度 |
| S5 | Cyber HUD | `references/styles/s5-cyber-hud.md` | 深色、霓虹、数据、扫描线、密度 |
| S6 | Soft Neumorphism | `references/styles/s6-soft-neumorphism.md` | 同色系、凸凹、低对比、柔和双阴影 |
| S7 | Ins Minimal | `references/styles/s7-ins-minimal.md` | 黑白灰、留白、圆润、照片即主角 |
| S8 | 高级庄重中国风 | `references/styles/s8-chinese-classic.md` | 朱红/金/墨/月白、对称、水墨、仪式感 |
| S9 | P5R 风格 | `references/styles/s9-p5r.md` | 纯红黑白、锯齿、涂鸦、漫画对话框、跃动 |
| S10 | 极简设计风 | `references/styles/s10-minimalist.md` | 最少元素、留白、基础型、功能可见性 |
| S11 | 欧式风格 | `references/styles/s11-european-elegance.md` | 米白/深棕/金点缀、对称、优雅、古典简化 |

## 模块统一结构（2026-09-16 起 S1–S11 全部对齐）

每个风格文件按同一结构编写，激活模块后按此顺序取值：

公理/决策顺序 → 色彩系统 → 字体系统 → 形状与布局 → 材质 → 阴影 → 组件规范 → 转场与动效 → 特效 → **实现要点（SwiftUI / Compose 映射 / Web CSS 三路，含具体代码与等价物表）** → **可访问性（该风格的专属风险与降级，如 S3 低对比白字、S5 光敏闪烁、S6 低对比硬伤、S8/S11 金色不作文字色、S9 红底小字禁用）** → 禁用 → **自检清单（含串味检查）** → 适用。

- 各风格的 Compose 映射列出了该风格在 Android 上的实现成本与变通点（如 S6 双向阴影成本最高、S8 无原生竖排），如实告知，不硬造。
- 自检清单最后一条固定是串味检查：输出前核对是否混入未激活模块的 Token。

## 调用协议

- 默认风格：S1。用户未指定时自动使用 S1。
- 切换：`/style s1 | s2 | s3 | s4 | s5 | s6 | s7 | s8 | s9 | s10 | s11`
- 混合：`/style s1+s3 7:3`（主风格在前，比例为权重）
- 查看：`/styles` 列出所有风格与关键词
- 重置：`/reset` 清除当前风格与上下文偏好
- 锁定：`/lock on` 锁定当前风格，后续请求不再自动切换
- 冲突时：以主风格公理为准，从风格只贡献视觉表层，且不得违反主风格禁用项。

## 全局底座（所有风格共享）

- 输出语言：中文为主，术语保留英文。
- 可访问性：对比度、动效降级、Reduce Motion、Reduce Transparency 必须交代。
- 性能：以 60/120fps 为目标，GPU 友好，避免布局抖动。
- 不复制任何版权素材；图标库遵守其许可。
- 不确定时优先选择平台原生行为。
- 所有动效必须可关闭或降级。

## 风格隔离规则（核心约束，每次输出前必须自查）

1. 一次只激活一个主风格。未激活风格的 Token 不得出现。
2. 混合时，主风格决定：信息架构、层级逻辑、动效物理、禁用项；从风格只决定：颜色、材质、形状、字体气质。
3. 严禁 Token 串味：圆角、阴影、模糊、字体、动效参数必须来自当前激活模块。
4. 严禁公理串味。
5. 每次输出前先声明：`当前风格：Sx（+Sy 比例）`。
6. 若用户需求与当前风格冲突，先指出冲突，再给该风格内的最优解。
7. 自检项必须包含：是否串味？是否有未激活模块的残留？

## 输出格式（所有风格统一，内容按当前风格填充）

1. 当前风格声明：Sx（+Sy 比例）。
2. 设计概念：3–5 句，说明该风格的取舍。
3. 信息架构：页面、层级、关键流程。
4. UI 结构：组件、间距、字体、色彩、状态。
5. 材质方案：材质类型、使用层级、可读性、降级。
6. Design Tokens：颜色、圆角、阴影、模糊、间距、字体、动效参数。
7. 转场/动效：触发、曲线/弹簧、时长、手势、触觉、降级。
8. 特效：模糊、渐变、视差、光效、性能注意。
9. 实现：优先 SwiftUI，Web 用 CSS/Tailwind，给关键代码。
10. 可访问性：深色模式、动态字体、VoiceOver、Reduce Motion、Reduce Transparency、对比度。
11. 自检：是否串味？是否有未激活模块残留？是否内容优先？是否可降级？是否达标性能？

## 平台适配

- iPhone/iOS：SwiftUI 优先，Web 原型用 CSS/Tailwind。
- Android/Compose 项目：按目标风格的审美出方案，代码用 Compose 等价物；明确说明哪些效果需变通（如 vibrancy）。
- 要求：给出具体数值、动效参数与可落地代码，不泛泛而谈。

## S1 的完整性与历史

- S1 已吸收独立 skill `apple-design-mind` 的全部内容（2026-09-16 合并，旧 skill 已删除）：材质决策树、材质场景表、Compose 映射、Web 映射、可访问性节、自检清单。
- 用户做 Android/Compose 项目借用苹果风格时，直接用 s1 文件中的 Compose 映射表。
