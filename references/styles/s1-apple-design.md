# S1 · Apple Design Mind（原生 iOS）

关键词：内容优先、层级、克制、材质深度、真实物理、高保真、Liquid Glass。
公理：内容即界面；层级即空间；运动即因果；材质即深度；反馈即信任；克制即高级；可访问性即设计。
决策顺序：信息架构 → 视觉层级 → 材质 → 运动 → 特效。禁止从特效开始设计，禁止先加毛玻璃再想层级。

## 色彩系统
- 语义色优先：label / secondaryLabel / tertiaryLabel / quaternaryLabel。
- 背景：systemBackground / secondarySystemBackground / tertiarySystemBackground / systemGroupedBackground / secondarySystemGroupedBackground。
- 填充：systemFill / secondarySystemFill / tertiarySystemFill / quaternarySystemFill。
- 分隔：separator / opaqueSeparator。
- 强调：tint（默认 systemBlue #007AFF），只用于关键操作。
- 系统色：systemRed #FF3B30、systemOrange #FF9500、systemYellow #FFCC00、systemGreen #34C759、systemTeal #5AC8FA、systemBlue #007AFF、systemIndigo #5856D6、systemPurple #AF52DE、systemPink #FF2D55。
- 深色模式：背景 #000000 / #1C1C1E / #2C2C2E；文字自动反相。
- 高对比度：Increase Contrast 时提高描边与文字对比。
- 禁止：高饱和撞色滥用、彩色玻璃滥用、渐变文字。

## 字体系统
- 字体族：SF Pro Display（≥20pt）、SF Pro Text（<20pt）。
- 字号：Large Title 34 Bold、Title1 28 Regular、Title2 22 Regular、Title3 20 Regular、Headline 17 Semibold、Body 17 Regular、Callout 16 Regular、Subheadline 15 Regular、Footnote 13 Regular、Caption1 12 Regular、Caption2 11 Regular。
- 行高：Body 22、Title 34/41、Caption 16。
- 字间距：大标题 -0.4 到 -0.8，正文 0。
- 必须支持 Dynamic Type，最大放大到 AX5。
- 数字使用等宽变体（monospacedDigit）。
- 禁止：花哨字体、艺术字、多字体混排超过 2 种。

## 形状与布局
- 8pt 网格。间距：4/8/12/16/20/24/32/40/48/64。
- 安全区：顶部 59pt（含灵动岛）、底部 34pt。
- 卡片圆角 16–28，按钮 10–14 或胶囊，Sheet 顶部 10–16（连续曲率，避免生硬直角）。
- 列表分组：insetGrouped，左右边距 16–20，组间距 32–36。
- 内容边距：16 或 20。
- 图标：SF Symbols，统一字重（regular/medium/semibold）、尺寸（17/20/24/28）、层级（hierarchical/palette/multicolor）。禁止风格冲突的自绘图标。
- 触控：最小 44x44pt。重要操作拇指可达，提供触觉反馈。
- 布局：安全区、光学对齐、边缘到边缘内容、分组列表、大标题、滚动边缘效果。

## 材质系统

### 材质家族
- **Material**：传统半透明模糊材质，用于建立层级。
- **Vibrancy**：玻璃上的文字/图标效果，让内容从背景中"透出来"。
- **Liquid Glass**（iOS 26+）：新玻璃语言，透镜、折射、边缘高光、自适应染色、交互形变。用于系统级控件与悬浮操作，不用于全屏铺满。

### 材质类型与使用场景
| 材质 | 通透度 | 使用场景 |
|---|---|---|
| ultraThinMaterial | 最通透 | 照片/媒体上的临时控件、短时 HUD。背景必须简单或加 scrim |
| thinMaterial | 轻 | 搜索建议、浮动词、轻量卡片 |
| regularMaterial | 通用 | Sheet、Popover、侧边栏、悬浮卡片 |
| thickMaterial | 低 | 高可读性面板、设置分组、需长时间阅读的浮层 |
| bar / chrome | — | 导航栏、TabBar、工具栏。保证滚动时内容可读 |
| Liquid Glass | 交互式 | 浮动按钮、控制中心、Dynamic Island、系统级操作。支持 morph、press、focus |

