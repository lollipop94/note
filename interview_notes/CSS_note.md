## CSS

### 盒模型（box-sizing）

一个盒子有margin、border、padding、content。

- IE盒模型（border-box）：width = content + padding + border
- W3C标准盒模型（content-box）：width = content

### position

- static：默认值，无定位，元素处于正常流中。
- absolute：绝对定位，相对于static定位以外的第一个父元素定位。
- relative：相对定位，相对于其正常位置定位。
- fixed：固定定位，相对于浏览器窗口定位。

### display

指定用于元素的呈现框的类型。

- none：元素不会占据空间，无法显示，相当于该元素不存在。
- block：块级元素，如果不指定宽高，默认会继承父元素的宽度，并且独占一行，高度一般以子元素撑开的高度为准。
- inline：行内元素，设置高度、宽度、`text-align`无效。
- inline-block：既有`block`的宽高特性又有`inline`的同行元素特性。
- list-item：列表显示。
- table：表格。
- flex：弹性布局。

### 浮动

脱离标准流，漂浮在标准流上，周围元素对其环绕。
父级元素height被忽略，会出现高度塌陷的现象。

**清除浮动的方法：**

- 在浮动元素后使用一个空元素如`<div class=‘clear’></div>`，设置`.clear { clear: both; }`即可；
- 给父级元素定义高度；
- 让父级元素也浮动；
- 将父级元素设置为BFC（`display: table;` / `overflow: hidden;`）；
- clearfix，使用内容生成的方式清除浮动：

```
.clearfix:after { /* :after选择器向选定的元素之后插入内容 */
	content: “”; /* 生成内容为空 */
	display: block; /* 块级元素显示 */
	clear: both; /* 清除前面的内容 */
}
```

### BFC（Block Formatting Context，块格式化上下文）

A block formatting context contains everything inside of the element creating it that is not also inside a descendant element that creates a new block formatting context. 
BFC是一个隔离的容器，将BFC内部元素与外部元素相互隔离，使内外元素的定位不会相互影响。

**BFC的创建条件（以下其一即可）：**

- 根元素或其他包含它的元素；
- 浮动（元素的`float`不为`none`）；
- 元素的position不为`static`或`relative`（`position`为`absolute`或`fixed`）；
- 行内块（inline-blocks）（`display: inline-block;`）；
- 表格单元格（`display: table-cell;`）；
- `overflow`的值不为`visible`的元素（`overflow: hidden;`）；
- 弹性盒flex boxes（`display`为`flex`或`inline-flex`）。

**BFC的特点：**

- 内部的盒在垂直方向上一个接一个排列；
- 处于同一个BFC中的元素相互影响（可能会发生margin collapse）；
- 每个元素的margin box的左边，与容器块border box的左边相接触，浮动也是如此；
- BFC是一个隔离的独立容器，容器里的子元素不会影响到外面的元素，反之亦然；
- 计算BFC高度时，考虑BFC做包含的所有元素（包括浮动元素）；
- 浮动盒区域不会叠加到BFC上。

**BFC的用处：**

- 消除Margin Collapse：让产生margin collapse的两个元素分别属于不同的BFC即可；
- 容纳浮动元素：假设一个容器里有浮动元素，但容器高度为0，可以将该容器实现BFC，或者利用伪元素清除浮动；
- 阻止文本换行：假设文本环绕浮动元素，可以讲margin-left设置为浮动盒的宽度，或者为文本元素建立BFC。

### CSS选择器优先级（权重）

**选择器：**ID选择器、类选择器、标签选择器、通配选择器、组合选择器、后代选择器、群组选择器、继承选择器、伪类选择器、子选择器、相邻兄弟选择器
**优先级：**!important > 行内样式 > ID选择器 > 类选择器 > 标签选择器 > 通配符 > 继承 > 浏览器默认

### CSS3新特性

- `border-radius` 圆角
- `box-sizing` 盒模型计算方式
- `@font-face` 字体
- `box-shadow`、`text-shadow` 框和文本的阴影
- `gradient` 线性渐变
- `transform` 旋转
- `scale` 缩放
- `translate` 定位
- `skew` 倾斜
- `border-image`
- `rgba`
- `::selection`


### 伪元素、伪类

**伪元素：**用于向某类选择器添加特殊的效果。有：:first-letter、:first-line、:before、:after。
**伪类：**用于将特殊的效果添加到某些选择器。有：:active、:focus、:hover、:link、:visited、:first-child、:lang。

### CSS新增伪类元素

`:nth-child`、`:after`、`:before`、`:checked`、`:disable`

### CSS动画

**transition：**`transition: property duration timing-function delay;`

- property：应用过渡CSS属性的名称。
- duration：过渡效果花费的时间，默认0。
- timing-function：过渡效果的时间曲线，ease（默认，逐渐放慢）、linear（匀速）、ease-in（加速）、ease-out（减速）、cubic-bezier函数（自定义速度模式）。
- delay：过渡效果何时开始，默认为0。

**animation：**`animation: name duration timing-function delay iteration-count direction fill-mode play-state;`

- name：要绑定到选择器的关键帧的名称。
- duration：指定动画需要多少秒或毫秒完成。
- timing-function：动画将如何完成一个周期。
- delay：动画在启动前的延迟间隔。
- iteration-count：动画的播放次数。
- direction：是否应该轮流反向播放动画。
- fill-mode：当动画不播放时，要应用到元素的样式。
- play-state：动画是否正在运行或已暂停。
- transform、transition、animation

