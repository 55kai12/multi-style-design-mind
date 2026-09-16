# S5 · Cyber HUD（赛博 / 科幻界面）

关键词：深色、霓虹、数据、扫描线、HUD、密度。
公理：信息即界面；光即状态；密度即专业感；故障即真实。
决策顺序：信息密度架构 → 数据层级 → 光即状态 → 动效（扫描/脉冲/故障）。

## 色彩系统
- 深底 #05070A / #0B1020 / #0F1626。
- 霓虹青 #00F0FF、品红 #FF00E5、荧光绿 #00FF88、警示橙 #FF6B00、危险红 #FF2D55。
- 文字：青白 #E0F7FF 主，rgba(224,247,255,0.6) 次。
- 辉光：0 0 12–32px 霓虹色。
- 深色模式：本身即深色。

## 字体系统
- 字体族：等宽（JetBrains Mono / SF Mono / IBM Plex Mono）+ 无衬线（Inter / Rajdhani）。
- 数字：等宽，字间距 1–2。
- 标题：24/32/40pt，字重 600–700，全大写。
- 正文：14/16pt，字重 400。
- 禁止：衬线、圆润字体。

## 形状与布局
- 圆角：0–4，直角为主。
- 斜切角、角标装饰、细描边 1px。
- 间距：4/8/12/16/24/32。
- 密度高，信息密集。
- 网格：细网格背景。

## 材质
- 半透明深色面板 + 细网格。
- 弱毛玻璃可用但必须深色。
- 禁止：浅色玻璃、柔和材质。

## 阴影
- 辉光代替阴影：0 0 12–32px 霓虹色。
- 禁止：柔和阴影。

## 组件规范
- 按钮：细描边 + 辉光 + hover 增强。
- 卡片：深色面板 + 细网格 + 角标。
- 输入框：等宽 + 细描边 + focus 辉光。
- 导航：顶部 HUD 条 + 状态指示。
- 弹窗：深色面板 + 扫描线。

## 动效
- 扫描、打字机、数据滚动、脉冲、故障闪烁。150–600ms。线性为主。
- 禁止：柔和弹簧、缓慢过渡。

## 特效
- 扫描线、噪点、故障位移、雷达、能量条、数据流。

## 实现要点

### Web / CSS（本风格主场）
- 辉光：`text-shadow: 0 0 12px #00F0FF; box-shadow: 0 0 24px rgba(0,240,255,0.5);`
- 扫描线：`background: repeating-linear-gradient(0deg, rgba(0,240,255,0.04) 0 1px, transparent 1px 3px);`
- 细网格：`repeating-linear-gradient` 双向，rgba(0,240,255,0.06)。
- 故障效果：clip-path + transform 错位帧动画 150–300ms，或 SVG feTurbulence + feDisplacementMap。
- 角标：伪元素画 L 形（border-top + border-left 各 2px 霓虹色）。
- 字体：JetBrains Mono、Rajdhani（Google Fonts 免费商用）。
- 性能：辉光层数控制，`will-change: transform` 只给动画元素；扫描线用背景而非独立 DOM 层。

### SwiftUI
- 辉光：`.shadow(color: Color(hex: "#00F0FF").opacity(0.6), radius: 8)` 叠两层（近小远大）。
- 扫描线：TimelineView 驱动 LinearGradient mask 移动，注意功耗，静止时停表。
- 斜切角：自定义 Shape（Path 画八边形）。

### Compose 映射
| 概念 | 等价物 | 注意 |
|---|---|---|
| 等宽字体 | FontFamily.Monospace 或打包 JetBrains Mono | 数字用 tabular figures |
| 辉光 | drawBehind 双层绘制：模糊层（blur 8–16）+ 实色层 | Compose 无 text-shadow |
| 细描边 | Modifier.border(1.dp, Color(0xFF00F0FF)) | — |
| 斜切角 | 自定义 Shape（Path） | — |
| 扫描/脉冲 | rememberInfiniteTransition + tween 线性 | Reduce Motion 时停用 |

## 可访问性
- **光敏安全是硬约束**：故障闪烁频率必须 < 3Hz（WCAG 2.3.1），且提供「关闭闪烁/故障效果」开关。
- 辉光不能替代对比度：#E0F7FF on #05070A ≈ 16:1 达标；霓虹青 #00F0FF 作正文需实测（≈10:1 尚可）；品红 #FF00E5 只作强调不作正文。
- 深底上 rgba(224,247,255,0.6) 次要文字 ≈ 6:1，达标题注级；更淡就违规。
- Reduce Motion：扫描/打字机/数据滚动/故障全部替换为静态状态显示或单次淡入。

## 禁用
柔和圆角、暖色、大面积留白、Apple 式克制、优雅字体。

## 自检清单
- [ ] 是否深色底、辉光代替阴影（无柔和投影）？
- [ ] 闪烁是否 <3Hz 且有开关？
- [ ] 霓虹色作正文是否实测对比 ≥4.5:1？
- [ ] Reduce Motion 是否关闭扫描/故障类动效？
- [ ] 信息密度是否服务于专业感而非堆砌？
- [ ] 是否串味（出现柔和阴影/大圆角/暖色 = S1/S6 残留）？

## 适用
监控大屏、游戏 UI、AI 工具、科幻概念、数据可视化。
