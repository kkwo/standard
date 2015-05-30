#CSS编码规范
===
##目的

本文档定义了CSS的编码规范，旨在推进代码的可维护性和可读性，方便后期的管理和维护。

##编码

所有CSS文件均采用 **`UTF-8`** 编码

##引入方式
* 外联

		<link rel="stylesheet" href="css/commom.css">

* 内联

		<style>...</style>
		
* **注意**
   * 原则上，不允许在html 上直接写样式
   * 内外联方式的类型声明type="text/css" 都可以省略
   * link 和style 标签都应该放入head 中
   * `禁止`在css文件内部采用 @import 方式引入其它css文件
   * 如遇修改线上css 文件内引用的背景图，需要在相应url 后添加版本号，如：
   
   			background: url(images/sprite.png?v=20150307);
   
##命名、规则书写规范
* 规则命名采用小写加中划线 `-` 的方式，不允许使用大写字母或下划线


* `禁止`直接为全局类名设置属性
* `禁止`类名中出现 **`ad`** 字样，防止被广告插件屏蔽
* 尽量避免使用!important
* 具体命名规则规定如下：
	  * 如果可以，颜色尽量用三位字符表示，例如#AABBCC 写成#ABC；
	  * 0 后面不需要单位，比如0px 可以省略成0，0.8px 可以省略成.8px；
	  * 如果没有边框时，不要写成border: 0，应该写成border: 0 none；
	  * background、font 等可以缩写的属性，尽量使用缩写形式，但一定要遵循W3C 的顺序

* 性能
  * 选择器应该在满足功能的基础上尽量简短，减少嵌套选择器的查询消耗。

		div > * { ... }


		
		.important-text { color: red; }
		
  * 在保持代码解耦的前提下，尽量合并重复的样式，例如：
  
  		h1 { color: red; }



##规则书写顺序
* 显示、位置属性

		display, position, left, top, float, clear, list-style
		
* 自身属性（盒模型）

		width, height, margin, padding, border

* 背景、行高
	
		background,line-height

* 文本属性

		color, font, text-decoration, text-align, text-indent, vertical-align, white-space,word-wrap,word-break

* 其它

		cursor, z-index, zoom，opacity

* css3

		transform, transition, animation, box-shadow, border-radius

* hack

##CSS取值规范
* font-family
  * font-family 不允许在业务代码中随意设置，需严格遵守视觉给出的规范；
  * css 中的字体不能出现中文，中文字体优先使用别名表示。遇别名中存在空格的情况，必须用引


	名  称   |  unicode编码         |    别名
  :-------- | :------------------: | :---------:

  * font-size 必须以px 或pt 为单位，推荐用px（注：pt 为打印版字体大小设置）；
* text-indent
  * 使用text-indent 时要避免使用一个很大的值来达到隐藏文字的效果，例如： text-indent:


##注释
* 文件顶部注释(多行)

		/**


		/* module: 模块中文名称by yourname */
		
	
		用于标注代办、修改等信息



##排版规范
* 缩进统一使用四个空格缩进
* 规则可以写成单行，或者多行，但是整个文件内的规则排版必须统一
* 单行书写风格
	1. 多个selector 共用一个样式集时，多个selector 之间作为分隔标识的逗号后需要一个空格
	2. 每一条规则的大括号`{ `前后都添加空格
	3. 属性名与值的冒号前不加空格，冒号之后加空格
	4. 每一个属性值后必须添加分号，并且分号后空格
	
			selector, selector2, selector3 { display: block; width: 100px; border: 1px solid #F00; }
			
* 多行的书写风格
	1. 多个selector 共用一个样式集时，多个selector 单独成行：

* 其他
	1. 在可以不使用引号的情况下尽量不使用引号，如背景图片路径；

##hack
hack 是一把双刃剑，原则上是：最大程度减少hack的使用

	color:red\9;     /* ie6+ */
	color:yellow\0;  /* ie8+ */
	color:yellow\9\0;  /* ie9+ */
	color:#333 !important;   /* 非ie6 */
	*color:green;  /* ie7,ie6 */
	+color:pink;  /* ie7 */
	_color:orange;  /* ie6 */
	
<h2 id="cssName">常用CSS命名</h2>

中文名	  |	 建议类名	    |	中文名	  |		建议类名
:------- | :---------- | :---------- | :--------
头部		| 	header 		|	外围容器		|	wrapper
尾部		|	footer 		|	容器			|	container

##常见bug
* [IE6]float时双倍边距，解决方法：
  * 将display属性设置为inline[建议]
  * 使用hack方式，对IE6特殊对待
* [IE6]列表 li 的楼梯 Bug，当在 li 中设置一些浮动但是 li 本身不浮动时，在 ie6 中就会出现楼梯效果。解决方法:
  * 为 li 设置浮动属性.
  * 为 li 设置 inline 属性
* [IE6]小于10px,解决方法：
  * 增加_overflow:hidden;
* [IE6]绝对定位元素消失的问题，解决方法：
  * 不要跟在浮动元素后面
  * 也可以在中间加个清除浮动
* [IE6]overflow:hidden 失效的bug，解决方法：
  * 父元素中设置position:relative
* [IE6]浮动出现3pxbug，解决方法：
  * margin-right:-3px 
* [IE6]重复字符，解决方法：
  * \<!-- --\>注释的影响，试着去掉注释
  * 减小第二个容器的宽度，使得父元素减去子元素大于3px 
  * 加一个或多个clear元素
* [IE6/7] z-index 失效的问题，解决方法：
  * 父元素或者祖元素这是z-index
* [IE6/7] 空\<a\>标签在 ie6，ie7下无法点击的bug，解决方法：
  * 给\<a\>标签设置一个background，然后设置透明度为0
* [chrome] chrome字体不能小于12px,解决方法：
  * -webkit-text-size-adjust:none;
  
##兼容性写法小技巧
* min-height

		min-height:50px;height:auto !important;height:50px;
	
* max-height

		max-height:45px;_height:expression(this.scrollHeight > 45 ? "45px" : "auto");
		
* 背景色透明(子元素不透明)
 		
 		/* AA指透明度，为十六进制正整数，取值范围为 00 – FF，00是完全透明，FF是完全不透明*/
 		filter:progid:DXImageTransform.Microsoft.gradient(enabled='true',
 		startColorstr='#AARRGGBB', endColorstr='#AARRGGBB');
 			