**transform**描述了元素的静态样式，不会更改元素或它周围的元素的布局，会对元素的整体产生影响，会对整个元素进行缩放、旋转、移动处理。
transition和animation都可以实现动画效果。

**transition和animation的不同：**

- 触发条件：transition由事件触发（过渡，由属性变化而触发），比如hover；animation无需事件触发，立即播放（关键帧动画）。
- 循环：animation可设定循环次数。
- 精确性：animation可设定每一帧的样式和时间；transition只设定头和尾。
- 与js交互：animation与js交互不是很紧密；transition动画+js设定变化样式。

### rem、em、%

- rem：相对于根元素html的font-size进行计算。
- em：相对于父元素的font-size进行计算。
- %：相对于父元素的百分值。

### vw、vh

- vm：viewpoint width，视窗宽度。
- vh：viewpoint height，视窗高度。

### flex布局（弹性布局）

- Flex容器：父元素设置`display: flex;`（水平的主轴，垂直的交叉轴）。
- Flex项目：Flex容器内的子元素。

**容器的属性：**

- flex-direction：主轴的方向，row / row-reverse / column / column-reverse
- flex-wrap： 如果一条轴线排不下，如何换行，nowrap / wrap（第一行在上方） / wrap-reverse（第一行在下方）
- flex-flow：flex-direction || flex-wrap
- justify-content：项目在主轴上的对齐方式，flex-start（左对齐） / flex-end（右对齐） / center / space-between（两端对齐） / space-around（每个项目两侧间隔相等）
- align-items：项目在交叉轴上如何对齐，flex-start / flex-end / center / baseline（项目第一行文字基线对齐） / stretch（未设置高度或设为auto，将占满高度）

**项目的属性：**

- order：项目的排列顺序，integer，数字越小，排列越靠前，默认为0。
- flex-grow：项目的放大比例，默认为0。
- flex-shrink：项目的缩小比例，默认为1。
- flex-basis：在分配多余空间之前，项目占据的 主轴空间，默认为auto。
- flex：flex-grow || flex-shrink || flex-basis
- align-self：允许单个项目有与其他项目不一样的对齐方式，auto / flex-start / flex-end / center / baseline / stretch

### 布局

#### 水平居中

1）文本/行内元素/行内块级元素：（子元素宽度大于父元素宽度时无效）

```
.parent {
	text-align: center;
}
```

2）单个块级元素：（前提：定宽）

```
.child {
	margin: 0 auto;
}
```

3）多个块级元素：

```
.parent {
	text-align: center;
}
.child {
	display: inline-block;
}
```

4）利用绝对定位实现：

对于子元素，`top`、`bottom`、`left`、`right`的值相对于父元素，`margin`、`transform`的值相对于自身。

5）flex布局：
```
.parent {
	display: flex;
	justify-content: center;
}
```

#### 垂直居中

1）单行文本/行内元素/行内块级元素：

将父元素的height与line-height值设为一样的。

2）多行文本/行内元素/行内块级元素：

- 用span标签包裹多行文本，设置`display: inline-block;`；
- 设置父元素的height和line-height，其中，line-height的值为height/5。

3）图片：

将父元素的height与line-height的值设为一样 ，且`font-size: 0;`（实现完全居中），同时，`.child { vertical-align: middle; }`。

4）单个块级元素：

利用table-cell实现：

```
.parent {
	display: table-cell;
	vertical-align: middle;
}
```

使用绝对定位：

```
.parent {
	position: relative;
}
.child {
	position: absolute;
	transform: translateY(-50%);
}
```

flex：

```
.parent {
	display: flex;
	align-items: center;
}
```

5）任意元素：flex布局（3种）

a）

```
.parent {
	display: flex;
	align-items: center;
}
```

b）

```
.parent {
	display: flex;
}
.child {
	align-self: center;
}
```

c）

```
.parent {
	display: flex;
	flex-direction: column;
	justify-content: center;
}
```

#### 水平垂直居中

1）行内/行内块级/图片：

```
.parent {
	/* height与line-height的值一样 */
	text-align: center;
	font-size: 0;
}
.child {
	display: inline-block; /* 块级元素需设为行内元素才生效 */
	vertical-align: middle;
}
```

2）table-cell：

```
.parent {
	display: table-cell;
	vertical-align: middle;
	text-align: center; /* 行内添加 */
}
.child {
	margin: 0 auto;
}
```

3）button作为父元素：

```
button { /* 改掉button默认样式 */
	outline: none;
	border: none;
}
.child { /* 居中元素表示形式改为行内 */
	display: inline-block;
}
```

4）绝对定位：

```
.parent {
	position: relative;
}
.child {
	position: absolute;
	transform: translate(-50%, -50%);
}
```

5）flex：

```
.parent {
	display: flex;
	justify-content: center;
	align-items: center;
}
```

#### 两列布局

1）左列定宽，右侧自适应：

- float+margin
- float+overflow
- table
- 绝对定位
- flex
- Grid（grid-template-columns）

2）一列不定，一列自适应：

- float+overflow
- flex
- Grid

#### 三列布局

1）两列定宽，一列自适应：

- float+margin
- float+overflow
- table
- flex
- Grid

2）两侧定宽，中间自适应：

- 双飞翼布局：在中间盒子里再加一个子盒子，设置这个子盒子的margin值来让出空位。
- 圣杯布局：设置父盒子padding值为左右盒子留出空间，让中间盒子宽度100%占满，使用margin负值将左右两个盒子拉回同一高度。
- Grid
- table
- flex
