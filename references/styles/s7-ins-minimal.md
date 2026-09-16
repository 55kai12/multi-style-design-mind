# S7 · Ins Minimal（Instagram 极简风）

关键词：内容优先、黑白灰、留白、圆润、近乎隐形、生活方式。
公理：内容即界面；留白即呼吸；装饰即噪音；照片即主角。
决策顺序：内容（照片/正文） → 留白分区 → 字体层级 → 呈现。无特效层。

## 色彩系统
- 黑白灰为主：#FFFFFF / #FAFAFA / #F5F5F5 / #E0E0E0 / #999999 / #666666 / #000000。
- 至多一个极低饱和提亮色：#F5E6D3（米）、#E8F0E8（淡绿）、#F0E8F0（淡紫）。
- 无渐变、无彩色玻璃。
- 深色模式：#000000 / #1A1A1A / #2A2A2A。

## 字体系统
- 字体族：Montserrat Light / Helvetica Neue / Futura PT / SF Pro。
- 标题：28/36/48pt，字重 Light 或 Bold，字间距 -0.5。
- 正文：15/16pt，Regular，行高 1.6。
- 极简、干净、大量留白。
- 禁止：花哨字体、多字体混排。

## 形状与布局
- 圆角：大圆角 16–24，柔和曲线。
- 间距：16/24/32/48/64。
- 网格：单列或双列，gutter 16–24。
- 留白极大，内容呼吸。
- 图片边到边或大圆角。

## 材质
- 极简，无毛玻璃。
- 靠纯色块和留白建立层级。
- 禁止：玻璃、渐变、噪点。

## 阴影
- 极淡或无。y 4 blur 12 opacity 0.04。
- 禁止：重阴影。

## 组件规范
- 按钮：胶囊或小圆角，纯色或描边。
- 卡片：大圆角 + 无阴影或极淡。
- 输入框：圆角 + 细线。
- 导航：极简 + 大标题。
- 弹窗：圆角 + 纯色。

## 动效
- 克制、快速、淡入 + 微位移，无过冲。150–300ms。
- 禁止：夸张动效、粒子、视差。

## 特效
- 无。最多淡入淡出。

## 实现要点（三平台实现成本都极低）

### SwiftUI
- 系统原生控件即可：`List` / `ScrollView` + `LazyVGrid`。
- 颜色：`Color(white: 0.98)` 系列灰阶；唯一提亮色定义一次全局引用。
- 字体：`.system(size: 36, weight: .light)` 标题 + `.kerning(-0.5)`。
- 动效：`.animation(.easeOut(duration: 0.2), value: ...)`，opacity + offset 8px。

### Compose 映射
| 概念 | 等价物 | 注意 |
|---|---|---|
| 大圆角卡片 | RoundedCornerShape(20.dp) + 纯色 surface | 无阴影 |
| 轻字重标题 | FontWeight.Light(300) | 中文配思源黑体 Light |
| 双列网格 | LazyVerticalGrid(GridCells.Fixed(2), horizontalArrangement 16.dp) | gutter 16–24 |
| 动效 | tween(200, FastOutSlowInEasing) fade + slide 8dp | 无过冲 |

### Web / CSS
- 单列/双列 grid；图片 `aspect-ratio` 固定防布局抖动；`object-fit: cover`。
- 字体：Montserrat（Google Fonts 免费）或系统字体栈。
- 图片懒加载 + 明确宽高，加载中用灰占位块（#F5F5F5）。

## 可访问性
- 黑白灰对比天然达标：#666 on #FFF ≈ 5.7:1 起步。
- 提亮色底（#F5E6D3）配黑字 ≈ 13:1 安全；**禁止浅底配浅字**。
- 图片全部提供内容描述（alt / accessibilityLabel）——照片即主角，主角必须可被读出。
- Reduce Motion：淡入改直接显示即可。

## 禁用
重色块、复杂纹理、多色强调、夸张动效、拥挤布局。

## 自检清单
- [ ] 提亮色是否至多一个？
- [ ] 留白是否充足（宁多勿少）？
- [ ] 是否零阴影零纹理（出现玻璃/渐变 = S3 残留）？
- [ ] 照片是否是绝对主角、是否有可访问描述？
- [ ] 是否串味（出现重阴影/彩色 = 残留）？

## 适用
社交、内容阅读、电商展示、生活方式 App、摄影产品。