### 材质决策树（每次用玻璃前必过）
1. 这个层是否浮在内容之上？否 → 不用毛玻璃。
2. 是否是系统栏？是 → bar / chrome。
3. 是否需要高可读性？是 → regular / thick；否 → thin / ultraThin。
4. 背景是否复杂、明亮、高对比？是 → 加 scrim + vibrancy。
5. 是否 iOS 26+ 且需要交互形变？是 → Liquid Glass。
6. 是否开启 Reduce Transparency？是 → 降级为不透明 systemBackground / secondarySystemBackground。

### 毛玻璃规则
- 一屏最多 1–2 层玻璃；禁止玻璃叠玻璃；只用于浮动层（NavigationBar、TabBar、Toolbar、Sheet、Popover、ContextMenu、Widget、悬浮按钮、搜索栏）。
- 禁止用于：正文背景、大面积滚动内容、低对比文字后面、每行列表都实时模糊。
- 玻璃上文字用 vibrancy 语义色，对比度 ≥4.5:1。
- 圆角连续曲率，外圆角 = 内圆角 + padding。
- 顶部 1px 高光 opacity 0.20–0.40，底部暗边 0.08–0.15；外阴影 y 8–24、blur 24–60、opacity 0.06–0.18；复杂背景加 scrim 黑 0.12–0.28。
- 深色模式玻璃更暗更薄（避免灰雾）；浅色更亮（避免脏灰）。染色只做低饱和 adaptive tint，opacity 0.08–0.16。
- 滚动时导航栏从透明过渡到 bar material；大标题收缩时材质渐显。
- Sheet 上推：背景缩放 0.92–0.96 + 模糊 + 变暗，下拉关闭反向恢复。
- 按压玻璃控件：scale 0.96–0.98、高光增强、轻触觉。Liquid Glass 交互（press/focus/morph/拖拽）必须可中断、可逆。
- 性能：优先系统材质，监控离屏渲染，避免列表每行实时模糊，目标 60/120fps。

## 阴影与层级
- 柔和阴影：y 8–24、blur 24–60、opacity 0.06–0.18。
- 层级用材质、模糊、透明度、视差表达，不用边框。
- 禁止：重投影、粗边框、霓虹。

## 组件规范
- NavigationBar：大标题 + 滚动收缩 + toolbarBackground(.ultraThinMaterial)。
- TabBar：底部固定，图标 + 文字，选中态 tint。
- Sheet：抓取条 + detents + 背景缩放 0.92–0.96 + 模糊变暗。
- Alert：居中卡片 + 毛玻璃 + 双按钮。
- ContextMenu：长按 + 毛玻璃 + 预览缩放。
- List：insetGrouped + 分隔线 + 滑动操作。
- Card：圆角 + 材质 + 柔和阴影。
- Toggle / Segmented / Picker：原生控件优先。
- Widget / Dynamic Island / Live Activity：系统级扩展。

## 转场与动效
- 默认弹簧：response 0.35–0.55 / damping 0.75–0.9。
- 快速交互：response 0.25–0.35 / damping 0.82–0.9。
- Push/Pop：层级滑动 + 轻微淡入/缩放，支持边缘返回手势。
- Sheet：底部上推 + 圆角 + 抓取条 + 背景缩放 + 可下拉关闭 + detents。
- FullScreen：淡入/上推，减少复杂位移。
- Hero / Matched Geometry：共享元素连续变形，Zoom 从卡片到详情。
- 时序：入场 250–400ms，退场 200–300ms，列表错峰 20–50ms。越深层级越慢。
- 物理：速度投射、橡皮筋、阻尼、轻微过冲。必须跟手、可中断、可逆。
- 按压：scale 0.96–0.98，opacity 0.9，配合轻触觉。
- Reduce Motion：降级为淡入淡出或直接切换。

## 特效
- 柔和渐变、Mesh Gradient、玻璃高光、边缘光、低饱和噪点、视差、符号动画。
- 粒子仅用于庆祝或状态，不常驻。
- 性能：优先系统材质，避免列表每行实时模糊，目标 60/120fps。

## 实现要点

