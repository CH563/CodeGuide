
# 钱端公司前端开发规范 v1.0

> 前言：在业务驱动下，我们前端组也越来越壮大。之前由于单独开发，没注意代码的规范，造成后期维护越来越增加工作量和难度。项目也越来越繁重和沉余，重构也增加许多工作量。为了更好的协同开发和项目管理，编写以下规范。在以后工作中大家共同维护与更新

|日期|版本|说明|作者|
|-----|:---:|:---:|---------|
|2017年7月14日|1.0|初稿|陈立文|

-------

<!-- TOC -->

- [钱端公司前端开发规范 v1.0](#钱端公司前端开发规范-v10)
  - [命名规则](#命名规则)
    - [SVN目录](#svn目录)
    - [项目命名](#项目命名)
    - [目录命名](#目录命名)
    - [HTML, JS, CSS, SCSS，图片文件命名](#html-js-css-scss图片文件命名)
  - [HTML语法](#html语法)
    - [JS生成标签](#js生成标签)
    - [减少标签数量](#减少标签数量)
    - [压缩图片](#压缩图片)
  - [css, scss语法](#css-scss语法)
    - [使用单引号](#使用单引号)
    - [样式属性顺序](#样式属性顺序)
    - [代码注释](#代码注释)
    - [媒体查询](#媒体查询)
  - [JavaScript语法](#javascript语法)
  - [开发环境](#开发环境)
    - [Gulp](#gulp)
    - [Webpack](#webpack)
  - [前后端分离项目](#前后端分离项目)
    - [使用vue-cli搭Vue项目](#使用vue-cli搭vue项目)
    - [Vue开发规范](#vue开发规范)

<!-- /TOC -->

## 命名规则

### SVN目录

前端SVN目录地址：http://192.168.20.116/svn/前端

文件夹命名以项目中文命名，首拼音字母+项目中文命

例：s商户平台

---

### 项目命名

全部采用小写方式， 以下划线分隔。**禁止使用拼音命名**

例：my_project_name

---

### 目录命名

参照项目命名规则；

有复数结构时，要采用复数命名法。

例：js, styles, images, data_models

---

### HTML, JS, CSS, SCSS，图片文件命名

参照项目命名规则。

例：account_model.js, retina_sprites.scss

---

## HTML语法

- 缩进使用soft tab（2个空格）；
- 嵌套的节点应该缩进；
- 在属性上，使用双引号，不要使用单引号；
- 属性名全小写，用中划线做分隔符；
- 不要在自动闭合标签结尾处使用斜线（HTML5 规范 指出他们是可选的）；
- 不要忽略可选的关闭标签，例：`</li>` 和 `</body>`;
---
- 页面开头使用doctype来启用标准模式，并且大写
- 应在html标签上加上lang属性。这会给语音工具和翻译工具帮助，告诉它们应当怎么去发音和翻译。
【[语言列表](http://dwz.cn/6iimvG)】
- 声明一个明确的字符编码，让浏览器轻松、快速的确定适合网页内容的渲染方式，通常指定为'UTF-8'
- 根据HTML5规范, 通常在引入CSS和JS时不需要指明 type，因为 text/css 和 text/javascript 分别是他们的默认值。

```html
<!DOCTYPE html>
<html lang="zh-cn">
    <head>
        <meta charset="UTF-8">
        <title>Page title</title>
    </head>
    <body>
        <img src="images/company_logo.png" alt="Company">

        <h1 class="hello-world">Hello, world!</h1>
    </body>
</html>
```
---

### JS生成标签

在JS文件中生成标签让内容变得更难查找，更难编辑，性能更差。应该尽量避免这种情况的出现。

---

### 减少标签数量

在编写HTML代码时，需要尽量避免多余的父节点；

很多时候，需要通过迭代和重构来使HTML变得更少

---

### 压缩图片

- 图标尽量使用iconfont
- 小图可以转换base64
- 大图片做点小小压缩，如：[TinyPNG](https://tinypng.com/)

---

## css, scss语法

> 禁止使拼音命名，使用有意义的英文命名

- 使用soft tab（2个空格）
- 每个属性声明末尾都要加分号
- 多行格式排版，编译后压缩代码
- 统一使用双引号
---
- class类名使用小写字母，以中划线分隔(也可以参考使用BEM命名方法使用)
- id采用驼峰式命名
- scss中的变量、函数、混合、placeholder采用驼峰式命名
- **scss嵌套最多不能超过3层**
- @import 引入的文件不需要开头的'_'和结尾的'.scss'
- 使用插件对一些新属性加个前缀，如：Autoprefixer
- 避免使用 !important

```scss
/* not good */
@import "_dialog.scss";

/* good */
@import "dialog";

/* class */
.element-content {
  color: red;
  background-color: black;
}

/* id */
#myDialog {
  ...
}

/* 变量 */
$colorBlack: #000;

/* 函数 */
@function pxToRem($px) {
  ...
}

/* 混合 */
@mixin centerBlock {
    ...
}

/* placeholder */
%myDialog {
    ...
}
```
---

- 当属性值或颜色参数为 0 - 1 之间的数时，省略小数点前的 0
- 当长度值为 0 时省略单位
- 十六进制的颜色属性值使用小写和尽量简写

```css
color: rgba(255, 255, 255, .5);

margin: 0 auto;

color: #fc0;
```

---

- 组件/公用类使用 %placeholders 定义，使用 @extend 引用

```scss
%clearfix {
  overflow: auto;
  zoom: 1;
}

.g-header {
  @extend %clearfix;
}
```

---

### 使用单引号

在某些样式中，会出现一些含有空格的关键字或者中文关键字。

**font-family 内使用引号**

当字体名字中间有空格，中文名字体及 Unicode 字符编码表示的中文字体，为了保证兼容性，都建议在字体两端添加单引号或者双引号：

**background-image 的 url 内使用引号**

如果路径里面有空格，旧版 IE 是无法识别的，会导致路径失效，建议不管是否存在空格，都添加上单引号或者双引号：

```css
body {
  font-family: 'Microsoft YaHei', '黑体-简', '\5b8b\4f53';
}

div {
  background-image: url('...');
}
```

---

### 样式属性顺序

单个样式规则下的属性在书写时，应按功能进行分组，并以 Positioning Model > Box Model > Typographic > Visual 的顺序书写，提高代码的可读性。

- 如果包含 content 属性，应放在最前面；
- Positioning Model 布局方式、位置，相关属性包括：position / top / right / bottom / left / z-index / display / float / ...
- Box Model 盒模型，相关属性包括：width / height / padding / margin / border / overflow / ...
- Typographic 文本排版，相关属性包括：font / line-height / text-align / word-wrap / ...
- Visual 视觉外观，相关属性包括：color / background / list-style / transform / animation / transition / ...

Positioning 处在第一位，因为他可以使一个元素脱离正常文本流，并且覆盖盒模型相关的样式。盒模型紧跟其后，因为他决定了一个组件的大小和位置。其他属性只在组件内部起作用或者不会对前面两种情况的结果产生影响，所以他们排在后面。

---

### 代码注释

**文件注释**

文件顶部必须包含文件注释，用 @name 标识文件说明。星号要一列对齐，星号与内容之间必须保留一个空格，标识符冒号与内容之间必须保留一个空格。

```css
/**
 * @name: 文件名或模块名
 * @description: 文件或模块描述
 * @author: author-name(mail-name@qianduan.com)
 *          author-name2(mail-name2@qianduan.com)
 * @update: 2015-04-29 00:02
 */
```

- @description为文件或模块描述。
- @update为可选项，建议每次改动都更新一下。

当该业务项目主要由固定的一个或多个人负责时，需要添加@author标识，一方面是尊重劳动成果，另一方面方便在需要时快速定位责任人。

**单行注释**

星号与内容之间必须保留一个空格。

```css
/* 表格隔行变色 */
```

**多行注释**

星号要一列对齐，星号与内容之间必须保留一个空格。

```css
/**
 * Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
 */
```

**规则声明块内注释**

使用 // 注释，// 后面加上一个空格，注释独立一行。

```css
.foo{
  border: 0;
  // ....
}
```


---

### 媒体查询

尽量将媒体查询的规则靠近与他们相关的规则，不要将他们一起放到一个独立的样式文件中，或者丢在文档的最底部，这样做只会让大家以后更容易忘记他们。

```scss
.box{
  width:1200px;
  @media (max-width: 750px){
    width:100%;
  }
}
```

---

## JavaScript语法

[![JavaScript Style Guide](https://camo.githubusercontent.com/e06d9d72eecca61c1ba39fdf19868f70fcb3a9b3/68747470733a2f2f63646e2e7261776769742e636f6d2f6665726f73732f7374616e646172642f6d61737465722f62616467652e737667)](https://github.com/feross/standard)

[详细规范请查看](https://github.com/standard/standard/blob/master/docs/RULES-zhcn.md)

> 以 JavaScript Standard Style 为标准执行，使用Eslint

全局安装
```cmd
$ npm install standard --global
```

**Sublime Text**

> 通过 Package Control，安装 SublimeLinter 和 SublimeLinter-contrib-standard。
如果想要保存时自动格式化，还需安装 StandardFormat。

**Visual Studio Code**

> 安装 vscode-standardjs（已经包含了自动格式化）。
安装 vscode-standardjs-snippets 以获得 JS snippets。

**WebStorm (PhpStorm, IntelliJ, RubyMine, JetBrains 等 jetbrains 全家桶系列)**

> WebStorm 最近宣布在其 IDE 中 自带 standard 规范。

---

- 使用soft tab（2个空格）
- **除需要转义的情况外，字符串统一使用单引号**
- 不要定义未使用的变量
- 关键字后面加空格
- 函数声明时括号与函数名间加空格
- 始终使用 === 替代 ==
- 字符串拼接操作符 (Infix operators) 之间要留空格
- 逗号后面加空格
- else 关键字要与花括号保持在同一行

```javascript
var message = 'hello, ' + name + '!'

var list = [1, 2, 3, 4]
function greet (name, options) { ... }

if (condition) {
  // ...
} else {
  // ...
}
```

---

- 文档注释

```javascript
/**
 * @func
 * @desc 一个带参数的函数
 * @param {string} a - 参数a
 * @param {number} b=1 - 参数b默认值为1
 * @param {string} c=1 - 参数c有两种支持的取值</br>1—表示x</br>2—表示xx
 * @param {object} d - 参数d为一个对象
 * @param {string} d.e - 参数d的e属性
 * @param {string} d.f - 参数d的f属性
 * @param {object[]} g - 参数g为一个对象数组
 * @param {string} g.h - 参数g数组中一项的h属性
 * @param {string} g.i - 参数g数组中一项的i属性
 * @param {string} [j] - 参数j是一个可选参数
 */
function foo(a, b, c, d, g, j) {
  ...
}
```

---

- 使用浏览器全局变量时加上 window. 前缀

```javascript
window.alert('hi')   // ✓ ok
```

---

- 不允许有连续多行空行
- 对于三元运算符 ? 和 : 与他们所负责的代码处于同一行
- 每个 var 关键字单独声明一个变量
- 单行代码块两边加空格

```javascript
/ ✓ ok
var location = env.development ? 'localhost' : 'www.api.com'

// ✓ ok
var location = env.development
  ? 'localhost'
  : 'www.api.com'

// ✓ ok
var silent = true
var verbose = true

// ✗ avoid
var silent = true, verbose = true

// ✗ avoid
var silent = true,
    verbose = true

function foo () { return true }  // ✓ ok
```

---

- 对于变量和函数名统一使用驼峰命名法，**禁止使用拼音**

```javascript
function my_function () { }    // ✗ avoid
function myFunction () { }     // ✓ ok

var my_var = 'hello'           // ✗ avoid
var myVar = 'hello'            // ✓ ok
```

---

- 不允许有多余的行末逗号

```javascript
var obj = {
  message: 'hello',   // ✗ avoid
}
```

---

- 键值对当中冒号与值之间要留空白

```javascript
var obj = { 'key' : 'value' }    // ✗ avoid
var obj = { 'key' :'value' }     // ✗ avoid
var obj = { 'key':'value' }      // ✗ avoid
var obj = { 'key': 'value' }     // ✓ ok
```

---

- 构造函数要以大写字母开头

```javascript
function animal () {}
var dog = new animal()    // ✗ avoid

function Animal () {}
var dog = new Animal()    // ✓ ok
```

---

- 使用数组字面量而不是构造器

``` javascript
var nums = new Array(1, 2, 3)   // ✗ avoid
var nums = [1, 2, 3]            // ✓ ok
```

---

- 避免修改使用 const 声明的变量
- 同一模块有多个导入时一次性写完
- 不要使用 eval()
- 不要省去小数点前面的0
- 嵌套的代码块中禁止再定义函数
- 不要重复声明变量
- 正确使用 ES6 中的字符串模板
- 行末不留空格
- 不要使用 undefined 来初始化变量
- 如果有更好的实现，尽量不要使用三元表达式

```javascript
let score = val ? val : 0     // ✗ avoid
let score = val || 0          // ✓ ok
```

---

- 避免不必要的 .call() 和 .apply()
- 检查 NaN 的正确姿势是使用 isNaN()
- 不要使用分号
> 当前主流的代码压缩方案都是基于词法（AST-based）进行的，所以在处理无分号的代码时完全没有压力（何况 JavaScript 中分号本来就不是强制的）。

---

## 开发环境

>安装`nodejs`，再使用`npm`包管理工具安装依赖（建议使用淘宝镜像`cnpm`安装或`Yarn`安装）


**全局安装常用工具包**

>- [Eslint](https://www.npmjs.com/package/eslint)
>- [Gulp](https://www.npmjs.com/package/gulp)
>- [Node-sass](https://www.npmjs.com/package/node-sass)
>- [Vue-cli](https://www.npmjs.com/package/vue-cli)

### Gulp

在项目根目录下创建一个名为 `gulpfile.js` 的文件

在工作常用于构建活动页、APP嵌入页等等的静态页面

结合`pug` 、`scss`编写页面，从而提高开发效率

在制作移过端项目时，利淘宝开发`flexible.js`，再通过`postcss-px2rem` 插件，轻松使用rem布局来适应不用dpr和分辨率的手机

原理和实现方法请查看：[Github仓库](https://github.com/CollectionFiler/lib-flexible)、[详细方法](https://github.com/amfe/article/issues/17)

```javascript
var gulp = require('gulp');

gulp.task('default', function() {
  // 将你的默认的任务代码放在这
});
```

**常用插件**

- [browser-sync](https://www.npmjs.com/package/browser-sync)
- [gulp-clean](https://www.npmjs.com/package/gulp-clean)
- [gulp-clean-css](https://www.npmjs.com/package/gulp-clean-css)
- [gulp-imagemin](https://www.npmjs.com/package/gulp-imagemin)
- [gulp-jshint](https://www.npmjs.com/package/gulp-jshint)
- [gulp-plumber](https://www.npmjs.com/package/gulp-plumber)
- [gulp-postcss](https://www.npmjs.com/package/gulp-postcss)
- [autoprefixer](https://www.npmjs.com/package/autoprefixer)
- [postcss-px2rem](https://www.npmjs.com/package/postcss-px2rem)
- [gulp-pug](https://www.npmjs.com/package/gulp-pug)
- [gulp-sass](https://www.npmjs.com/package/gulp-sass)
- [gulp-uglify](https://www.npmjs.com/package/gulp-uglify)

---

### Webpack

> 不推荐全局安装，项目本地安装即可

[中文文档](https://doc.webpack-china.org/concepts/)

---

## 前后端分离项目

放在对应SVN目录下，以前面命名规则创建目录

在目录应存两个文件夹:

- doc - 存放开发说明文档、接口文档、产品设计原型等下相关需求文档
- project - 项目前端开代码存放

### 使用vue-cli搭Vue项目

全局安装后，在相应目录下使用命令安装

```cmd
$ vue init webpack my-project
```

使用webpack模版安装即可

ESLint 选用准备模式

Karma + Mocha 测试工具，不需要安装

e2e 用户行为模拟测试，不需要安装

---

### Vue开发规范

始终基于模块的方式来构建你的 app，每一个子模块只做一件事情。

Vue.js 的设计初衷就是帮助开发者更好的开发界面模块。一个模块是应用程序中独立的一个部分。

views 文件夹下面是由 以页面为单位的 vue 文件 或者 模块文件夹 组成的，放在 src 目录之下，与 components、assets 同级

功能型的css，最好和组件一起，不推荐拆离，比如一个通用的confirm确认框

减少AJAX请求，如果列表的删除，请求成功后，操作本地数据删除即可，不用再请求渲染列表

**views 文件夹：**

- views 下面的 vue 文件代表着页面的名字
- 只有一个文件的情况下不会出现文件夹，而是直接放在 views 目录下面，如 Login.vue Home.vue
- 一个导航功能下有多个页面时，应建立文件夹来存放，如：用户列表 应建立 user文件夹，再包含文件userList.vue userAdd.vue userEdit.vue等，页面公共样式也可以存放一起 user.scss


**method 自定义方法**

- 语法参看前面JS部分
- 动宾短语，如：jumpPage、openCarInfoDialog
- ajax 方法以 get、post 开头，以 data 结，如：getListData、postFormData
- 事件方法以 on 开头，如：onTypeChange、onUsernameInput
- init、refresh 单词除外
- 尽量使用常用单词开头（set、get、open、close、jump）
- 驼峰命名，如：getListData
- 切勿直接操作DOM，要操作数据
- 尽量使用Vue的语法糖，比如可以用:style代替v-bind:style；用@click代替v-on:click

**data props 方法**

- 使用 data 里的变量时请先在 data 里面初始化
- props 指定类型，也就是 type
- props 改变父组件数据 基础类型用 $emit ，复杂类型直接改
- 不命名多余数据，现在是用户列表页，你的数据是 ajax 请求的，那就直接声明一个对象叫 userList，而不是每个字段都声明
- 表单数据请包裹一层 form

**生命周期方法**

- 不在 mounted、created 之类的方法写逻辑，取 ajax 数据
- 在 created 里面监听 Bus 事件
