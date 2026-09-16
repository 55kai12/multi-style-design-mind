# Multi-Style Design Mind

可切换设计风格的 AI 设计大师系统，内置 **11 个独立风格模块**，专为 [WorkBuddy](https://www.workbuddy.cn) Skill 系统设计（同样适用于任何支持 SKILL.md 规范的 Agent）。

每次只激活一个风格（或按权重混合指定模块），未激活模块的设计公理、Design Token、特效规则完全隔离，杜绝「风格串味」。

> **English edition available** → see [README.en.md](README.en.md)，英文版 skill 在仓库的 `en/` 目录。

## 风格模块

| 编号 | 风格 | 关键词 |
|---|---|---|
| S1 | Apple Design Mind | 内容优先、材质深度、Liquid Glass、真实物理 |
| S2 | Swiss Minimal | 网格、留白、字重对比、零装饰、理性 |
| S3 | Glassmorphism Web | 彩色渐变、玻璃卡片、发光边、氛围 |
| S4 | Neo-Brutalism | 粗黑边、硬阴影、高饱和、贴纸感、态度 |
| S5 | Cyber HUD | 深色、霓虹、扫描线、信息密度、辉光 |
| S6 | Soft Neumorphism | 同色系、凸起凹陷、柔和双阴影 |
| S7 | Ins Minimal | 黑白灰、大留白、圆润、照片即主角 |
| S8 | 高级庄重中国风 | 朱红/金/墨/月白、对称、水墨、仪式感 |
| S9 | P5R 风格 | 纯红黑白、锯齿、涂鸦、漫画对话框、跃动 |
| S10 | 极简设计风 | 最少元素、单一焦点、基础型、功能可见性 |
| S11 | 欧式风格 | 米白/深棕/金点缀、对称、优雅、古典简化 |

每个模块统一遵循同一结构：

> 公理/决策顺序 → 色彩 → 字体 → 形状布局 → 材质 → 阴影 → 组件 → 动效 → 特效 → **实现要点（SwiftUI / Jetpack Compose / Web CSS 三平台）** → **可访问性（专属风险与降级方案）** → 禁用 → **自检清单** → 适用场景

## 特点

- **渐进披露**：激活哪个风格才加载哪个文件，上下文零污染。
- **三平台落地代码**：每个风格都给出 SwiftUI、Jetpack Compose（含等价物映射表与实现成本说明）、Web CSS 的具体写法，不是只给 Token。
- **可访问性是硬约束不是建议**：如 S3/S6 的低对比风险与降级、S5 的光敏闪烁 <3Hz 限制、S8/S11 的金色禁止作文字色、S9 的红底小字禁用等，均实测对比度并写明。
- **风格隔离规则**：混合时主风格决定信息架构、动效物理与禁用项，从风格只贡献视觉表层。
- **实现成本如实告知**：如 S6 双向阴影在 Compose 上成本最高、S8 无原生竖排，不硬造方案。

## 安装（WorkBuddy / 兼容 Agent）

```bash
git clone https://github.com/55kai12/multi-style-design-mind.git \
  ~/.workbuddy/skills/multi-style-design-mind
```

重启会话后生效。

## 使用

| 命令 | 作用 |
|---|---|
| `/style s1` … `/style s11` | 切换风格（默认 S1） |
| `/style s1+s3 7:3` | 混合：主风格在前，按权重叠加 |
| `/styles` | 列出所有风格与关键词 |
| `/reset` | 清除当前风格与上下文偏好 |
| `/lock on` | 锁定当前风格 |

混合示例：`/style s1+s3 7:3` —— 以 Apple 的结构、层级、动效物理为主，叠加 Web 玻璃拟态的色彩与材质氛围；禁用项以 S1 为准。

## 目录结构

```
multi-style-design-mind/
├── SKILL.md                      # 入口：调用协议、隔离规则、统一输出格式
├── references/
│   └── styles/
│       ├── s1-apple-design.md    # 最完整：含材质决策树、Compose/Web 映射、自检清单
│       ├── s2-swiss-minimal.md
│       ├── s3-glassmorphism-web.md
│       ├── s4-neo-brutalism.md
│       ├── s5-cyber-hud.md
│       ├── s6-soft-neumorphism.md
│       ├── s7-ins-minimal.md
│       ├── s8-chinese-classic.md
│       ├── s9-p5r.md
│       ├── s10-minimalist.md
│       └── s11-european-elegance.md
└── en/                           # 英文版（完整 skill）
    ├── SKILL.md
    └── references/styles/…       # 11 个英文风格模块
```

## License

[MIT](LICENSE)