### SwiftUI（优先）
- 材质：.ultraThinMaterial / .thinMaterial / .regularMaterial / .thickMaterial / .bar / .chrome。
- 系统栏：.toolbarBackground(.ultraThinMaterial, for: .navigationBar) + .toolbarBackground(.visible, for: .navigationBar)。
- 玻璃容器：RoundedRectangle(cornerRadius: 24, style: .continuous).fill(.regularMaterial)。
- 降级：@Environment(\.accessibilityReduceTransparency) → Color(.secondarySystemBackground)。
- UIKit：UIVisualEffectView + UIBlurEffect(style: .systemThinMaterial) + UIVibrancyEffect。
- iOS 26+：.glassEffect / GlassEffectContainer（以当前 SDK 为准）。

### Compose 映射（Android 项目借用苹果风格时）
| iOS 概念 | Compose 等价物 | 注意 |
|---|---|---|
| Material (ultraThin~thick) | Modifier.blur() 背景 + 半透明 surface 叠加，或 RenderEffect.createBlurEffect（API 31+） | 无系统级 vibrancy；列表项禁止逐行 blur，用预渲染模糊背景图 |
| 语义色 | 自定义 ColorScheme（Material 3），按深浅色各定义一套 label/surface/separator | 用低饱和中性色板模拟 systemGray 系列 |
| SF Pro | 默认 Roboto/SansSerif 或引入可商用近亲字体 | 不内置 SF Pro（版权） |
| SF Symbols | Material Symbols / 自选统一风格图标库，统一字重与尺寸 | 保持单一字重层级 |
| 弹簧动效 | spring(dampingRatio = 0.75–0.9f, stiffness)；response 0.35s ≈ stiffness ≈ 300–350 | animateFloatAsState / AnimatedContent |
| Reduce Motion | 读 Settings.Global.TRANSITION_ANIMATION_SCALE 或 App 内开关 | 降级为 tween(fade) |
| 连续曲率圆角 | 平滑圆角自绘（三次贝塞尔近似 superellipse） | 普通 RoundedCornerShape 也可接受，视还原度要求 |
| Large Title 折叠 | CollapsingTopBar（NestedScrollConnection 自实现） | 滚动时材质渐显 |

### Web / HTML 映射
- Material：backdrop-filter: blur(20px) saturate(1.8) + background: rgba(...) 分层；注意离屏渲染成本，避免大面积/多层嵌套。
- 降级：@media (prefers-reduced-motion: reduce) 关动效；@supports not (backdrop-filter: blur(1px)) 降级为不透明背景。
- 弹簧：CSS transition 用 cubic-bezier(0.32, 0.72, 0, 1) 近似，复杂弹簧用 Web Animations API 或 motion 库。

## 可访问性（默认，不是补丁）
- 深色模式：所有颜色/材质双套定义，玻璃深色下更暗更薄。
- 动态字体：文字尺寸跟随系统设置，不硬编码 pt 固定布局，最大 AX5。
- VoiceOver / TalkBack：每个可交互元素有语义标签，焦点顺序符合视觉顺序。
- Reduce Motion：所有动效可关闭或降级为淡入淡出。
- Reduce Transparency：所有毛玻璃可降级为不透明材质。
- 对比度：正文 ≥ 4.5:1，大字号 ≥ 3:1。

## 禁用
霓虹、重阴影、粗边框、花哨字体、全屏毛玻璃、玻璃叠玻璃、彩色玻璃滥用、玻璃上低对比文字、无意义炫技、忽略 Reduce Transparency。

## 自检清单
- [ ] 是否内容优先？
- [ ] 是否可关闭动效（Reduce Motion 降级）？
- [ ] 触控目标是否 ≥ 44pt？
- [ ] 是否使用语义色？
- [ ] 是否原生（优先系统行为，不发明新交互）？
- [ ] 是否 120fps / 60fps？
- [ ] 毛玻璃是否只用于浮动层？
- [ ] 是否避免玻璃叠玻璃？
- [ ] 可读性是否达标（4.5:1）？
- [ ] 是否所有毛玻璃都能降级为不透明？

## 适用
iOS App、iPadOS、watchOS、macOS、系统级产品、高保真原型；Android 项目可借用审美（用 Compose 映射）。
