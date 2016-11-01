#关于flex布局的探究与解释#

###flex布局是什么？###

Flex是Flexible Box的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性，并且任何一个容器都可以指定为Flex布局，行内元素也可以使用Flex布局。

###一、基本概念###

采用Flex布局的元素，称为Flex容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为Flex项目（flexitem），简称"项目"。

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

###二、容器的属性###

容器总共有六种属性

* **flex-direction**
* **flex-wrap**
* **flex-flow**
* **justify-content**
* **align-items**
* **align-content**

####2.1**flex-direction**####
flex-direction属性决定主轴的方向（即项目的排列方向）。

* row（默认值）：主轴为水平方向，起点在左端。
* row-reverse：主轴为水平方向，起点在右端。
* column：主轴为垂直方向，起点在上沿。
* column-reverse：主轴为垂直方向，起点在下沿。
####2.2**flex-wrap**####
默认情况下，项目都排在一条线（又称"轴线"）上。

* nowrap（默认）：不换行。
* wrap：换行，第一行在上方。
* wrap-reverse：换行，第一行在下方。
####2.3**flex-flow**####
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
####2.4**justify-content**####
justify-content属性定义了项目在主轴上的对齐方式。

* flex-start（默认值）：左对齐
* flex-end：右对齐
* center： 居中
* space-between：两端对齐，项目之间的间隔都相等。
* space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
####2.5**align-items**####
align-items属性定义项目在交叉轴上如何对齐。

* flex-start：交叉轴的起点对齐。
* flex-end：交叉轴的终点对齐。
* center：交叉轴的中点对齐。
* baseline: 项目的第一行文字的基线对齐。
* stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
####2.6**align-content**####
align-content属性定义了多根轴线的对齐方式。(如果项目只有一根轴线，该属性不起作用。)

* lex-start：与交叉轴的起点对齐。
* flex-end：与交叉轴的终点对齐。
* center：与交叉轴的中点对齐。
* space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
* space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
* stretch（默认值）：轴线占满整个交叉轴。
###三、子元素（项目）###
####3.1order####
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
####3.2flex-grow####
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
> 如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
####3.3flex-shrink####
flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
> 如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。
负值对该属性无效。
####3.4flex-basis####
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
> 它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。
####3.5flex####
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
####3.6align-self####
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
#关于响应式布局的理解#
##一、通过百分比进行布局##
我们通常把使用百分比的布局称为流动布局

通过响应式中有名的media queries可以在某个分辨率节点改变布局，那么使用百分比可以让处于这些节点之间的设备屏幕或是浏览器窗口也能正常显示全部内容。

有一个通过运算得出一个百分比的宽度，一个基本的公式就是“固定布局的宽度/基准参考值=流动布局百分比”。
> 关键点在于这个“基准参考值”，假设基准参考值1000px，而1000px是他们的父级块的宽度，所以，想要求出当前元素的百分比，他的基准参考值应该是父级块的宽度。

百分比的每块区域都会随着窗口的大小自动发生变化，有时我们也需要让某个块的尺寸是不变的，而其旁边的元素自动适应剩余宽度。
##二、通过媒体查询进行布局##
@media是CSS3中新引进的一个特性，被称为媒体查询。在页面中也可以通过这个属性来引入媒体类型。它的语法格式是：@media screen {
   选择器{样式代码。。。}
}

* screen 适用于计算机彩色屏幕。
* print 适用于打印预览模式下查看的内容或者打印机打印的内容。

媒体查询主要依据是：自动判断屏幕尺寸的width，符合尺寸要求的屏幕才会被允许执行当前的样式。

**优点：**

* 面对不同分辨率设备灵活性强
* 能够快捷解决多设备显示适应问题 

**缺点：**

* 兼容各种设备工作量大，效率低下 
* 代码累赘，会出现隐藏无用的元素，加载时间加长 
* 是一种折衷性质的设计解决方案，多方面因素影响而达不到最佳效果 一定程度上改变了网站原有的布局结构，会出现用户混淆的情况
##三、通过rem进行布局##

em是指相对于根元素的字体大小的单位。简单的说它就是一个相对单位。看到rem大家一定会想起em单位，em是指相对于父元素的字体大小的单位。它们之间其实很相似，只不过一个计算的规则是依赖根元素一个是依赖父元素计算。

**rem原理：**
rem是根据html的font-size大小来变化，正是基于这个出发，我们可以在每一个设备下根据设备的宽度设置对应的html字号，从而实现了自适应布局。

**如何获得rem的值**

* 1、是根据js来调整html的字号
* 2、是通过媒体查询来调整字号

    <script>        
        (function (doc, win) {
        var docEl = doc.documentElement,
          isIOS = navigator.userAgent.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/),//判断是不是移动设备
          dpr = isIOS? Math.min(win.devicePixelRatio, 3) : 1,//win.devicePixelRatio设备独立像素
          dpr = window.top === window.self? dpr : 1, //被iframe引用时，禁止缩放
          dpr = 1,
          scale = 1 / dpr,
          resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize';
        docEl.dataset.dpr = dpr;
        var metaEl = doc.createElement('meta');
        metaEl.name = 'viewport';
        metaEl.content = 'initial-scale=' + scale + ',maximum-scale=' + scale + ', minimum-scale=' + scale;
        docEl.firstElementChild.appendChild(metaEl);
        var recalc = function () {
            var width = docEl.clientWidth;
            if (width / dpr > 750) {
                width = 750 * dpr;
            }
            docEl.style.fontSize = 100 * (width / 750) + 'px';
          };
        recalc()
        if (!doc.addEventListener) return;
        win.addEventListener(resizeEvt, recalc, false);
      })(document, window);
		</script>
