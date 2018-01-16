# 前端编码指南

## 原则

不管有多少人共同参与同一项目，确保每一行代码都像同一个人编写的。

## 命名规则

### 项目命名

全部采用小写方式，多个单词组成时，以中划线分隔。
例：`flagwind-core`、`flagwind-web`

### 目录命名

参照项目命名规则，有复数结构时，采用复数命名法。
例：`config`、`components`、`styles`、`assets`、`models`

### 文件命名

参照项目命名规则。
例：`settings.vue`、`account-model.js`、`retina-sprites.less`

## HTML

### 语法

- 使用4个空格代替 tab 缩进
- 嵌套标签应当另起一行并缩进一次（`head` 和 `body` 标签不需要缩进）
- 在大的模块之间用空行隔开，使模块更清晰
- 在模块之间采用 `<!--XXX BEGIN--> <!--XXX END-->` 包裹起来
- 在属性上，确保全部使用双引号，而不是单引号
- 属性名全小写，用中划线做分隔符
- 确保在自闭合标签的尾部添加斜线（例：`<img />` 或 `<input />`）
- 脚本文件应在 `</body>` 的前一行引入

``` html
<!DOCTYPE html>
<html lang="zh-hans">
<head>
    <meta charset="utf-8" />
    <meta name="renderer" content="webkit" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    
    <title>Untitled</title>
    <meta name="description" content="" />
    <meta name="keywords" content="" />
    
    <!-- CSS 文件 -->
    <link rel="stylesheet" href="styles/layout.css" />
</head>

<body>
    <div class="container">
        <!-- 公共头部 BEGIN -->
        <header>
            <h1>网页标题...</h1>
        </header>
        <!-- 公共头部 END -->
    </div>
    
    <!-- JavaScript 文件 -->
    <script src="scripts/vue.js"></script>
</body>
</html>
```

### DOCTYPE

为每个 HTML 页面的第一行添加标准模式的声明，这样能够确保在每个浏览器中拥有一致的展现。

``` html
<!DOCTYPE html>
```

### 语言属性

根据 HTML5 规范：

*强烈建议为 html 根元素指定 lang 属性，从而为文档设置正确的语言。这将有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等。*

