# S9 · P5R 风格（女神异闻录5 皇家版）

关键词：纯红/黑/白、非对称、锯齿、涂鸦、漫画对话框、跃动。
公理：冲突即张力；华丽到极致、不羁到张狂；界面即表演。
决策顺序：信息 → 色块与锯齿构图 → 非对称张力 → 跃动动效（演出层）。材质层不存在。

## 色彩系统
- 纯红 #E60012 主色。
- 纯黑 #000000。
- 纯白 #FFFFFF。
- 少量黄 #FFCC00 点缀。
- 比例：红 50%、黑 30%、白 15%、黄 5%。
- 深色模式：保持同一逻辑，黑白反相。
- 禁止：低饱和、柔和色。

## 字体系统
- 英文：DIN Condensed Bold / Bebas Neue。
- 日文：新ゴ B / 思源黑体 Bold。
- 手写：brush 风格（克制使用）。
- 字号：标题 40/56/72pt，正文 16/18pt。
- 字重：900 或 Bold。
- 倾斜、旋转、错位。
- 禁止：细字重、衬线、优雅字体。

## 形状与布局
- 斜角对称、锯齿边缘、撕裂效果。
- 漫画式对话框、围绕角色身体展开的指令树。
- 色块 + 文字构造。
- 圆角：0–8 或直角。
- 布局非对称、动态、张力强。

## 材质
- 无毛玻璃。
- 纯色块、矢量图形、涂鸦、半调网点。
- 禁止：玻璃、柔和材质。

## 阴影
- 硬阴影，无模糊，offset 4–8px，纯黑。
- 禁止：柔和阴影。

## 组件规范
- 按钮：锯齿边 + 纯红 + 硬阴影 + hover 位移。
- 卡片：斜角 + 纯色 + 涂鸦。
- 输入框：粗边 + 纯色底。
- 导航：非对称 + 高对比。
- 弹窗：漫画对话框 + 纯色。

## 动效
- 界面切换动画密集，Pop 文字跃动，快速生硬位移，允许错位抖动。80–300ms。
- 禁止：柔和过渡、缓慢动画。

## 特效
- 涂鸦、锯齿撕裂、半调网点、色块翻转、Pop 文字、动态指示条纹。

## 实现要点

### Web / CSS（本风格最适合）
- 锯齿：`clip-path: polygon(...)` 或 SVG path 撕裂边缘；斜切角 `polygon(8px 0, 100% 0, 100% calc(100% - 8px), calc(100% - 8px) 100%, 0 100%, 0 8px)`。
- 倾斜：`transform: rotate(-2deg) skewX(-3deg);`（容器级，文本反向转回保证可读）。
- Pop 文字：进入时 `scale(1.3) → 1` + rotate 回弹，80–150ms，配 `steps()` 或强 spring。
- 半调网点：`background-image: radial-gradient(#000 1px, transparent 1px); background-size: 4px 4px; opacity: 0.08;`
- 字体：Bebas Neue（Google Fonts 免费）替代 DIN Condensed（有版权）；中文思源黑体 Bold。
- 性能：动画只动 transform/opacity；锯齿用 clip-path 而非图片。

### SwiftUI
- 色块斜角：自定义 Shape（Path）；旋转 `.rotationEffect(.degrees(-2))`；skew 需 GeometryEffect 自实现。
- Pop 文字：`.scaleEffect` + `.spring(response: 0.25, dampingFraction: 0.5)`。
- 撕裂边缘：SVG 转 asset 或 mask。

### Compose 映射
| 概念 | 等价物 | 注意 |
|---|---|---|
| 锯齿/斜切 | 自定义 Shape（Path 画多边形） | — |
| 倾斜错位 | Modifier.graphicsLayer { rotationZ = -2f; transformOrigin } | skew 用 Matrix |
| 硬阴影 | drawBehind 偏移纯黑层（同 S4） | 别用 elevation |
| Pop 文字 | animateFloatAsState spring(dampingRatio = 0.4f) | 80–150ms |
| 色块翻转 | Crossfade / AnimatedContent + tween(100) | — |
| 半调网点 | Canvas 点阵或纹理 asset | — |

## 可访问性
- **红底白字 #E60012/#FFF ≈ 4.0:1 —— 大字号（≥24pt Bold）达标 3:1，小字号正文必须改黑底白字（≈ 18:1）**。这是硬约束，不是建议。
- 黄 #FFCC00 只作色块与描边，禁止作文字色（on 白 ≈ 1.6:1）。
- 高密度跃动动效是光敏与 Reduce Motion 重灾区：闪烁 <3Hz；提供「跳过演出」降级——转场演出直接切内容（游戏化界面尤其需要，参考 P5R 自身的快进设置）。
- 非对称布局的 Tab/焦点顺序仍须符合逻辑顺序。

## 禁用
柔和圆角、低饱和、克制、留白呼吸感、优雅字体。

## 自检清单
- [ ] 是否纯红黑白黄四色、零低饱和？
- [ ] 阴影是否全硬无模糊？
- [ ] 小字正文是否避开红底？
- [ ] 演出动效是否可跳过、闪烁是否 <3Hz？
- [ ] 焦点/Tab 顺序是否符合逻辑（非对称 ≠ 乱序）？
- [ ] 是否串味（出现留白呼吸感/圆角卡片/玻璃 = S1/S7/S3 残留）？

## 适用
游戏 UI、潮牌、音乐产品、创意活动页、Z世代产品。
