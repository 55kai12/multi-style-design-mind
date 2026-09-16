# S3 · Glassmorphism Web（网页玻璃拟态）

关键词：彩色渐变、玻璃卡片、大圆角、发光边、通透、氛围。
公理：背景即氛围；玻璃即层级；光即引导；通透即现代。
决策顺序：背景氛围 → 玻璃层级 → 光效引导 → 动效。

## 色彩系统
- 背景渐变：紫蓝 #667EEA→#764BA2、粉橙 #FF6B6B→#FFA07A、青绿 #43E97B→#38F9D7。
- 玻璃填充：rgba(255,255,255,0.08–0.18)。
- 边框：1px rgba(255,255,255,0.18–0.35)。
- 文字：白色 #FFFFFF 主，rgba(255,255,255,0.7) 次。
- 强调：亮青 #00E5FF 或亮粉 #FF2D95。
- 内发光：inset 0 1px 0 rgba(255,255,255,0.3)。
- 深色模式：更深渐变 + 更低透明度。

## 字体系统
- 字体族：Inter / SF Pro / Manrope / Poppins。
- 标题：32/40/48pt，字重 600–700。
- 正文：16/18pt，字重 400–500，行高 1.6。
- 字间距：0 到 0.5。
- 禁止：衬线体、花哨字体。

## 形状与布局
- 圆角：卡片 20–32，按钮胶囊，输入框 12–16。
- 间距：16/24/32/48/64。
- 网格：12 列，gutter 24。
- 留白充足，卡片间距 24–32。

## 材质
- backdrop-blur 16–40px。
- 背景 rgba(255,255,255,0.08–0.18)。
- 边框 1px rgba(255,255,255,0.18–0.35)。
- 内发光 + 外发光可选。
- 禁止：玻璃叠玻璃超过 2 层、全屏模糊导致性能崩。

## 阴影
- 大而柔：y 20 blur 60 opacity 0.2。
- 可带彩色投影：0 20 60 rgba(102,126,234,0.3)。

## 组件规范
- 按钮：胶囊 + 玻璃 + 发光边框 + hover 抬升。
- 卡片：大圆角 + 玻璃 + 内发光。
- 输入框：玻璃 + 圆角 + focus 发光。
- 导航：顶部玻璃条 + 模糊。
- 弹窗：玻璃 + 大圆角 + 背景模糊。

## 动效
- 漂浮、微视差、悬浮抬升、渐变流动。200–500ms，ease-out。
- hover：translateY(-4px) + shadow 增强。
- 禁止：生硬位移、闪烁。

## 特效
- 光斑、噪点叠层、鼠标跟随高光、渐变位移。
- 背景可加 animated gradient。

## 实现要点

### Web / CSS（本风格的主场）
- 玻璃：`backdrop-filter: blur(24px) saturate(160%); background: rgba(255,255,255,0.12); border: 1px solid rgba(255,255,255,0.25);`
- 内发光：`box-shadow: inset 0 1px 0 rgba(255,255,255,0.3);` 彩色投影：`0 20px 60px rgba(102,126,234,0.3)`。
- 背景：`linear-gradient(135deg, #667EEA, #764BA2)` + 光斑 blob（`position:absolute; border-radius:50%; filter: blur(80px); opacity:0.4`）。
- hover：`transform: translateY(-4px); box-shadow: 0 24px 68px rgba(102,126,234,0.4);`
- 性能预算：一屏 backdrop-filter 元素 ≤3 个，禁止嵌套玻璃；低端设备降级为半透明实色。

### SwiftUI
- `.background(.ultraThinMaterial, in: RoundedRectangle(cornerRadius: 24, style: .continuous))`，彩色渐变放最底层作氛围。
- 注意 iOS 材质自带克制性：氛围靠背景渐变和光斑，不要给玻璃加染色。

### Compose 映射
| 概念 | 等价物 | 注意 |
|---|---|---|
| backdrop-blur | `Modifier.graphicsLayer { renderEffect = RenderEffect.createBlurEffect(24f, 24f, TileMode.CLAMP).asComposeRenderEffect() }` | API 31+；低版本降级为半透明实色卡片 |
| 玻璃填充 | 半透明白 surface（0.08–0.18 alpha） | — |
| 发光边框 | Modifier.border(1.dp, Brush.linearGradient(白→透明)) | — |
| hover 抬升 | animateFloatAsState + graphicsLayer translationY | — |

## 可访问性
- **最大风险是低对比白字**：玻璃上的主文字必须实测 ≥4.5:1，不达标时玻璃后加 rgba(0,0,0,0.2) scrim 或提高填充不透明度。
- Reduce Transparency：玻璃卡片降级为实色 rgba(30,30,60,0.95)，保留圆角与阴影。
- Reduce Motion：漂浮/渐变流动/鼠标跟随全部停止，保留静态渐变。
- 动态字体：玻璃卡片高度随文字放大自适应，禁止固定高度截断。

## 禁用
低对比白字、玻璃叠玻璃超过 2 层、全屏模糊导致性能崩、纯黑背景。

## 自检清单
- [ ] 玻璃是否 ≤2 层、无玻璃叠玻璃？
- [ ] 白字对比是否实测 ≥4.5:1（必要时加 scrim）？
- [ ] backdrop-filter 是否有性能预算（≤3 个/屏）？
- [ ] 是否有实色降级（Reduce Transparency）？
- [ ] 是否串味（出现 S1 式 1px 高光/语义色体系 = 残留）？

## 适用
SaaS 落地页、Dashboard、Web3、产品官网、AI 工具。
