## HTML

### 什么是语义化，语义化的作用

根据内容的结构化（内容语义化），选择合适的标签（代码语义化）便于开发者阅读和写出更优雅的代码的同时，让浏览器的爬虫和机器跟好地解析。

**作用：**

- 在没有CSS的情况下，页面能很好地呈现内容结构/代码结构；
- 用户体验：比如`title`、`alt`用于给用户解释信息；
- 有利于SEO：爬虫；
- 方便其他设备解析以意义的方式来渲染网页；
- 便于团队开发维护。

### HTML5语义化标签

`header`、`footer`、`hgroup`（多个标题）、`nav`、`aside`（附属信息）、`section`（段）、`article`（文档）、`address`（联系信息）、`time`、`ruby`（注释）、`details`（细节）、`mark`（突出）、`video`（视频）、`audio`（声音）、`canvas`

### HTML5新特性

- 语义化标签
- HTML5表单新元素：`datalist`（定义选项列表）、`keygen`（规定用于表单的密钥对生成器字段，IE不支持）、`output`（定义不同类型的输出）。
表单input新输入类型：`color`、`date`、`datetime`、`datatime-local`、`email`、`month`、`number`、`range`、`search`、`tel`、`time`、`url`、`week`。
- 表单新属性：`placeholder`、`required`、`pattern`、`min`和`max`、`step`、`height`和`width`、`autofocus`、`multiple`。
视频（`video`）和音频（`audio`）
- Canvas
- SVG绘图：可伸缩的矢量图形。
- HTML5 Geolocation（地理位置）：用于定位用户的位置。
- 拖放API
- Web Worker：运行在后台的JavaScript，独立于其他脚本，不会影响页面的性能。
- Web Storage：`localStorage`、`sessionStorage`。
- WebSocket：一种在单个TCP连接上进行全双工通讯的协议。

### SVG与Canvas的区别

**SVG**是一种使用XML描述2D图形的语言。在SVG中，每个被绘制的图形均被视为对象，如果SVG对象的属性发生变化，那么浏览器能够自动重现图形。
**Canvas**通过JavaScript来绘制2D图形。在Canvas中，一旦图形被绘制完成，它就会不会继续得到浏览器的关注。如果位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

### 行内元素和块元素

**行内元素：**只占据它对应标签的边框所包含的空间。只能容纳文本或其他内联元素。
比如：`a`、`abbr`（缩写）、`acronym`（首字）、`b`、`big`（大字体）、`br`、`cite`（引用）、`code`、`dfn`（定义字段）、`em`（强调）、`font`、`i`、`img`、`input`、`kbd`（定义键盘文本）、`label`、`q`、`s`（中划线）、`select`、`small`（小字体文本）、`span`、`strike`（中划线）、`strong`、`sub`（下标）、`sup`（上标）、`textarea`、`tt`（电传文本）、`u`（下划线）。

**块级元素：**占据其父元素（容器）的整个空间，通常浏览器能在块级元素前后另起一行。能容纳其他块元素或者内联元素。
比如：`address`、`blockquote`、`center`（居中对齐块）、`dir`、`div`、`dl`（定义列表）、`fieldset`（form控制组）、`form`、`h1`-`h6`、`hr`、`menu`、`ol`、`ul`、`p`、`pre`（格式化文本）、`table`。
