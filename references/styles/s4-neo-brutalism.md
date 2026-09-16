# S4 · Neo-Brutalism（新粗野主义）

关键词：粗黑边、硬阴影、高饱和、贴纸感、故意不精致、态度。
公理：冲突即张力；直白即态度；规则即用来打破；不完美即真实。
决策顺序：信息 → 高饱和色块分区 → 粗边框定义边界 → 硬阴影制造深度 → 动效。

## 色彩系统
- 高饱和撞色：黄 #FFE600、黑 #000000、粉 #FF2D95、青 #00E5FF、绿 #00FF88、橙 #FF6B00。
- 纯色无渐变。
- 比例：黑 40%、白 20%、主色 30%、辅色 10%。
- 深色模式：保持高饱和，背景换深灰 #1A1A1A。

## 字体系统
- 字体族：超粗无衬线（Archivo Black / Space Grotesk / Inter Black）或等宽（JetBrains Mono / Space Mono）。
- 字号：标题 40/56/72pt，正文 16/18pt。
- 字重：900 或 Bold。
- 允许全大写、字间距 1–2。
- 禁止：细字重、衬线、优雅字体。

## 形状与布局
- 圆角：0–8。
- 边框：2–4px 纯黑。
- 间距：8/16/24/32/48。
- 布局可故意错位、重叠、倾斜 1–3°。
- 网格可打破。

## 材质
- 无毛玻璃。
- 可用半调网点、贴纸、像素纹理、手绘涂鸦。
- 背景纯色或粗网格。

## 阴影
- 硬阴影，无模糊，offset 4–8px，纯黑。
- 禁止：柔和阴影、渐变。

## 组件规范
- 按钮：粗黑边 + 硬阴影 + hover 位移。
- 卡片：粗黑边 + 硬阴影 + 贴纸感。
- 输入框：粗黑边 + 纯色底。
- 导航：粗黑边 + 高饱和。
- 弹窗：粗黑边 + 硬阴影。

## 动效
- 生硬、快速、位移式。80–200ms，linear 或强弹簧。
- 允许错位、抖动、色块翻转。
- 禁止：柔和过渡、缓慢动画。

## 特效
- 描边偏移、hover 位移、色块翻转、半调网点。

## 实现要点

### Web / CSS（本风格最自然）
- 边框：`border: 3px solid #000; border-radius: 0–8px;`
- 硬阴影：`box-shadow: 6px 6px 0 #000;`（**无 blur**）
- hover 位移（按压感）：`transform: translate(2px, 2px); box-shadow: 2px 2px 0 #000;`
- 字体：Archivo Black / Space Grotesk（Google Fonts 免费商用）。
- 半调网点：`background-image: radial-gradient(#000 1px, transparent 1px); background-size: 6px 6px; opacity: 0.1;`
- 动效：`transition: transform 0.12s linear;`

### SwiftUI
- 粗边：`.overlay(RoundedRectangle(cornerRadius: 4).stroke(Color.black, lineWidth: 3))`。
- 硬阴影：系统 `.shadow` 带 blur 不可用——用 `.background(Color.black.offset(x: 6, y: 6))` 叠层模拟。
- 动效：`.animation(.linear(duration: 0.12))` 或 `.spring(response: 0.2, dampingFraction: 0.5)` 强弹簧。

### Compose 映射
| 概念 | 等价物 | 注意 |
|---|---|---|
| 粗黑边 | Modifier.border(3.dp, Color.Black, RoundedCornerShape(4.dp)) | — |
| 硬阴影 | drawBehind 画偏移 6.dp 纯黑圆角矩形；或 Box 叠层偏移 | 别用 elevation/shadow（带 blur） |
| 色块翻转 | AnimatedContent + tween(120, LinearEasing) | — |
| 倾斜错位 | Modifier.graphicsLayer { rotationZ = -2f } | ≤3° |
| 半调网点 | 纹理图 asset 或 Canvas 画点阵 | — |

## 可访问性
- 高饱和组合要抽检：黄 #FFE600 底配黑字 ≈ 14:1 安全；**黄底白字、白底黄字禁止**。
- 动效快速生硬仍必须提供 Reduce Motion 降级：位移动画改为直接切换状态。
- 错位倾斜 ≤3° 且不遮挡点击区；触控目标 ≥44pt，不因贴纸感缩小。
- 全大写文字配 letter-spacing 1–2 保证可读，长段落禁用全大写。

## 禁用
柔和阴影、细腻渐变、精致毛玻璃、低饱和、优雅字体。

## 自检清单
- [ ] 阴影是否全部无模糊、纯黑、offset 4–8px？
- [ ] 边框是否 2–4px 纯黑？
- [ ] 是否零渐变零玻璃（出现 soft shadow / blur = S1/S3 残留）？
- [ ] 倾斜错位是否 ≤3° 且不遮挡触控？
- [ ] Reduce Motion 降级是否存在？
- [ ] 文字对比是否逐组合实测？

## 适用
创意机构、活动页、潮牌、独立产品、Z世代品牌。
