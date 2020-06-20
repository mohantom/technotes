CSS
---------


优先级：div/span < class < id < div/span里的style

div b {color: red}  //只将div中的b标签变成红色：关联选择器（空格）
.haha, #division, b { color:blue } 组合选择器（逗号）

伪元素选择器
:link, :visited, :hover, :active, 
a:link, a:visited {color:#00ff80; text-decoration: none;}  //访问前后样式一致
div:hover {color:#000000; background-color:#FFFFFF}
input:focus{background-color:#ffffff}
p:first-line, p:first-letter


CSS
--------------
Course: Your First Day with CSS
Text editor: brackets
CSS VALIDATION

W3C CSS Validator
http://jigsaw.w3.org/css-validator/

CSS ZEN GARDEN

CSS Zen Garden
http://csszengarden.com


main.css
img {
	width: 600px;
	border； 1px solid rgb(105, 105, 105);
}

LESS
-----------------
Dynamic style sheet language, compiles to CSS, introduces programming features to CSS (all CSS are valid LESS).
<link rel = “stylesheet/less” href = “css/my.less” type=”text/css”>
<script src = “less.js” …>

Or LESS on the server:
	Npm install less
ASP.NET: dotless 

// my.less
@import “init.less”;
@baseFontSize: 14px;
#main {
	H1 {
		Font-size: @baseFontSize;
	}
}

//

// operations
Font-size: 4px + 4;
Font-size: @base-size + 4px;

// color functions
Color: lighten(@color, 10%)
Darken, saturate, desaturate, fadein, fadeout, fade, spin, mix
@hue: hue(@color)
	Saturation, lightnes, alpha, hsl

In LESS, all color should be numeric values (not named like “red”)

// mixins
.rounded-corners-all(@size: 5px) {  // default is 5px
Border-radius: @size;
-webkit-border-radius: @size;
}

#form { .round-corners-all(5px);

// overloads, like Java
// using guards
.color(@color) when (alpha(@color) >= 50%) { Color: black; }
.color(@color) when (alpha(@color) < 50%) { Color: transparent; }

.width(@size) when (isnumber(@size)) { width: @size*2;}
.width(@size) when (ispercentage(@size)) { width: @size;}
#form { .width(50%); }

// nested rules
 

// use combinatory (&) to mix with parent
 

// namespaces
#my-forms {
	.set-button {
		Font-size: 14px;
		Text-align: center;
	}
}
#submit-button {
	#my-forms > .set-button;
}

// scope, variables/mixins are scoped
@size: 24px;
#form { 
@size: 18px; 
	.button {
		Font-size: @size; // 18px
	}
}

// string interpolation
@root: “/images/”;

// using javascript
@app-root: `”@{root}”.toUpperCase()`;
#form {
	Background: url(“@{app-root}/back.jpg”); // “IMAGES/back.jpg”


SASS
Syntactically awesome stylesheets, compiles to CSS
Two syntaxes: SASS (indention based) and SCSS (more like CSS)
	Npm install sass
	Var less = require(‘sass’)
ASP.NET: chirpy, design-time compilation, “foo.chirpy.sass”

My.sass -> my.css

// variables
$myColor: #ffeedd;

// operations
Font-size: 4px + 4;
Font-size: 20px * .8;
Color: #FFF / 4;
Width: (100% / 2) + 25%; // 75%

// color functions
Color: Lighten($color, 10%)
Darken, saturate, desaturate, fade_in, fade_out, invert, compliment
Quote($sometext), unquote($sometext)
If(true, $color1, $color2)
Round, ceil, floor, percentage

// string interpolation
$root: “/images/”;
url(“#{$root}background.jpg”);

$name: “my-class”;	// define a class
.#{$name} {
	Color: blue;
}


// Rules: nested
// parent selector (&)

// directives
@import: include or embed

@extend: inherits styles from another
.button { color: black; }
.submit-button { @extend .button; border: 1px black solid; }
// multiple inheritance

@mixin: repeatable sections, feel like functions
@mixin font-large {
	Font: { size: 14px; family: san-serif; }
}
#form { @include font-large; }
@mixin rounded-corners-all($size) { … }

@function
 

@if, @for, @each, @while
H1 {
	@if $size > 14px { color: blue; } 
	@else if …
	@else …
}



CSS
<font size="1"> only from 1 to 7. larger use CSS.
 
Faststone Capture
 
<input type="image"> 提交按钮为一个图片
 
<embed src="">
<bgsound src=#> #=wav file location
<bgsound loop=#> # repeat times
 
 
<img src="url.gif" dynsrc="url.avi">
Ulr.gif作为视频的封面
 