这里列出了[语言代码表](http://www.sitepoint.com/web-foundations/iso-2-letter-language-codes/)。

``` html
<!DOCTYPE html>
<html lang="zh-hans">
</html>
```

### 字符编码

通过声明一个明确的字符编码，让浏览器轻松、快速的确定适合网页内容的渲染方式，通常指定为`utf-8`。

``` html
<meta charset="utf-8" />
```

### IE 兼容模式

IE 通过特定的 `<meta>` 标签来确定渲染页面所采用的版本；
如果你想要了解更多，请点击[这里](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do)；
不同 doctype 在不同浏览器下会触发不同的渲染模式（[这篇文章](https://hsivonen.fi/doctype/)总结的很到位）；
除非有强烈的特殊需求，否则最好设置为 **Edge** 模式，从而通知 IE 采用其所支持的最新的模式。

``` html
<meta http-equiv="X-UA-Compatible" content="IE=Edge" />
```

### 引入 CSS 和 JavaScript 文件

根据 HTML5 规范，在引入 CSS 和 JavaScript 文件时不需要指定 type 属性，因为 `text/css` 和 `text/javascript` 分别是它们的默认值。

HTML5 规范链接：

- [使用 link](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
- [使用 style](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)
- [使用 script](http://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)

``` html
<!-- 引入外部样式表 -->
<link rel="stylesheet" href="styles/layout.css" />

<!-- 内部样式表 -->
<style>
    /* ... */
</style>

<!-- 引入外部脚本 -->
<script src="scripts/vue.js"></script>

<!-- 内部脚本 -->
<script>
    ...
</script>
```

### 属性顺序

属性应该按照特定的顺序出现以保证易读性；

- `class`
- `id`
- `name`
- `data-*`
- `src`, `for`, `type`, `href`, `value`, `max-length`, `max`, `min`, `pattern`
- `placeholder`, `title`, `alt`
- `aria-*`, `role`
- `required`, `readonly`, `disabled`

class 是为高可复用组件设计的，所以应处在第一位；  
id 更加具体且应该尽量少使用，所以将它放在第二位。

``` html
<a class="..." id="..." data-modal="toggle" href="#">Example link</a>

<input class="form-control" type="text" />

<img src="..." alt="..." />
```

### 布尔属性

布尔型属性可在声明时不赋值（XHTML 规范要求为其赋值，但是 HTML5 规范不需要）；  
建议采用 **属性值=属性名** 的方式赋值；  
了解更多内容，请参考 [WhatWG section on boolean attributes](http://www.whatwg.org/specs/web-apps/current-work/multipage/common-microsyntaxes.html#boolean-attributes)。

``` html
<!-- 不写属性代表属性为false -->
<input type="checkbox" />

<!-- 属性值=属性名，代表属性为true -->
<input type="checkbox" checked="checked" />

<select>
    <option value="1" selected="selected">1</option>
</select>
```

### 减少标签数量

编写 HTML 代码时，尽量避免多余的父元素；  
很多时候，这需要迭代和重构来实现。

``` html
<!-- 糟糕的实例 -->
<span class="avatar">
    <img src="..." />
</span>

<!-- 好的实例 -->
<img class="avatar" src="..." />
```

### HTML语义化

选择合适的语义化标签，便于开发者阅读，同时能让浏览器和搜索引擎更好的解析；

- 少用无语义的 `div` 和 `span` 标签
- 使用 `h1-h6` 定义页面对应级别的标题
- 在语义不明显时，既可以使用 `div` 或 `p` 时，尽量使用 `p` 标签
- 不要使用纯样式或已过时的标签，如：`b`、`font`、`u`、`center`、`strike` 等
- 需要强调的文本包含在 `strong` 或 `em` 标签中
- 使用表格时，标题使用 `caption`，表头使用 `thead`，主体内容使用 `tbody`，尾部使用 `tfoot`，表头单元格使用 `th`，内容单元格使用 `td`
- 表单域使用 `fieldset` 包裹起来，并使用 `legend` 标签说明表单的用途
- 每个 `input` 标签对应的说明都应该使用 `label` 标签，并为 `input` 设置 `id` 属性，在 `label` 中设置 `for` 属性使说明和 `input` 关联起来
- 不要省略某些标签的的属性，如： `img` 标签的 `alt` 属性，`a` 标签的 `title` 属性
- 任何时候都要用尽量小的复杂度和尽量少的标签来解决问题

[这里](http://www.csszengarden.com/)有一个很好的文档结构供大家参考。

## CSS

### 缩进

使4个空格代替 tab。

``` css
.element
{
    position: absolute;
    top: 10px;
    left: 10px;

    width: 50px;
    height: 50px;

    border-radius: 10px;
}
```

### 分号

所有声明语句都应当以分号结尾，包括最后一条语句。

``` css
.element
{
    width: 20px;
    height: 20px;

    background-color: red;
}
```

### 空格

以下几种情况需要空格

- 声明值前，即 `:` 后，例： `width: 50px`
- 选择器 `>`、`+`、`~` 前后，例：`header > h1`
- `!important` 前，例：`color: red !important`
- 属性值中的 `,` 后，例：`background-color: rgba(0, 0, 0, .5)`
- 注释 `/*` 后和 `*/` 前，例：`/* 头部导航 */`

以下几种情况不需要空格

- 属性名后
- 多个规则的分隔符 `,` 前
- `!important` 的 `!` 后
- 属性值中 `(` 后和 `)` 前
- 行末不要有多余的空格

``` css
/* 糟糕的实例 */
.element{
    color :red! important;
    background-color: rgba(0,0,0,.5);
}

/* 好的实例 */
.element
{
    color: red !important;
    background-color: rgba(0, 0, 0, .5);
}

/* 糟糕的实例 */
.element ,
.dialog{
    ...
}

/* 好的实例 */
.element,
.dialog
{
    ...
}

/* 糟糕的实例 */
.element>.dialog{
    ...
}

/* 好的实例 */
.element > .dialog
{
    ...
}

/* 糟糕的实例 */
@if{
    ...
}@else{
    ...
}

/* 好的实例 */
@if
{
    ...
}
@else
{
    ...
}
```

### 空行

以下几种情况需要空行：

- 文件最后保留一个空行
- 声明块的右花括号 `}` 后最好跟一个空行，包括 scss 中嵌套的规则
- 属性之间需要适当的空行，具体见属性声明顺序

``` css
/* 糟糕的实例 */
.element {
    ...
}
.dialog {
    color: red;
    &:after {
        ...
    }
}

/* 好的实例 */
.element
{
    ...
}

.dialog
{
    color: red;

    &:after
    {
        ...
    }
}
```

### 换行

- 在左大括号 `{` 和右大括号 `}` 前后换行
- 每条声明都应该独占一行
- 多个规则的分隔符 `,` 后换行
- 为选择器分组时，将单独的选择器单独放一行

``` css
/* 糟糕的实例 */
.element
{color: red; background-color: black;}

/* 好的实例 */
.element
{
    color: red;
    background-color: black;
}

/* 糟糕的实例 */
.element, .dialog {
    ...
}

/* 好的实例 */
.element,
.dialog
{
    ...
}
```

### 注释

代码是由人编写并维护的，请确保你的代码能够自然描述、注释良好并且易于他人理解；
好的代码注释能够传达上下文关系和代码目的，不要简单地重声明组件或 class 名称；
对于较长的注释，务必书写完整的句子，对于一般性注解，可以书写简洁的短语。

``` css
/* 糟糕的实例 */

/*
 * Modal header
 */
.modal-header
{
    ...
}

/* 好的实例 */

/*
 * 包含标题和关闭操作的容器。
 */
.modal-header
{
    ...
}
```

### 引号

最外层统一使用双引号；  
url 内容要用引号；  
属性选择器中的属性值需要引号。

``` css
.element:after
{
    content: "";
    background-image: url("images/logo.png");
}

input[type="number"]
{
    ...
}
```

### 命名

- 类名使用小写字母，以中划线分隔
- id 采用驼峰式命名（首字母小写）
- scss 中的变量、函数、混合、placeholder 采用驼峰式命名
- 避免过度任意的简写，如：`.s` 不能表达任何意思
- 基于最近的父 class 或基本（base）class 作为新 class 的前缀
- 使用 `.js-*` class 来标识行为（与样式相对），并且不要将这些 class 包含到 CSS 文件中

``` css
/* class */
.element-content
{
    ...
}

/* id */
#loginDialog
{
    ...
}

/* 变量 */
$colorBlack: #000;

/* 函数 */
@function pxToRem($px)
{
    ...
}

/* 混合 */
@mixin centerBlock
{
    ...
}

/* placeholder */
%loginDialog
{
    ...
}
```

### 代码组织

- 以组件为单位组织代码段
- 制定一致的注释规范
- 使用一致的空白符将代码分隔成块，这样利于阅读较大的文档
- 如果使用了多个 CSS 文件，将其按照组件而非页面的形式分拆，因为页面会被重组，而组件只会被移动

``` css
/*
 * Component section heading
 */

.element { ... }


/*
 * Component section heading
 *
 * Sometimes you need to include optional context for the entire component.
 * Do that up here if it's important enough.
 */

.element { ... }

/*
 * Contextual sub-component or modifer
 */

.element-heading { ... }
```

### 选择器

- 对于通用元素使用 class ，这样利于渲染性能的优化
- 对于经常出现的组件，避免使用属性选择器（例如：`[class^="..."]`）
- 选择器要尽可能短，并且尽量限制组成选择器的元素个数，建议不要超过 3 个
- 只有在必要的时候才将 class 限制在最近的父元素内（也就是后代选择器）

扩展阅读:

- [Scope CSS classes with prefixes](http://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/)
- [Stop the cascade](http://markdotto.com/2012/03/02/stop-the-cascade/)

``` css
/* 糟糕的实例 */
span { ... }
.container #stream .stream-item .header .username { ... }
.avatar { ... }

/* 好的实例 */
.header .username { ... }
.header .avatar { ... }
```

### 属性声明顺序

相关的属性声明应当归为一组，并按照下面的顺序排列：

1. Positioning（定位）
2. Box model（盒模型）
3. Typographic（排版）
4. Visual（外观）

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在第一位。盒模型紧跟其后，因为他决定了一个组件的尺寸和位置。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，所以他们排在后面。

关于完整的属性以及他们的顺序，请参考 [Recess](http://twitter.github.io/recess/)。

``` css
.declaration-order
{
    /* 定位 */
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 100;

    /* 盒模型 */
    display: block;
    float: right;
    width: 100px;
    height: 100px;

    /* 排版 */
    font: normal 13px "Helvetica Neue", sans-serif;
    line-height: 1.5;
    color: #333;
    text-align: center;

    /* 外观 */
    background-color: #f5f5f5;
    border: 1px solid #e5e5e5;
    border-radius: 3px;

    /* 其他 */
    opacity: 1;
}

```

为了方便查阅，我们将 Recess 的顺序贴了一份出来：

``` js
"position",
"top",
"right",
"bottom",
"left",
"z-index",
"display",
"float",
"width",
"height",
"max-width",
"max-height",
"min-width",
"min-height",
"padding",
"padding-top",
"padding-right",
"padding-bottom",
"padding-left",
"margin",
"margin-top",
"margin-right",
"margin-bottom",
"margin-left",
"margin-collapse",
"margin-top-collapse",
"margin-right-collapse",
"margin-bottom-collapse",
"margin-left-collapse",
"overflow",
"overflow-x",
"overflow-y",
"clip",
"clear",
"font",
"font-family",
"font-size",
"font-smoothing",
"osx-font-smoothing",
"font-style",
"font-weight",
"hyphens",
"src",
"line-height",
"letter-spacing",
"word-spacing",
"color",
"text-align",
"text-decoration",
"text-indent",
"text-overflow",
"text-rendering",
"text-size-adjust",
"text-shadow",
"text-transform",
"word-break",
"word-wrap",
"white-space",
"vertical-align",
"list-style",
"list-style-type",
"list-style-position",
"list-style-image",
"pointer-events",
"cursor",
"background",
"background-attachment",
"background-color",
"background-image",
"background-position",
"background-repeat",
"background-size",
"border",
"border-collapse",
"border-top",
"border-right",
"border-bottom",
"border-left",
"border-color",
"border-image",
"border-top-color",
"border-right-color",
"border-bottom-color",
"border-left-color",
"border-spacing",
"border-style",
"border-top-style",
"border-right-style",
"border-bottom-style",
"border-left-style",
"border-width",
"border-top-width",
"border-right-width",
"border-bottom-width",
"border-left-width",
"border-radius",
"border-top-right-radius",
"border-bottom-right-radius",
"border-bottom-left-radius",
"border-top-left-radius",
"border-radius-topright",
"border-radius-bottomright",
"border-radius-bottomleft",
"border-radius-topleft",
"content",
"quotes",
"outline",
"outline-offset",
"opacity",
"filter",
"visibility",
"size",
"zoom",
"transform",
"box-align",
"box-flex",
"box-orient",
"box-pack",
"box-shadow",
"box-sizing",
"table-layout",
"animation",
"animation-delay",
"animation-duration",
"animation-iteration-count",
"animation-name",
"animation-play-state",
"animation-timing-function",
"animation-fill-mode",
"transition",
"transition-delay",
"transition-duration",
"transition-property",
"transition-timing-function",
"background-clip",
"backface-visibility",
"resize",
"appearance",
"user-select",
"interpolation-mode",
"direction",
"marks",
"page",
"set-link-source",
"unicode-bidi",
"speak"
```

### 颜色

- 十六进制值应该全部小写，例如：`#abcdef`
- 使用简写形式的十六进制值，例如：用 `#fff` 代替 `#ffffff`

``` css
/* 糟糕的实例 */
.element
{
    color: #ABCDEF;
    background-color: #001122;
}

/* 好的实例 */
.element
{
    color: #abcdef;
    background-color: #012;
}
```

### 属性简写

在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

- `padding`
- `margin`
- `font`
- `background`
- `border`
- `border-radius`

大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

Mozilla Developer Network 有一篇对不熟悉属性简写及其行为的人来说很棒的关于 [shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) 的文章。

``` css

/* 糟糕的实例 */
.element
{
    margin: 0 0 10px;
    background: red;
    background: url("image.jpg");
    border-radius: 3px 3px 0 0;
}

/* 好的实例 */
.element
{
    margin-bottom: 10px;
    background-color: red;
    background-image: url("image.jpg");
    border-top-left-radius: 3px;
    border-top-right-radius: 3px;
}

```

### 媒体查询

尽量将媒体查询的规则靠近与他们相关的规则，不要将他们一起放到一个独立的样式文件中，或者丢在文档的最底部，这样做只会让大家以后更容易忘记他们。

``` css
.element
{
    ...
}

.element-avatar
{
    ...
}

@media(min-width: 480px)
{
    .element
    {
        ...
    }

    .element-avatar
    {
        ...
    }
}
```

### 带前缀的属性

- 同个属性不同前缀的写法需要在垂直方向保持对齐，具体参照下边的写法
- 无前缀的标准属性应该写在有前缀的属性后面

``` css
.element
{
    -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, .15);
            box-shadow: 0 1px 2px rgba(0, 0, 0, .15);
}
```

### 其他

- 不允许有空的规则
- 元素选择器用小写字母
- 对于属性值或颜色参数，省略小于 1 的小数前面的 0，例如：`.5` 代替 `0.5`；`-.5px` 代替 `-0.5px`
- 避免为 0 值指定单位，例如：用 `margin: 0` 代替 `margin: 0px`
- 不要在同个规则里出现重复的属性，如果重复的属性是连续的则没关系
- 不要在一个文件里出现两个相同的规则
- 用 `border: 0` 代替 `border: none`
- 发布的代码中不要有 `@import`
- 尽量少用 `*` 选择器

更多规则请参考 Wikipedia 中的 [CSS语法部分](http://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax)

``` css
/* 糟糕的实例 */
.element
{
}

/* 糟糕的实例 */
LI
{
    ...
}

/* 好的实例 */
li
{
    ...
}

/* 糟糕的实例 */
.element
{
    color: rgba(0, 0, 0, 0.5);
}

/* 好的实例 */
.element
{
    color: rgba(0, 0, 0, .5);
}

/* 糟糕的实例 */
.element
{
    width: 50.0px;
}

/* 好的实例 */
.element
{
    width: 50px;
}

/* 糟糕的实例 */
.element
{
    width: 0px;
}

/* 好的实例 */
.element
{
    width: 0;
}

/* 糟糕的实例 */
.element
{
    border-radius: 3px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;

    background: linear-gradient(to bottom, #fff 0, #eee 100%);
    background: -webkit-linear-gradient(top, #fff 0, #eee 100%);
    background: -moz-linear-gradient(top, #fff 0, #eee 100%);
}

/* 好的实例 */
.element
{
    -webkit-border-radius: 3px;
       -moz-border-radius: 3px;
            border-radius: 3px;

    background: -webkit-linear-gradient(top, #fff 0, #eee 100%);
    background:    -moz-linear-gradient(top, #fff 0, #eee 100%);
    background:         linear-gradient(to bottom, #fff 0, #eee 100%);
}

/* 糟糕的实例 */
.element
{
    color: rgb(0, 0, 0);
    width: 50px;
    color: rgba(0, 0, 0, .5);
}

/* 好的实例 */
.element
{
    color: rgb(0, 0, 0);
    color: rgba(0, 0, 0, .5);
}
```

## JavaScript

### 缩进

缩进的单位为4个空格，规则也很简单——花括号里面的东西。

``` js
function outer(a, b)
{
    let c = 1,
        d = 2,
        inner;

    if(a > b)
    {
        inner = function()
        {
            return {
                r: c - d
            };
        };
    }
    else
    {
        inner = function()
        {
            return {
                r: c + d
            };
        };
    }

    return inner;
}
```

### 分号

以下几种情况后需加分号：

- 变量声明
- 表达式
- return
- throw
- break
- continue
- do-while

### 空格

以下几种情况需要空格：

- 操作符 `+`，`-`，`*`，`/`，`=`，`<`，`>`，`<=`，`>=`，`===`，`!==`，`&&`，`||`，`+=` 前后
- 三元运算符 `?` 和 `:` 前后
- 单行注释 `//` 后（若单行注释和代码同行，则 `//` 前也需要），多行注释 `*` 后
- 对象的属性值前，例：`{a: 1, b: 2};`
- 分隔数组项的逗号后面，例：`[1, 2, 3];`
- for 循环分号分开后的的部分，例： `for(let i = 0; i < 10; i++) {...}`
- for 循环中初始化的多变量(i 和 max)：`for(let i = 0, max = 10; i < max; i++) {...}`
- 函数的参数之间

以下几种情况不需要空格：

- 对象的属性名后
- 前缀一元运算符后
- 后缀一元运算符前
- 函数调用括号前
- 无论是函数声明还是函数表达式，`(` 前不要空格
- 数组的 `[` 后和 `]` 前
- 对象的 `{` 后和 `}` 前
- 运算符 `(` 后和 `)` 前

``` js
// 糟糕的实例
let a =
{
    b :1
};

// 好的实例
let a =
{
    b: 1
};

// 糟糕的实例
++ x;
y ++;
z = x?1:2;

// 好的实例
++x;
y++;
z = x ? 1 : 2;

// 糟糕的实例
let a = [ 1, 2 ];

// 好的实例
let a = [1, 2];

// 糟糕的实例
let a = ( 1+2 )*3;

// 好的实例
let a = (1 + 2) * 3;

// 声明函数时 `(` 前面没有空格
let doSomething = function(a, b, c)
{
    // do something
};

// 调用函数时 `(` 前面没有空格
doSomething(item);

// 糟糕的实例
for(i=0;i<6;i++)
{
    x++;
}

// 好的实例
for(i = 0; i < 6; i++)
{
    x++;
}
```

### 空行

以下几种情况需要空行：

- 变量声明后（当变量声明在代码块的最后一行时，则无需空行）
- 注释前（当注释在代码块的第一行时，则无需空行）
- 代码块后（在函数调用、数组、对象中则无需空行）
- 逻辑块之间加空行增加可读性
- 文件最后保留一个空行

``` js
// 变量声明后需要空行
let x = 1;

// 当变量声明在代码块的最后一行时，则无需空行
if(x >= 1)
{
    let y = x + 1;
}

let a = 2;

// 在行注释前添加一个空行
a++;

function b()
{
    // 当注释在代码块的第一行时，则无需空行
    return a;
}

// 代码块后面需要添加空行
for(let i = 0; i < 2; i++)
{
    if(true)
    {
        return false;
    }

    continue;
}

let obj =
{
    foo: function()
    {
        return 1;
    },

    bar: function()
    {
        return 2;
    }
};

func
(
    2,
    function()
    {
        a++;
    },
    3
);

let foo =
[
    2,
    function()
    {
        a++;
    },
    3
];

let foo =
{
    a: 2,
    b: function()
    {
        a++;
    },
    c: 3
};
```

### 换行

换行的地方，行末必须有 `,` 或者运算符；

以下几种情况需要换行：

- 代码块 `{` 和 `}` 前后
- 下列关键字后：`else`、`catch`、`finally`
- 变量赋值后

``` js
// 糟糕的实例
let a =
{
    b: 1
    , c: 2
};

x = y
    ? 1 : 2;

// 好的实例
let a =
{
    b: 1,
    c: 2
};

x = y ? 1 : 2;
x = y ?
    1 : 2;

if(condition)
{
    ...
}
else
{
    ...
}

try
{
    ...
}
catch(e)
{
    ...
}
finally
{
    ...
}

function test()
{
    ...
}

// 糟糕的实例
let a, foo = 7, b,
    c, bar = 8;

// 好的实例
let foo = 7,
    bar = 8;
    a,
    b,
    c;
```

### 单行注释

双斜线后，必须跟一个空格；  
缩进与下一行代码保持一致；  
可位于一个代码行的末尾，与代码间隔一个空格。

``` js
if(condition)
{
    // 条件成立，执行 allowed 函数。
    allowed();
}

let name = "jason";    // 双斜线距离分号一个缩进，双斜线后始终保留一个空格。
```

### 多行注释

什么时候使用多行注释？

- 难于理解的代码段
- 可能存在错误的代码段
- 浏览器特殊的 HACK 代码
- 业务逻辑相关的代码

多行注释的标准？

- 在注释前面保留一个空行
- 最少三行，格式如下：

``` js
/*
 * 注释内容与星号前保留一个空格
 */
let x = 1;
```

### 文档注释

请按照如下场景添加文档注释，具体用到的标签（例如：`@param`）请参考 [JSDoc](http://www.css88.com/doc/jsdoc/index.html)。

- 文件头部
- 所有常量
- 所有函数
- 所有类
- 所有类成员（字段、属性、方法）

``` js
/**
 * 天干地支之地支速查表<=>生肖
 * @const
 * @description ["鼠","牛","虎","兔","龙","蛇","马","羊","猴","鸡","狗","猪"]
 * @returns Array<string>
 */
const ANIMALS = ["\u9f20", "\u725b", "\u864e", "\u5154", "\u9f99", "\u86c7", "\u9a6c", "\u7f8a", "\u7334", "\u9e21", "\u72d7", "\u732a"];

/**
 * 根据农历数字日期获取对应的汉字表示法。
 * @param  {number} day 农历日期
 * @example let day = LunarUtils.getChinaDay(25);   day = "廿五"
 * @returns string
 */
function getChinaDay(day)
{
    ...
}
```

### 引号

最外层统一使用双引号 "" 或模板字符串 ``。

``` js
let name = "jason",
    time = "today";
    
// 普通字符串
let str1 = "In JavaScript '\n' is a line-feed.";

// 模板字符串
let str2 = `Hello ${name}, how are you ${time}?`;
```

### 变量命名

- 变量名和方法名使用 Camel（首字母小写）命名方式，如：`let name = p1.getName();`
- 常量名采用全大写加下划线连接形式，如：`const PI = 3.141592653;`
- 类名（构造函数名）使用 Pascal（首字母大写）命名方式，如：`function Animal() {...}`
- 使用一个下划线前缀来表示一个私有字段，如：`this._name = "jason";`
- DOM 对象以 `$` 开头命名，如：`let $passwordInput = $("#txtPassword");`

``` js
let thisIsMyName;
let goodID;
let reportURL;
let androidVersion;
let iOSVersion;

const MAX_COUNT = 10;

function Person(name)
{
    this._name = name;
}

Person.prototype.showName = function()
{
    alert(this._name);
}

let $passwordInput = document.getElementById("txtPassword");
```

### 变量声明

如果没有用到 es6 的语法，那么在一个函数作用域中所有的变量声明尽量提到函数首部，用一个 `var` 声明。

``` js
function doSomethingWithItems(items)
{
    var value = 10,
        result = value + 10,
        i,
        len;

    for(i = 0, len = items.length; i < len; i++)
    {
        result += 10;
    }
}
```

### 函数

函数调用括号前不需要空格；  
立即执行函数外必须包一层括号；  
不要给inline function命名；  
参数之间用 `,` 分隔，注意逗号后有一个空格。 

``` js
// 括号 '(' 前面不需要添加空格
let doSomething = function(item)
{
    // do something
};

function doSomething(item)
{
    // do something
}

// 糟糕的实例
doSomething (item);

// 好的实例
doSomething(item);

// 立即执行函数外必须包一层括号
(function()
{
    return 1;
})();

// 糟糕的实例
[1, 2].forEach(function x()
{
    ...
});

// 好的实例
[1, 2].forEach(function()
{
    ...
});

// 糟糕的实例
let a = [1, 2, function a()
{
    ...
}];

// 好的实例
let a = [1, 2, function()
{
    ...
}];

// 参数之间用 ',' 分隔，逗号后有一个空格
let doSomething = function(a, b, c)
{
    // do something
};
```

### 数组、对象

对象属性名不需要加引号；  
对象以缩进的形式书写，不要写在一行；  
数组、对象最后不要有逗号。  

``` js
// 糟糕的实例
let a =
{
    'b': 1
};

let a = {b: 1};

let a =
{
    b: 1,
    c: 2,
};

// 好的实例
let a =
{
    b: 1,
    c: 2
};
```

### 花括号

花括号 `{}` 应总被使用，即使在它们为可选的时候。虽然在 `if` 或者 `for` 中如果语句仅一条，花括号是不需要的，但是你还是应该总是使用它们，这会让代码更有持续性和易于更新。

想象下你有一个只有一条语句的 for 循环，你可以忽略花括号，而没有解析的错误。

``` js

// 糟糕的实例
for(let i = 0; i < 10; i++)
    alert(i);

```

但是，如果，后来，主体循环部分又增加了行代码：

``` js

// 糟糕的实例
for(let i = 0; i < 10; i++)
    alert(i);
    alert(i + " is " + (i % 2 ? "odd" : "even"));

```

第二个 alert 已经在循环之外，缩进可能欺骗了你。为了长远打算，最好总是使用花括号，即使只有一行代码：

``` js

// 好的实例
for(let i = 0; i < 10; i++)
{
    alert(i);
}

```

因此，涉及 `if`，`for`，`while`，`do...while`，`try...catch...finally` 的地方都必须使用花括号。

### null

适用场景：

- 初始化一个将来可能被赋值为对象的变量
- 与已经初始化的变量做比较
- 作为一个参数为对象的函数的调用传参
- 作为一个返回对象的函数的返回值

不适用场景：

- 不要用 null 来判断函数调用时有无传参
- 不要与未初始化的变量做比较

``` js
// 糟糕的实例
function test(a, b)
{
    if (b === null)
    {
        ...
    }
}

let a;

if(a === null)
{
    ...
}

// 好的实例
let a = null;

if(a === null)
{
    ...
}
```

### undefined

永远不要直接使用 undefined 进行变量判断；  
使用 typeof 和字符串 `"undefined"` 对变量进行判断。  

``` js
// 糟糕的实例
if(person === undefined)
{
    ...
}

// 好的实例
if(typeof person === "undefined")
{
    ...
}
```

### 其他

不要混用 tab 和空格；  
对上下文 this 的引用只能使用 `_this`、`that`、`self` 其中一个来命名；  
`switch` 的穿透和没有默认判断的情况一定要有注释特别说明；  
不允许有空的代码块；  
尽量减少全局变量的使用，不要让局部变量覆盖全局变量；  
`eval` 和 `with` 非特殊场景，应避免使用他们；  
不要给 `setTimeout` 或者 `setInterval` 传递字符串参数；  
使用 `{}` 代替 `new Object()`；  
使用 `[]` 代替 `new Array()`；  
应该总是使用分号，即使他们可由 JavaScript 解析器隐式创建；  
`use strict` 必须放在函数的第一行，可以用自执行函数包含大的代码段；  
使用 `===` 和 `!==` 操作符代替 `==` 和 `!=`；  
`for in` 循环里一定要有 `hasOwnProperty` 的判断；  
不要在内置对象的原型上添加方法，如：`Array`、`Date`、`Number`；  
不要在内层作用域的代码里声明了变量，之后却访问到了外层作用域的同名变量；  
变量不要先使用后声明；  
不要在一句代码中单单使用构造函数，记得将其赋值给某个变量；  
不要在同个作用域下声明同名变量；  
不要在一些不需要的地方加括号，例：delete(a.b)；  
不要使用未声明的变量；  
不要声明了变量却不使用；  
不要在应该做比较的地方做赋值；  
debugger不要出现在提交的代码里；  
数组中不要存在空元素；  
不要在循环内部声明函数；  
不要像这样使用构造函数，例：new function () { ... }, new Object。

``` js
// 糟糕的实例
let a   = 1;

function Person()
{
    // 糟糕的实例
    let me = this;

    // 好的实例
    let _this = this;

    // 好的实例
    let that = this;

    // 好的实例
    let self = this;
}

// 好的实例
switch (condition)
{
    case 1:
    case 2:
        ...
        break;
    case 3:
        ...
    // 因为xxx原因这里故意穿透
    case 4
        ...
        break;
    // 因为xxx原因这里没有做默认判断
}

// 糟糕的实例，空的代码快
if(condition)
{

}

// 糟糕的实例
if(a == 1)
{
    a++;
}

// 好的实例
if(a === 1)
{
    a++;
}

// 好的实例
for(key in obj)
{
    if(obj.hasOwnProperty(key))
    {
        // 确保 obj[key] 是自有属性而不是原型链上的
        console.log(obj[key]);
    }
}

// 糟糕的实例
Array.prototype.count = function(value)
{
    return 4;
};

// 糟糕的实例
var x = 1;

function test()
{
    if(true)
    {
        var x = 0;
    }

    x += 1;
}

// 糟糕的实例
function test()
{
    console.log(x);

    var x = 1;
}

// 糟糕的实例
new Person();

// 好的实例
let person = new Person();

// 糟糕的实例
delete(obj.attr);

// 好的实例
delete obj.attr;

// 糟糕的实例
if(a = 10)
{
    a++;
}

// 糟糕的实例
let a = [1, , , 2, 3];

// 糟糕的实例
let nums = [];

for(let i = 0; i < 10; i++)
{
    (function(i)
    {
        nums[i] = function(j)
        {
            return i + j;
        };
    }(i));
}

// 糟糕的实例
let singleton = new function()
{
    let privateVar;

    this.publicMethod = function()
    {
        privateVar = 1;
    };

    this.publicMethod2 = function()
    {
        privateVar = 2;
    };
};
```