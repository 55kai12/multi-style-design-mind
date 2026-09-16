# S2 · Swiss Minimal（国际主义 / 极简网格）

关键词：网格、留白、秩序、中性、字重对比、零装饰、理性。
公理：网格即秩序；留白即呼吸；字体即图形；装饰即噪音；对齐即美；理性即普适。
决策顺序：信息架构 → 网格建立 → 排版层级（字重对比） → 对齐校准 → 呈现。装饰层不存在——这是特性，不是缺失。

## 色彩系统
- 黑 #000000、白 #FFFFFF、灰阶 #F5F5F5 / #E5E5E5 / #999999 / #666666 / #333333。
- 强调色仅一个：红 #E30613 或蓝 #0055FF 或黄 #FFD500。
- 无渐变、无透明、无彩色玻璃。
- 色彩比例：黑 10%、白 70%、灰 15%、强调 5%。
- 深色模式：反相，保持同一逻辑。

## 字体系统
- 字体族：Helvetica Now / Inter / SF Pro / Univers。
- 标题：大而粗，48/64/80pt，字重 Bold/Black，字间距 -1 到 -2。
- 正文：16/18pt，Regular，行高 1.5–1.6。
- 强字重对比：标题 Black vs 正文 Regular。
- 严格左对齐，禁止居中（除少数海报式）。
- 网格基线：4pt 或 8pt。
- 禁止：花哨字体、书法、装饰字。

## 形状与布局
- 网格：12 列或 6 列，gutter 24–32，margin 32–64。
- 间距：8/16/24/32/48/64/96/128。
- 圆角：0–4 或直角。
- 分隔：1px 细线 #E5E5E5。
- 对齐：严格左对齐，元素对齐网格。
- 留白：大面积，呼吸感强。

## 材质与阴影
- 无毛玻璃、无渐变、无噪点。
- 纯色块与细线分隔。
- 阴影：无，或极淡单层 y 1 blur 2 opacity 0.05。
- 禁止：玻璃、发光、拟物、纹理。

## 组件规范
- 按钮：矩形或小圆角，纯色填充，无阴影。
- 卡片：无圆角或 4pt，细线边框或纯色块。
- 输入框：底部 1px 线，无圆角。
- 导航：顶部左对齐，字号对比强。
- 列表：细线分隔，无圆角。

## 动效
- 快速、线性或小弹簧。淡入 + 位移 8–16px。120–240ms。无过冲。
- 禁止：夸张弹簧、粒子、视差、漂浮。

## 特效
- 无。最多用遮罩揭示或简单淡入。

## 实现要点

### SwiftUI
- 字体：系统 SF Pro 即 Helvetica 血统，`.font(.system(size: 64, weight: .black))` + `.kerning(-2)`；正文 `.system(size: 16, weight: .regular)`。
- 分隔线：`Rectangle().fill(Color(hex: "#E5E5E5")).frame(height: 1)`。
- 布局：`LazyVGrid(columns: 12)` 或自定义 Layout；全部 `.leading` 对齐。
- 动效：`.animation(.linear(duration: 0.18), value: ...)`，淡入 + offset 8–16px；禁用 spring。

### Compose 映射
| 概念 | 等价物 | 注意 |
|---|---|---|
| 12 列网格 | 自定义 Layout（Row/Column 手动分配） | 无原生 12 列，需自实现 |
| 字重对比 | FontWeight.Black(900) vs FontWeight.Normal(400) | 对比即层级 |
| 字间距 | TextStyle letterSpacing = (-1).sp | 标题负间距 |
| 细线分隔 | HorizontalDivider(thickness = 1.dp, color = #E5E5E5) | — |
| 直角 | RoundedCornerShape(0.dp) / RectangleShape | — |
| 动效 | tween(180, LinearEasing)，fade + slide 8–16dp | 禁 spring/tween 弹性 |

### Web / CSS
- 网格：`grid-template-columns: repeat(12, 1fr); gap: 24–32px;` margin 32–64px。
- 字体：Inter（Google Fonts 免费商用），标题 `font-weight: 900; letter-spacing: -2px`。
- 输入框：`border: none; border-bottom: 1px solid #E5E5E5; border-radius: 0;`
- 动效：`transition: opacity .18s linear, transform .18s linear;`

## 可访问性
- 黑白灰天然高对比：#333 on #FFF ≈ 12:1，正文达标无压力。
- 强调色红 #E30613 作文字色对白底 ≈ 5:1 可用；黄 #FFD500 只能作色块底色配黑字（≈ 14:1），禁止作文字色。
- Reduce Motion：本就线性淡入，降级为直接切换即可。
- 响应式：窄屏/大字体下网格折叠列数（12→4→2），左对齐原则不变。

## 禁用
毛玻璃、发光、渐变、圆角卡片、拟物、粒子、夸张弹簧、装饰元素。

## 自检清单
- [ ] 是否严格对齐网格？
- [ ] 是否严格左对齐（除海报式）？
- [ ] 强调色是否只有一个、占比 ≤5%？
- [ ] 是否零装饰（无阴影、无玻璃、无渐变）？
- [ ] 标题/正文字重对比是否足够强？
- [ ] 是否串味（出现圆角卡片/毛玻璃/弹簧动效 = S1/S3 残留）？

## 适用
编辑器、作品集、数据密集后台、品牌站、建筑与设计机构。