<img start=#> #=fileopen, mouseover
控制合适开始播放
 
<img src="f.gif" dynsrc="clock.avi" start="mouseover" loop=2>
 
网页本身的编码应当和content-type的一致
<meta http-equiv="Content-type" content="text/html;charset=utf-8">
 
<hr size="6px" noshade width="100px" align="left">
<b><i><u><s><strike>
 
客户端字体
<font face="华文彩云">
 
<p>
<center>
<multicol>
<blink>
 
客户端图片映射
原点在左上角
<img src="mapping.gif" usemap="#Face">
<map name="Face">
<area shape="rect" onclick="show()" href="fpage.html" coords="140, 20, 280, 60">
<area shape="circle" href="new.html" coords="80, 100, 60">
</map>
 
 
<input type="text">  // checkbox, radio, image, submit
<select>
<textarea>
 
<fieldset>
<legend> Info</legend>
<form>
<input type="text" />
</form>
</fieldset>
 
 
Css
-----------
basic
.Demo1 {
Font-size: 30px;
Font-color: red;
Text-decoration: underline;
}
 
Filter
图片颜色全部变成黑白
<style type="text/css">
a:link Img{
Filter:gray;
}
a:hover img{
Filter:"";
}
</style>
<a><img src="2.jpg"/></a>
 
Selector 4种选择器 (优先级)
Id > 类> html元素>通配符
#mydiv
Div{}
 
a:link{}, a:hover{}
p.cls1 { }, p.cls2{}
<p class="cls1" > class 1 </p>
 
通配符(for all elements)
*{ margin-top: 40px; margin: 10px 10px 20px 20px;}
 
Good practice:
*{margin:0px;padidng:0px}
 
父子选择器：必须是html元素，不要超过3层。
#id span { }
#id span span {}
.myClass span {}
Div #id .myClass {}
 
一个元素可以同时有一个id和多个类选择器
<span class="s1 s2" id="news"> News Now </span>
.s1{}
.s2{}
#id{}
当s1 s2有冲突时，以在css文件里出现在后面的为准。
 
将共同部分抽出 (注意要都好分开)
S1, s2, s3 {Background-color: pink; }
 
行内元素inline element: <span>, <a>, <input type=xxx>
<span>span1<span>
<span>span2<span>
显示为(不会换行): span1 span2
块元素block element: div, p
注意：有些css属性对行内元素不生效，比如margin, left, right, width, height。尽可能使用block element
可以互相转换：display: inline; display:block
 
Html 和css 都不区分大小写。js区分!
 
css之间可以相互引用
  @import url('comm.css')
 
标准流和非标准流
html元素在网页中显示的顺序，写在前面的在前显示。
 
盒子模型
Content, padding, border, margin
 
 
Body { border: 1px solid red;
Width: 600px;
Margin: 0 auto; // 0是上下边距为0，auto表示自动居中
}
 
Div {
Padding-left: 50px //如果超过会使盒子变大！在内部盒子里用margin控制
}
 
Img {
Margin-left: 50px; //image会到div外面去。
}
 
<!DOCTYPE HTML ….> 引入dtd文件width才会生效。
 
.faceurl li {
List-style-type: none; // 去掉list前面的小点
}
 
Background: pink url("") repeat-y;
 
float
一行的div都需要有float，否则会显示奇怪。
如果加了float，元素会变成display:block.
清除float:
Clear:right; clear:left; clear: both;
 
定位
Static
Left/top属性对static 没有效果！！
用margin-left和margin-top定位！！
 
Relative: 相对于原来的位置
#spe{ position: relative; left: 40px; top:40px;}  //向右向下移动40px
 
虽然脱离标准流，但是它的空间不能被占用。
 
Absolute 
#spe{ position: absolute; left: 40px; top:40px;} 
 
原来的位置会让出。
对该元素最近的那个脱离了标准流的元素定位。如果没有父元素（或者有父元素，但是没有脱离标准流），则相对body左上角定位。
 
<div class="div2">
<div class="spe">
内容2
</div></div>
 
.div2 { position:relative;} //只要不是static; 否则内容2还会在以前的位置。
 
 
 
Fixed: 相对body左上角
 
层叠 z-index: 6;
大的数值在上面
 
动态显示背景图
<li><a href="#"><span> Link1</span></a></li>
#navi a span {
Font-size:14px;font-weight:bold;color:#666666;display:block;padding-top:10px;padding-bottome:10px;
Background:url('nav_bg_right.gif'); }
#navi a:hover span {background-position: 100% -50px;}
// x轴不变，y轴下移50px
 
 
 
能不用table就不用table
