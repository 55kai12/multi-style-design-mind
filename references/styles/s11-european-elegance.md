# S11 · 欧式风格（European Elegance）

关键词：中性色、米白/浅灰/深棕、金色点缀、对称、优雅、古典简化。
公理：降噪即高级；克制即奢华；对称即庄重；细节即品质。
决策顺序：庄重基调 → 对称构图 → 细节线框 → 材质（哑光/织物/金属） → 动效（仪式感）。

## 色彩系统
- 米白 #F5F0E8 主。
- 浅灰 #E5E0D8 辅。
- 深棕 #3A2E24 深度。
- 金色 #C9A961 点缀 ≤5%。
- 比例：米白 50%、浅灰 25%、深棕 20%、金 5%。
- 经典三色组合：米白 + 金色 + 深棕（7:2:1）。
- 深色模式：深棕底 + 米白文字 + 金色点缀。
- 禁止：高饱和撞色、霓虹。

## 字体系统
- 标题：衬线体（Cormorant / Playfair Display / Didot）。
- 正文：无衬线（Inter / SF Pro）或衬线。
- 字号：标题 32/40/56pt，正文 16/18pt。
- 字重细腻：标题 Light/Regular，正文 Regular。
- 字间距：标题 1–3，正文 0.5。
- 禁止：粗黑体、花哨字体。

## 形状与布局
- 对称布局。
- 精致线框、适度圆角。
- 简化古典元素（雕花线框简化为细线）。
- 间距：16/24/32/48/64/96。
- 留白充足，庄重感。

## 材质
- 哑光石材纹理、细腻织物感、金属描边。
- 弱毛玻璃可用于现代欧式。
- 避免强反光。
- 禁止：霓虹、重玻璃。

## 阴影
- 柔和：y 8 blur 24 opacity 0.08。
- 禁止：硬阴影、重投影。

## 组件规范
- 按钮：金色描边或深棕填充 + 圆角小。
- 卡片：米白底 + 金色细边。
- 输入框：细线 + 米白底。
- 导航：对称 + 衬线标题。
- 弹窗：圆角 + 金色边。

## 动效
- 优雅缓慢，淡入淡出、轻微缩放、视差。300–600ms。
- 有仪式感但不过度。
- 禁止：生硬、快速、夸张。

## 特效
- 金色微光、织物纹理、石材纹理、淡入淡出。

## 实现要点

### Web / CSS
- 字体：Playfair Display + Cormorant + Inter（Google Fonts 免费商用；Didot 有版权，别嵌入）。
- 金色细线：`border: 1px solid #C9A961;` 双线用伪元素外扩 3px 再画一圈；金属微光 `linear-gradient(90deg, #C9A961, #E5D9A8, #C9A961)` 作分割线背景。
- 织物/石材纹理：低透明纹理图，`opacity ≤ 0.05`，`mix-blend-mode: multiply`。
- 动效：`opacity + scale(0.98 → 1)` 400–600ms ease-out；视差幅度 ≤8px。
- 对称：grid 或 flex 居中构图，装饰线用伪元素补齐左右对称。

### SwiftUI
- 衬线：`.fontDesign(.serif)`（系统衬线近似）或打包 Cormorant 字体文件。
- 金渐变描边：`.overlay(RoundedRectangle(cornerRadius: 8).stroke(LinearGradient(colors: [#C9A961, #E5D9A8, #C9A961], startPoint: .topLeading, endPoint: .bottomTrailing), lineWidth: 1))`。
- 纹理：asset 图 `.opacity(0.05)` + `.allowsHitTesting(false)`。

### Compose 映射
| 概念 | 等价物 | 注意 |
|---|---|---|
| 衬线标题 | FontFamily.Serif 或打包 Cormorant/Playfair（OFL 许可可商用） | — |
| 金渐变描边 | Modifier.border(1.dp, Brush.linearGradient(金三停), shape) | — |
| 双线框 | Box 两层 border（内 1dp 金 + 外 1dp 金，间隔 3dp padding） | — |
| 织物纹理 | 纹理 asset + Image(alpha = 0.05f) | — |
| 动效 | tween(400–600, FastOutSlowInEasing)，scale 0.98→1 | — |

## 可访问性
- 深棕 #3A2E24 on 米白 #F5F0E8 ≈ 11:1 达标。
- **金 #C9A961 on 米白 ≈ 2.3:1 —— 金色只用于装饰线框与细线，禁止作文字色**；金色微光文字效果也禁止（同理）。
- 衬线标题 Light 字重在低分屏易发虚，字号 ≥32pt 才用 Light；正文一律 Regular。
- 动效缓慢有仪式感但必须可跳过：Reduce Motion → 直接渐显；视差幅度 ≤8px 防眩晕。

## 禁用
高饱和撞色、霓虹、粗野主义、过度装饰。

## 自检清单
- [ ] 金色是否 ≤5% 且不作文字色？
- [ ] 是否对称构图（装饰线左右是否补齐）？
- [ ] 古典元素是否简化为细线（无雕花堆砌）？
- [ ] 动效是否可跳过、视差是否 ≤8px？
- [ ] 是否串味（出现高饱和/霓虹/硬阴影 = S4/S9 残留）？

## 适用
奢侈品、高端酒店、珠宝腕表、生活方式品牌、企业官网。
