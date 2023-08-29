# *this* 指向

[bangbangji](E:\help file\xgglt\JS\核心概念\this指向.md)

## 经典真题



- *this* 的指向哪几种 ？

INSERT INTO `personal-social-homepage`.`essay` (`id`, `title`, `description`, `content`, `catalogue`, `cover`, `scanCount`, `commentCount`, `likeCount`, `createDate`, `categoryid`, `userid`) VALUES ('23', 'JavaScript中尺寸和位置总结', 'JavaScript中尺寸和位置，万字长文。', '<h1 id=\"尺寸和位置\">尺寸和位置</h1>\n<p>在 <em>JavaScript</em> 中操作 <em>DOM</em> 节点使其运动的时候，常常会涉及到各种宽高以及位置坐标等概念，如果不能很好地理解这些属性所代表的意义，就会在书写代码时遇到不小的问题。而由于这些属性概念较多，加上浏览器之间实现方式不同，常常会造成概念混淆。</p>\n<p>本章，我们就一起来总结一下使用 <em>JavaScript</em> 操作 <em>DOM</em> 时，尺寸和宽高相关的属性。</p>\n<p>主要分为以下两部分：</p>\n<ul>\n<li><em>DOM</em> 对象相关尺寸和位置属性\n<ul>\n<li>只读属性\n<ul>\n<li><em>clientWidth</em> 和 <em>clientHeight</em> 属性</li>\n<li><em>offsetWidth</em> 和 <em>offsetHeight</em> 属性</li>\n<li><em>clientTop</em> 和 <em>clientLeft</em> 属性</li>\n<li><em>offsetLeft</em> 和 <em>offsetTop</em> 属性</li>\n<li><em>scrollHeight</em> 和 <em>scrollWidth</em> 属性</li>\n</ul>\n</li>\n<li>可读可写属性\n<ul>\n<li><em>scrollTop</em> 和 <em>scrollLeft</em> 属性</li>\n<li><em>domObj.style.xxx</em> 属性</li>\n</ul>\n</li>\n</ul>\n</li>\n<li><em>event</em> 事件对象相关尺寸和位置属性\n<ul>\n<li><em>clientX</em> 和 <em>clientY</em> 属性</li>\n<li><em>screenX</em> 和 <em>screenY</em> 属性</li>\n<li><em>offsetX</em> 和 <em>offsetY</em> 属性</li>\n<li><em>pageX</em> 和 <em>pageY</em> 属性</li>\n</ul>\n</li>\n</ul>\n<blockquote>\n<p><em>DOM</em> 对象相关尺寸和位置属性</p>\n</blockquote>\n<table>\n<thead>\n<tr>\n<th>属性名</th>\n<th>含义</th>\n<th>是否只读</th>\n</tr>\n</thead>\n<tbody>\n<tr>\n<td><em>clientWidth</em> 和 <em>clientHeight</em> 属性</td>\n<td>元素的可视部分宽度和高度 即<code>padding + content</code></td>\n<td>只读</td>\n</tr>\n<tr>\n<td><em>offsetWidth</em> 和 <em>offsetHeight</em> 属性</td>\n<td>元素的 <em>border+padding+content</em> 的宽度和高度</td>\n<td>只读</td>\n</tr>\n<tr>\n<td><em>clientTop</em> 和 <em>clientLeft</em> 属性</td>\n<td>元素的 <em>border</em> 的宽度和高度</td>\n<td>只读</td>\n</tr>\n<tr>\n<td><em>offsetLeft</em> 和 <em>offsetTop</em> 属性</td>\n<td>相对于其 <em>offsetParent</em>(离自己最近的并且定了位的祖先元素) 的left和top</td>\n<td>只读</td>\n</tr>\n<tr>\n<td><em>scrollHeight</em> 和 <em>scrollWidth</em> 属性</td>\n<td>元素内部的内容超出其宽度和高度的时候，元素内部内容的实际宽度和高度</td>\n<td>只读</td>\n</tr>\n<tr>\n<td><em>scrollTop</em> 和 <em>scrollLeft</em> 属性</td>\n<td>元素其中的内容超出其宽高的时候，元素被卷起的高度和宽度</td>\n<td>可读可写</td>\n</tr>\n</tbody>\n</table>\n<blockquote>\n<p><em>event</em> 事件对象相关尺寸和位置属性</p>\n</blockquote>\n<table>\n<thead>\n<tr>\n<th>属性名</th>\n<th>含义</th>\n</tr>\n</thead>\n<tbody>\n<tr>\n<td><em>clientX</em> 和 <em>clientY</em> 属性</td>\n<td>事件发生时鼠标相对于浏览器窗口的坐标，即浏览器左上角坐标的（ <em>0 , 0</em> ）</td>\n</tr>\n<tr>\n<td><em>screenX</em> 和 <em>screenY</em> 属性</td>\n<td>事件发生时鼠标相对于电脑屏幕的坐标，以设备屏幕的左上角为原点</td>\n</tr>\n<tr>\n<td><em>offsetX</em> 和 <em>offsetY</em> 属性</td>\n<td>鼠标点击位置相对于该事件源的位置，即点击该 <em>DOM</em> 元素，以该 <em>DOM</em> 左上角为原点来计算鼠标点击位置的坐标</td>\n</tr>\n<tr>\n<td><em>pageX</em> 和 <em>pageY</em> 属性</td>\n<td>该属性是事件发生时鼠标点击位置相对于页面的位置，通常浏览器窗口没有出现滚动条时，该属性和 <em>clientX</em> 及 <em>clientY</em> 是等价的</td>\n</tr>\n</tbody>\n</table>\n<h2 id=\"dom-对象相关尺寸和位置属性\"><em>DOM</em> 对象相关尺寸和位置属性</h2>\n<p>在 <em>DOM</em> 对象所提供的尺寸和位置相关属性中，可以分为<strong>只读属性</strong>和<strong>可读可写属性</strong>。</p>\n<h3 id=\"只读属性\">只读属性</h3>\n<p>所谓的只读属性指的是 <em>DOM</em> 节点的固有属性，该属性只能通过 <em>JavaScript</em> 去获取而不能通过 <em>JavaScript</em> 去设置，而且获取的值是只有数字并不带单位的（ <em>px、em</em> 等 ）</p>\n<p>常见的只读属性有：</p>\n<ul>\n<li><em>clientWidth</em> 和 <em>clientHeight</em> 属性</li>\n<li><em>offsetWidth</em> 和 <em>offsetHeight</em> 属性</li>\n<li><em>clientTop</em> 和 <em>clientLeft</em> 属性</li>\n<li><em>offsetLeft</em> 和 <em>offsetTop</em> 属性</li>\n<li><em>scrollHeight</em> 和 <em>scrollWidth</em> 属性</li>\n</ul>\n<p>下面我们来一组一组进行介绍。</p>\n<h4 id=\"clientwidth-和-clientheight-属性\"><em>clientWidth</em> 和 <em>clientHeight</em> 属性</h4>\n<p>==该属性指的是元素的可视部分宽度和高度==，即 ==*padding + content*==，例如：</p>\n<pre><code class=\"language-html\">&lt;div id=&quot;container&quot; class=&quot;container&quot;&gt;&lt;/div&gt;\n</code></pre>\n<pre><code class=\"language-css\">.container{\n  width: 200px;\n  height: 200px;\n  background-color: red;\n  border: 1px solid;\n  overflow: auto;\n  padding: 10px;\n  margin: 20px;\n}\n</code></pre>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\nconsole.log(&quot;clientWidth:&quot;,container.clientWidth); // 220\nconsole.log(&quot;clientHeight:&quot;,container.clientHeight); // 220\n</code></pre>\n<h4 id=\"offsetwidth-和-offsetheight-属性\"><em>offsetWidth</em> 和 <em>offsetHeight</em> 属性</h4>\n<p>这一对属性指的是==元素的 <em>border+padding+content</em> 的宽度和高度==。例如：</p>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\nconsole.log(&quot;offsetWidth:&quot;, container.offsetWidth); // 222\nconsole.log(&quot;offsetWidth:&quot;, container.offsetWidth); // 222\n</code></pre>\n<p>可以看到该属性和 <em>clientWidth</em> 以及 <em>clientHeight</em> 相比，多了设定的边框 <em>border</em> 的宽度和高度。</p>\n<h4 id=\"clienttop-和-clientleft-属性\"><em>clientTop</em> 和 <em>clientLeft</em> 属性</h4>\n<p>这一对属性是用来读取==元素的 <em>border</em> 的宽度和高度==的。例如：</p>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\nconsole.log(&quot;clientTop:&quot;, container.clientTop); // 1\nconsole.log(&quot;clientLeft:&quot;, container.clientLeft); // 1\n</code></pre>\n<h4 id=\"offsetleft-和-offsettop-属性\"><em>offsetLeft</em> 和 <em>offsetTop</em> 属性</h4>\n<p>首先需要介绍一下 <em>offsetParent</em> 属性，该属性是获取当前元素的==离自己最近的并且定了位的祖先元素==，该祖先元素就是当前元素的 *offsetParent*。</p>\n<p>如果从该元素向上寻找，找不到这样一个祖先元素，那么当前元素的 <em>offsetParent</em> 就是 <em>body</em> 元素。</p>\n<p><em>offsetLeft</em> 和 <em>offsetTop</em> 指的是当前元素，相对于其 <em>offsetParent</em> 左边距离和上边距离，即当前元素的 <em>border</em> 到包含它的 <em>offsetParent</em> 的 <em>border</em> 的距离。</p>\n<p>下面我们来具体举例说明：</p>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\nconsole.log(container.offsetParent); // body\n</code></pre>\n<p>可以看到，我们直接访问 <em>container</em> 盒子的 <em>offsetParent</em> 属性，因为不存在定了位的祖先元素，所以显示出来的是 <em>body</em> 元素。</p>\n<p>接下来我们对上面的代码进行改造：</p>\n<pre><code class=\"language-html\">&lt;div id=&quot;container&quot; class=&quot;container&quot;&gt;\n  &lt;div id=&quot;item&quot; class=&quot;item&quot;&gt;&lt;/div&gt;\n&lt;/div&gt;\n</code></pre>\n<pre><code class=\"language-css\">.container {\n  width: 200px;\n  height: 200px;\n  background-color: red;\n  border: 1px solid;\n  overflow: auto;\n  padding: 10px;\n  margin: 20px;\n  position: relative;\n}\n.item{\n  width: 50px;\n  height: 50px;\n  background-color: blue;\n  position: absolute;\n  left: 100px;\n  top: 100px;\n}\n</code></pre>\n<p>当前效果如下：</p>\n<img src=\"https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2021-11-05-063813.png\" alt=\"image-20211105143812415\" style=\"zoom:50%;\" />\n<p>接下来我们来获取 <em>item</em> 盒子的 <em>offsetLeft</em> 以及 <em>offsetTop</em> 属性值。</p>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\nvar item = document.getElementById(&quot;item&quot;);\nconsole.log(item.offsetParent); // container 盒子 dom 对象\nconsole.log(item.offsetLeft); // 100\nconsole.log(item.offsetTop); // 100\n</code></pre>\n<p>接下来我们不对 <em>item</em> 子元素进行定位，而是使用 <em>margin</em> 的方式来设置子盒子的位置，如下：</p>\n<pre><code class=\"language-css\">.item{\n  width: 50px;\n  height: 50px;\n  background-color: blue;\n  margin: 50px;\n}\n</code></pre>\n<p>然后再次获取 <em>item</em> 盒子的 <em>offsetLeft</em> 以及 <em>offsetTop</em> 属性值，如下：</p>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\nvar item = document.getElementById(&quot;item&quot;);\nconsole.log(item.offsetParent); // container 盒子 dom 对象\nconsole.log(item.offsetLeft); // 60\nconsole.log(item.offsetTop); // 60\n</code></pre>\n<p>可以看到，打印出来的是 <em>60</em>，因为我们设置的 <em>margin</em> 的值为 <em>50</em>，但是其定了位的父元素还设置了 <em>10</em> 像素的 <em>padding</em>，所以加起来就是 <em>60</em>。</p>\n<h4 id=\"scrollheight-和-scrollwidth-属性\"><em>scrollHeight</em> 和 <em>scrollWidth</em> 属性</h4>\n<p>顾名思义，这两个属性指的是当==元素内部的内容超出其宽度和高度的时候，元素内部内容的实际宽度和高度==。</p>\n<p>如果当前元素的内容没有超过其高度或者宽度，那么返回的就是元素的可视部分宽度和高度，即和 <em>clientWidth</em> 和 <em>clientHeight</em> 属性值相同。</p>\n<pre><code class=\"language-html\">&lt;div id=&quot;container&quot; class=&quot;container&quot;&gt;Lorem ipsum dolor sit, amet consectetur adipisicing elit. Nulla repellat porro atque culpa rem sunt sed! Voluptates vel incidunt accusamus reiciendis aut, adipisci ut. Hic, impedit officia.Quis, animi beatae. Facere dolorum quasi laborum, rem facilis illum necessitatibus sint doloribus beatae\nexercitationem sapiente! Quod vel cupiditate quam libero, delectus natus.&lt;/div&gt;\n</code></pre>\n<pre><code class=\"language-css\">.container {\n  width: 200px;\n  height: 200px;\n  background-color: red;\n  border: 1px solid;\n  overflow: auto;\n  padding: 10px;\n  margin: 20px;\n}\n</code></pre>\n<p>上面的代码中，我们为 <em>container</em> 盒子加入了一些文字，使其能够产生滚动效果，接下来访问 <em>scrollHeight</em> 和 <em>scrollWidth</em> 属性，如下：</p>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\nconsole.log(&quot;scrollWidth:&quot;, container.scrollWidth); // scrollWidth: 220\nconsole.log(&quot;scrollHeight&quot;, container.scrollHeight); // scrollHeight 372\n</code></pre>\n<p>如果 <em>container</em> 盒子不具备滚动的条件，那么返回的值和 <em>clientWidth</em> 和 <em>clientHeight</em> 属性值是相同的。</p>\n<pre><code class=\"language-html\">&lt;div id=&quot;container&quot; class=&quot;container&quot;&gt;&lt;/div&gt;\n</code></pre>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\nconsole.log(&quot;scrollWidth:&quot;, container.scrollWidth); // scrollWidth: 220\nconsole.log(&quot;scrollHeight&quot;, container.scrollHeight); // scrollHeight 220\n</code></pre>\n<h3 id=\"可读可写属性\">可读可写属性</h3>\n<p>所谓的可读可写属性指的是不仅能通过 <em>JavaScript</em> 获取该属性的值，还能够通过 <em>JavaScript</em> 为该属性赋值。</p>\n<h4 id=\"scrolltop-和-scrollleft-属性\"><em>scrollTop</em> 和 <em>scrollLeft</em> 属性</h4>\n<p>这对属性是可读写的，指的是当==元素其中的内容超出其宽高的时候，元素被卷起的高度和宽度==。</p>\n<pre><code class=\"language-html\">&lt;div id=&quot;container&quot; class=&quot;container&quot;&gt;Lorem ipsum dolor sit, amet consectetur adipisicing elit. Nulla repellat porro atque culpa rem sunt sed! Voluptates vel incidunt accusamus reiciendis aut, adipisci ut. Hic, impedit officia.Quis, animi beatae. Facere dolorum quasi laborum, rem facilis illum necessitatibus sint doloribus beatae\nexercitationem sapiente! Quod vel cupiditate quam libero, delectus natus.&lt;/div&gt;\n</code></pre>\n<pre><code class=\"language-css\">.container {\n  width: 200px;\n  height: 200px;\n  background-color: red;\n  border: 1px solid;\n  overflow: auto;\n  padding: 10px;\n  margin: 20px;\n}\n</code></pre>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\ncontainer.onscroll = function () {\n  console.log(&quot;scrollTop:&quot;, container.scrollTop);\n  console.log(&quot;scrollLeft&quot;, container.scrollLeft);\n}\n</code></pre>\n<p>在上面的代码中，我们的 <em>container</em> 盒子内容超出了容器的高度，我们为该盒子绑定了 <em>scroll</em> 事件，滚动的时候打印出 <em>scrollTop</em> 和 <em>scrollLeft</em>，即元素被卷起的高度和宽度。</p>\n<p>效果如下：</p>\n<img src=\"https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2021-11-05-071632.gif\" alt=\"2021-11-05 15.15.58\" style=\"zoom:50%;\" />\n<p>该属性因为是可读可写属性，所以可以通过赋值来让内容自动滚动到某个位置。例如很多网站右下角都有回到顶部的按钮，背后对应的 <em>JavaScript</em> 代码就是通过该属性来实现的。</p>\n<h4 id=\"domobjstylexxx-属性\"><em>domObj.style.xxx</em> 属性</h4>\n<p>对于一个 <em>DOM</em> 元素来讲，它的 <em>style</em> 属性返回的也是一个对象，并且这个对象中的任意一个属性是可读写的。例如 <em>domObj.style.top、domObj.style.wdith</em> 等，在读的时候，它们返回的值常常是带有单位的（如 <em>px</em> ）。</p>\n<p>但是，对于这种方式，<strong>它只能够获取到该元素的行内样式，而并不能获取到该元素最终计算好的样式</strong>。如果想要获取计算好的样式，需要使用 *obj.currentstyle（ IE ）*和 <em>getComputedStyle</em>（ <em>IE</em> 之外的浏览器 ）</p>\n<p>另一方面，由于 <em>domObj.style.xxx</em> 属性能够被赋值，所以 <em>JavaScript</em> 控制 <em>DOM</em> 元素运动的原理就是通过不断修改这些属性的值而达到其位置改变的，需要注意的是，<strong>给这些属性赋值的时候需要带单位的要带上单位，否则不生效</strong>。</p>\n<h2 id=\"event-事件对象相关尺寸和位置属性\"><em>event</em> 事件对象相关尺寸和位置属性</h2>\n<p>对于元素的运动的操作，通常还会涉及到事件里面的 <em>event</em> 对象，而 <em>event</em> 对象也存在很多位置属性，且由于浏览器兼容性问题会导致这些属性间相互混淆，这里也来进行一个总结。</p>\n<h4 id=\"clientx-和-clienty-属性\"><em>clientX</em> 和 <em>clientY</em> 属性</h4>\n<p>这对属性是当事件发生时，==鼠标点击位置相对于浏览器（可视区）的坐标，即浏览器左上角坐标的（ <em>0 , 0</em> ）==，该属性以浏览器左上角坐标为原点，计算鼠标点击位置距离其左上角的位置，</p>\n<p>不管浏览器窗口大小如何变化，都不会影响点击位置的坐标。</p>\n<pre><code class=\"language-html\">&lt;div id=&quot;container&quot; class=&quot;container&quot;&gt;&lt;/div&gt;\n</code></pre>\n<pre><code class=\"language-css\">*{\n  margin: 0;\n  padding: 0;\n}\n.container {\n  width: 200px;\n  height: 200px;\n  background-color: red;\n  border: 1px solid;\n  overflow: auto;\n  padding: 10px;\n  margin: 20px;\n}\n</code></pre>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\ncontainer.onclick = function (ev) {\n  var evt = ev || event;\n  console.log(evt.clientX + &quot;:&quot; + evt.clientY);\n}\n</code></pre>\n<p>在上面的代码中，我们为 <em>container</em> 盒子绑定了点击事件，获取该盒子的 <em>clientX</em> 以及 <em>clientY</em> 的值，接下来我们来进行点击测试：</p>\n<img src=\"https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2021-11-05-073614.png\" alt=\"image-20211105153614467\" style=\"zoom:50%;\" />\n<p>我们分别点击该盒子的最左上角和最右下角，打印出来的值分别是（<em>20 , 20</em>）和 （<em>241 , 241</em>），可以看出这确实是以浏览器左上角坐标的（ <em>0 , 0</em> ）为原点来进行计算的。</p>\n<h4 id=\"screenx-和-screeny-属性\"><em>screenX</em> 和 <em>screenY</em> 属性</h4>\n<p><em>screenX</em> 和 <em>screenY</em> 是事件发生时鼠标相对于屏幕的坐标，以设备屏幕的左上角为原点，事件发生时鼠标点击的地方即为该点的 <em>screenX</em> 和 <em>screenY</em> 值。例如：</p>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\ncontainer.onclick = function (ev) {\n  var evt = ev || event;\n  console.log(evt.screenX + &quot;:&quot; + evt.screenY);\n}\n</code></pre>\n<img src=\"https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2021-11-05-074500.png\" alt=\"image-20211105154500066\" style=\"zoom:50%;\" />\n<p>我们将浏览器缩小，同样是点击 <em>container</em> 盒子的最左上角，打印出来的是（<em>368 , 365</em>），因为这是以屏幕最左上角为原点的。</p>\n<h4 id=\"offsetx-和-offsety-属性\"><em>offsetX</em> 和 <em>offsetY</em> 属性</h4>\n<p>这一对属性是指当事件发生时，==鼠标点击位置相对于该事件源的位置，即点击该 <em>DOM</em> 元素，以该 <em>DOM</em> 左上角为原点来计算鼠标点击位置的坐标==。例如：</p>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\ncontainer.onclick = function (ev) {\n  var evt = ev || event;\n  console.log(&quot;offsetX:&quot;, evt.offsetX);\n  console.log(&quot;offsetY:&quot;, evt.offsetY);\n}\n</code></pre>\n<p>同样点击 <em>container</em> 元素的最左上角，打印出（ <em>0, 0</em> ）</p>\n<h4 id=\"pagex-和-pagey-属性\"><em>pageX</em> 和 <em>pageY</em> 属性</h4>\n<p>顾名思义，该属性是事件发生时鼠标点击位置相对于页面的位置，通常浏览器窗口没有出现滚动条时，该属性和 <em>clientX</em> 及 <em>clientY</em> 是等价的。</p>\n<p>例如：</p>\n<pre><code class=\"language-js\">var container = document.getElementById(&quot;container&quot;);\ncontainer.onclick = function (ev) {\n  var evt = ev || event;\n  console.log(&quot;pageX:&quot;, evt.pageX);\n  console.log(&quot;pageY:&quot;, evt.pageY);\n  console.log(&quot;clientX:&quot;, evt.clientX);\n  console.log(&quot;clientY:&quot;, evt.clientY);\n}\n</code></pre>\n<p>此时点击 <em>container</em> 盒子，得到的 <em>pageX、pageY</em> 的值和 <em>clientX、clientY</em> 完全相同。</p>\n<p>但是当浏览器出现滚动条的时候，<em>pageX</em> 通常会大于 <em>clientX</em>，因为页面还存在被卷起来的部分的宽度和高度。</p>\n<p>例如：</p>\n<pre><code class=\"language-css\">...\nbody{\n  height: 5000px;\n}\n...\n</code></pre>\n<p>我们为 <em>body</em> 添加一个 <em>height</em> 为 <em>500px</em>，使其能够产生滚动效果，此时两组属性的区别就出来了。如下：</p>\n<img src=\"https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2021-11-05-080641.gif\" alt=\"2021-11-05 16.06.06\" style=\"zoom:50%;\" />\n<hr />\n<p>-<em>EOF</em>-</p>\n', '[{\"name\":\"尺寸和位置\",\"anchor\":\"尺寸和位置\",\"children\":[{\"name\":\"*DOM* 对象相关尺寸和位置属性\",\"anchor\":\"dom-对象相关尺寸和位置属性\",\"children\":[{\"name\":\"只读属性\",\"anchor\":\"只读属性\",\"children\":[{\"name\":\"*clientWidth* 和 *clientHeight* 属性\",\"anchor\":\"clientwidth-和-clientheight-属性\",\"children\":[]},{\"name\":\"*offsetWidth* 和 *offsetHeight* 属性\",\"anchor\":\"offsetwidth-和-offsetheight-属性\",\"children\":[]},{\"name\":\"*clientTop* 和 *clientLeft* 属性\",\"anchor\":\"clienttop-和-clientleft-属性\",\"children\":[]},{\"name\":\"*offsetLeft* 和 *offsetTop* 属性\",\"anchor\":\"offsetleft-和-offsettop-属性\",\"children\":[]},{\"name\":\"*scrollHeight* 和 *scrollWidth* 属性\",\"anchor\":\"scrollheight-和-scrollwidth-属性\",\"children\":[]}]},{\"name\":\"可读可写属性\",\"anchor\":\"可读可写属性\",\"children\":[{\"name\":\"*scrollTop* 和 *scrollLeft* 属性\",\"anchor\":\"scrolltop-和-scrollleft-属性\",\"children\":[]},{\"name\":\"*domObj.style.xxx* 属性\",\"anchor\":\"domobjstylexxx-属性\",\"children\":[]},{\"name\":\"*clientX* 和 *clientY* 属性\",\"anchor\":\"clientx-和-clienty-属性\",\"children\":[]},{\"name\":\"*screenX* 和 *screenY* 属性\",\"anchor\":\"screenx-和-screeny-属性\",\"children\":[]},{\"name\":\"*offsetX* 和 *offsetY* 属性\",\"anchor\":\"offsetx-和-offsety-属性\",\"children\":[]},{\"name\":\"*pageX* 和 *pageY* 属性\",\"anchor\":\"pagex-和-pagey-属性\",\"children\":[]}]}]},{\"name\":\"*event* 事件对象相关尺寸和位置属性\",\"anchor\":\"event-事件对象相关尺寸和位置属性\",\"children\":[]}]}]', '/static/upload/obvtqc-1681490866394.jpg', '2', '0', '0', '1681490871209', '1', '2');

## *this* 指向总结



*this* 关键字是一个非常重要的语法点。毫不夸张地说，不理解它的含义，大部分开发任务都无法完成。

*this* 可以用在构造函数之中，表示实例对象。除此之外，*this* 还可以用在别的场合。**但不管是什么场合，*this* 都有一个共同点：它总是返回一个对象**。



关于 *this* 的指向，有一种广为流传的说法就是“谁调用它，*this* 就指向谁”。

这样的说法没有太大的问题，但是并不是太全面。总结起来，*this* 的指向规律有如下几条：



- 在函数体中，非显式或隐式地简单调用函数时，在严格模式下，函数内的 *this* 会被绑定到 *undefined* 上，在非严格模式下则会被绑定到全局对象 *window/global* 上。

  

- 一般使用 *new* 方法调用构造函数时，构造函数内的 *this* 会被绑定到新创建的对象上。

  

- 一般通过 *call/apply/bind* 方法显式调用函数时，函数体内的 *this* 会被绑定到指定参数的对象上。

  

- 一般通过上下文对象调用函数时，函数体内的 *this* 会被绑定到该对象上。

  

- 在箭头函数中，*this* 的指向是由外层（函数或全局）作用域来决定的。



当然，真实环境多种多样，下面我们就来根据实战例题逐一梳理。



### 全局环境中的 *this*

例题 *1*：

```js
function f1() {
    console.log(this);
}

function f2() {
    'use strict'
    console.log(this);
}

f1(); // window or global
f2(); // undefined
```

==这种情况相对简单、直接，函数在浏览器全局环境下被简单调用，在非严格模式下 *this* 指向 *window*，在通过 *use strict* 指明严格模式的情况下指向 *undefined*。==

虽然上面的题目比较基础，但是需要注意上面题目的变种，例如

例题 *2*：

```js
const foo = {
    bar : 10,
    fn : function(){
        console.log(this); // window or global
        console.log(this.bar); // undefined
    }
}
var fn1 = foo.fn;
fn1();
```

这里的 *this* 仍然指向 *window*。虽然 *fn* 函数在 *foo* 对象中作为该对象的一个方法，但是在赋值给 *fn1* 之后，*fn1* 仍然是在 *window* 的全局环境下执行的。因此上面的代码仍然会输出 *window* 和 *undefined*。

还是上面这道题目，如果改成如下的形式

例题 *3*：

```js
const foo = {
    bar : 10,
    fn : function(){
        console.log(this); // { bar: 10, fn: [Function: fn] }
        console.log(this.bar); // 10
    }
}
foo.fn();
```

这时，*this* 指向的是最后调用它的对象，在 *foo.fn( )* 语句中，this 指向的是 *foo* 对象。



### 上下文对象调用中的 *this*



例题 *4*：

```js
const student = {
    name: 'zhangsan',
    fn: function () {
        return this;
    }
}
console.log(student.fn() === student); // true
```

在上面的代码中，*this* 指向当前的对象 *student*，所以最终会返回 *true*。

当存在更复杂的调用关系时，如以下代码中的嵌套关系，*this* 将指向最后调用它的对象，例如



例题 *5*：

```js
const student = {
    name: 'zhangsan',
    son: {
        name: 'zhangxiaosan',
        fn: function () {
            return this.name
        }
    }
}
console.log(student.son.fn()); // zhangxiaosan
```

在上面的代码中，*this* 会指向最后调用它的对象，因此输出的是 *zhangxiaosan*。

至此，*this* 的上下文对象调用已经介绍得比较清楚了。我们再来看一道比较高阶的题目

例题 *6*：

```js
const o1 = {
    text: 'o1',
    fn: function () {
        return this.text;
    }
}

const o2 = {
    text: 'o2',
    fn: function () {
        return o1.fn();
    }
}

const o3 = {
    text: 'o3',
    fn: function () {
        var fn = o1.fn;
        return fn();
    }
}

console.log(o1.fn()); // o1
console.log(o2.fn()); // o1
console.log(o3.fn()); // undefined
```

答案是 *o1、o1、undefined*。

这里主要讲一下为什么第三个是 *undefined*。这里将 *o1.fn* 赋值给了 *fn*，所以 *fn* 等价于 *function () { return this.text; }*，然后该函数在调用的时候，是直接 *fn( )* 的形式调用的，并不是以对象的形式，相当于还是全局调用，指向 *window*，所以打印出 *undefined*。



### *this* 指向绑定事件的元素



==*DOM* 元素绑定事件时，事件处理函数里面的 *this* 指向绑定了事件的元素==。

这个地方一定要注意它和 *target* 的区别，*target* 是指向触发事件的元素。

示例如下：

```html
<ul id="color-list">
  <li>red</li>
  <li>yellow</li>
  <li>blue</li>
  <li>green</li>
  <li>black</li>
  <li>white</li>
</ul>
```

```js
// this 是绑定事件的元素
// target 是触发事件的元素 和 srcElememnt 等价
let colorList = document.getElementById("color-list");
colorList.addEventListener("click", function (event) {
  console.log('this:', this);
  console.log('target:', event.target);
  console.log('srcElement:', event.srcElement);
})
```

当我点击如下位置时打印出来的信息如下：

<img src="https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2021-09-28-033304.png" alt="image-20210928113303839" style="zoom:50%;" />



有些时候我们会遇到一些困扰，比如在 *div* 节点的事件函数内部，有一个局部的 *callback* 方法，该方法被作为普通函数调用时，*callback* 内部的 *this* 是指向全局对象 *window* 的

例如：

```html
<div id="div1">我是一个div</div>
```

```js
window.id = 'window';
document.getElementById('div1').onclick = function(){
  console.log(this.id); // div1
  const callback = function(){
    console.log(this.id); // 因为是普通函数调用，所以 this 指向 window
  }
  callback();
}
```

==此时有一种简单的解决方案，可以用一个变量保存 *div* 节点的引用，如下：==

```js
window.id = 'window';
document.getElementById('div1').onclick = function(){
  console.log(this.id); // div1
  const that = this; // 保存当前 this 的指向
  const callback = function(){
    console.log(that.id); // div1
  }
  callback();
}
```



### 改变 *this* 指向



#### 1. *call、apply、bind* 方法修改 *this* 指向

> ==函数执行时进行绑定==

由于 *JavaScript*  中 *this* 的指向受函数运行环境的影响，指向经常改变，使得开发变得困难和模糊，所以在封装 *sdk* 或者写一些复杂函数的时候经常会用到 *this* 指向绑定，以避免出现不必要的问题。

*call、apply、bind* 基本都能实现这一功能，起到确定 *this* 指向的作用



***Function.prototype.call( )***



*call* 方法可以指定 *this* 的指向（即函数执行时所在的的作用域），然后再指定的作用域中，执行函数。



```js
var obj = {};
var f = function(){
	return this;
};
console.log(f() === window);  // this 指向 window
console.log(f.call(obj) === obj) // 改变this 指向 obj
```

上面代码中，全局环境运行函数 *f* 时，*this* 指向全局环境（浏览器为 *window* 对象）；

*call* 方法可以改变 *this* 的指向，指定 *this* 指向对象 *obj*，然后在对象 *obj* 的作用域中运行函数 *f*。



==*call* 方法的参数，应该是对象 *obj*，如果参数为空或 *null、undefind*，则默认传参全局对象。==

```js
var n = 123;
var obj = { n: 456 };

function a() {
  console.log(this.n);
}

a.call() // 123
a.call(null) // 123
a.call(undefined) // 123
a.call(window) // 123
a.call(obj) // 456
```

上面代码中，*a* 函数中的 *this* 关键字，如果指向全局对象，返回结果为 *123*。

如果使用 *call* 方法将 *this* 关键字指向 *obj* 对象，返回结果为 *456*。可以看到，如果 *call* 方法没有参数，或者参数为 *null* 或 *undefined*，则等同于指向全局对象。



==如果 *call* 传参不是以上类型，则转化成对应的包装对象，然后传入方法。==

例如，*5* 转成 *Number* 实例，绑定 *f* 内部 *this*

```js
var f = function () {
  return this;
};

f.call(5); // Number {[[PrimitiveValue]]: 5}
```

==*call* 可以接受多个参数，第一个参数是 *this* 指向的对象，之后的是函数回调所需的参数。==

```js
function add(a, b) {
  return a + b;
}

add.call(this, 1, 2) // 3
```

==*call* 方法的一个应用是调用对象的原生方法。==

```js
var obj = {};
obj.hasOwnProperty('toString') // false

// 覆盖掉继承的 hasOwnProperty 方法
obj.hasOwnProperty = function () {
  return true;
};
obj.hasOwnProperty('toString') // true

Object.prototype.hasOwnProperty.call(obj, 'toString') // false
```

上面代码中 *hasOwnProperty* 是 *obj* 继承来的方法，用来判断对象是否包含自身特点（非继承）属性，但是 *hasOwnProperty* 并不是保留字，如果被对象覆盖，会造成结果错误。

*call* 方法可以解决这个问题，它将 *hasOwnProperty* 方法的原始定义放到 *obj* 对象上执行，这样无论 *obj* 上有没有同名方法，都不会影响结果。



***Function.prototype.apply( )***



*apply* 和 *call* 作用类似，也是改变 *this* 指向，然后调用该函数，唯一区别是 *apply* 接收数组作为函数执行时的参数。语法如下：

```js
func.apply(thisValue, [arg1, arg2, ...])
```

==*apply* 方法的第一个参数也是 *this* 所要指向的那个对象，如果设为 *null* 或 *undefined*，则等同于指定全局对象。==

==第二个参数则是一个数组，该数组的所有成员依次作为参数，传入原函数。==

原函数的参数，在 *call* 方法中必须一个个添加，但是在 *apply* 方法中，必须以数组形式添加。

```js
function f(x, y){
  console.log(x + y);
}

f.call(null, 1, 1) // 2
f.apply(null, [1, 1]) // 2
```

利用这一特性，可以实现很多小功能。==比如，输出数组的最大值：==

```js
var a = [24,30,2,33,1]
Math.max.apply(null,a)  //33
```

还可以将数组中的空值，转化成 *undefined*。

通过 *apply* 方法，利用 *Array* 构造函数将数组的空元素变成 *undefined*。

```js
var a = ['a',,'b'];
console.log(Array.apply(null,a)); //['a',undefind,'b']
```

空元素与 *undefined* 的差别在于，==数组的 *forEach* 方法会跳过空元素，但是不会跳过 *undefined*。因此，遍历内部元素的时候，会得到不同的结果。==

```js
var a = ['a', , 'b'];

function print(i) {
  console.log(i);
}

a.forEach(print)
// a
// b

Array.apply(null, a).forEach(print)
// a
// undefined
// b
```

==配合数组对象的 *slice* 方法，可以将一个类似数组的对象（比如 *arguments* 对象）转为真正的数组。==

```js
Array.prototype.slice.apply({0: 1, length: 1}) // [1]
Array.prototype.slice.apply({0: 1}) // []
Array.prototype.slice.apply({0: 1, length: 2}) // [1, undefined]
Array.prototype.slice.apply({length: 1}) // [undefined]
```

上面代码的 *apply* 方法的参数都是对象，但是返回结果都是数组，这就起到了将对象转成数组的目的。

从上面代码可以看到，==这个方法起作用的前提是，被处理的对象必须有 *length* 属性，以及相对应的数字键。==



***Function.prototype.bind( )***



*bind* 用于将函数体内的 *this* 绑定到某个对象，==然后返回一个新函数==

> ==bind绑定后，函数内部this不再取决于怎么调用函数 函数内部的this都固定为了bind的对象== ==直接绑死==

```js
var d = new Date();
d.getTime() // 1481869925657

var print = d.getTime;
print() // Uncaught TypeError: this is not a Date object.
```

报错是因为 *d.getTime* 赋值给 *print* 后，*getTime* 内部的 *this* 指向方式变化，已经不再指向 *date* 对象实例了。

解决方法：

```js
var print = d.getTime.bind(d);
print() // 1481869925657
```

*bind* 接收的参数就是所要绑定的对象

```js
var counter = {
  count: 0,
  inc: function () {
    this.count++;
  }
};

var func = counter.inc.bind(counter);
func();
counter.count // 1
```

绑定到其他对象

```js
var counter = {
  count: 0,
  inc: function () {
    this.count++;
  }
};

var obj = {
  count: 100
};
var func = counter.inc.bind(obj);
func();
obj.count // 101
```

*bind* 还可以接收更多的参数，将这些参数绑定到原函数的参数

```js
var add = function (x, y) {
  return x * this.m + y * this.n;
}

var obj = {
  m: 2,
  n: 2
};

var newAdd = add.bind(obj, 5);
newAdd(5) // 20
```

上面代码中，==*bind* 方法除了绑定 *this* 对象，还将 *add* 函数的第一个参数 *x* 绑定成 *5*，然后返回一个新函数 *newAdd*，这个函数只要再接受一个参数 *y* 就能运行了。==



==如果 *bind* 方法的第一个参数是 *null* 或 *undefined*，等于将 *this* 绑定到全局对象，函数运行时 *this* 指向顶层对象（浏览器为 *window*）。==

```js
function add(x, y) {
  return x + y;
}

var plus5 = add.bind(null, 5);
plus5(10) // 15
```

上面代码中，函数 *add* 内部并没有 *this*，使用 *bind* 方法的主要目的是绑定参数 *x*，以后每次运行新函数 *plus5*，就只需要提供另一个参数 *y* 就够了。

而且因为 *add* 内部没有 *this*，所以 *bind* 的第一个参数是 *null*，不过这里如果是其他对象，也没有影响。



*bind* 方法有一些使用注意点。

（1）每一次返回一个新函数

==*bind* 方法每运行一次，就返回一个新函数==，这会产生一些问题。比如，监听事件的时候，不能写成下面这样。

```
element.addEventListener('click', o.m.bind(o));
```

上面代码中，*click* 事件绑定 *bind* 方法生成的一个匿名函数。这样会导致无法取消绑定，所以，下面的代码是无效的。

```js
element.removeEventListener('click', o.m.bind(o));
```

正确的方法是写成下面这样：

```js
var listener = o.m.bind(o);
element.addEventListener('click', listener);
//  ...
element.removeEventListener('click', listener);
```

（2）结合回调函数使用

回调函数是 *JavaScript* 最常用的模式之一，但是一个常见的错误是，将包含 *this* 的方法直接当作回调函数。解决方法就是使用 *bind* 方法，将 *counter.inc* 绑定 *counter*。

```js
var counter = {
  count: 0,
  inc: function () {
    'use strict';
    this.count++;
  }
};

function callIt(callback) {
  callback();
}

callIt(counter.inc.bind(counter));
counter.count // 1
```

上面代码中，*callIt* 方法会调用回调函数。这时如果直接把 *counter.inc* 传入，调用时 *counter.inc* 内部的 *this* 就会指向全局对象。使用 *bind* 方法将 *counter.inc* 绑定 *counter* 以后，就不会有这个问题，*this* 总是指向 *counter*。

还有一种情况比较隐蔽，就是某些数组方法可以接受一个函数当作参数。这些函数内部的 *this* 指向，很可能也会出错。

```js
var obj = {
  name: '张三',
  times: [1, 2, 3],
  print: function () {
    this.times.forEach(function (n) {
      console.log(this.name);
    });
  }
};

obj.print()
// 没有任何输出
```

上面代码中，*obj.print* 内部 *this.times* 的 *this* 是指向 *obj* 的，这个没有问题。

==但是，*forEach* 方法的回调函数内部的 *this.name* 却是指向全局对象，导致没有办法取到值。==稍微改动一下，就可以看得更清楚。

```js
obj.print = function () {
  this.times.forEach(function (n) {
    console.log(this === window);
  });
};

obj.print()
// true
// true
// true
```

==解决这个问题，也是通过 *bind* 方法绑定 *this*。==

```js
obj.print = function () {
  this.times.forEach(function (n) {
    console.log(this.name);
  }.bind(this));
};

obj.print()
// 张三
// 张三
// 张三
```

（3）==结合 *call* 方法使用==

利用 *bind* 方法，可以改写一些 *JavaScript* 原生方法的使用形式，以数组的 *slice* 方法为例。

```js
[1, 2, 3].slice(0, 1) // [1]
// 等同于
Array.prototype.slice.call([1, 2, 3], 0, 1) // [1]
```

上面的代码中，数组的 *slice* 方法从 *[1, 2, 3]* 里面，按照指定位置和长度切分出另一个数组。这样做的本质是在 *[1, 2, 3]* 上面调用 *Array.prototype.slice* 方法，因此可以用 *call* 方法表达这个过程，得到同样的结果。

*call* 方法实质上是调用 *Function.prototype.call* 方法，因此上面的表达式可以用 *bind* 方法改写。

```js
var slice = Function.prototype.call.bind(Array.prototype.slice);
slice([1, 2, 3], 0, 1) // [1]
```

上面代码的含义就是，将 *Array.prototype.slice* 变成 *Function.prototype.call* 方法所在的对象，调用时就变成了 *Array.prototype.slice.call*。类似的写法还可以用于其他数组方法。

```js
var push = Function.prototype.call.bind(Array.prototype.push);
var pop = Function.prototype.call.bind(Array.prototype.pop);

var a = [1 ,2 ,3];
push(a, 4)
a // [1, 2, 3, 4]

pop(a)
a // [1, 2, 3]
```

如果再进一步，将 *Function.prototype.call* 方法绑定到 *Function.prototype.bind* 对象，就意味着 *bind* 的调用形式也可以被改写。

```js
function f() {
  console.log(this.v);
}

var o = { v: 123 };
var bind = Function.prototype.call.bind(Function.prototype.bind);
bind(f, o)() // 123
```

上面代码的含义就是，将 *Function.prototype.bind* 方法绑定在 *Function.prototype.call* 上面，所以 *bind* 方法就可以直接使用，不需要在函数实例上使用。



#### 2. 箭头函数的 *this* 指向



当我们的 *this* 是以函数的形式调用时，*this* 指向的是全局对象。

不过对于箭头函数来讲，却比较特殊。==箭头函数的 *this* 指向始终为外层的作用域。==

先来看一个普通函数作为对象的一个方法被调用时，*this* 的指向，如下：

```js
const obj = {
    x : 10,
    test : function(){
        console.log(this); // 指向 obj 对象
        console.log(this.x); // 10
    }
}
obj.test();
// { x: 10, test: [Function: test] }
// 10
```

可以看到，普通函数作为对象的一个方法被调用时，*this* 指向当前对象。

在上面的例子中，就是 *obj* 这个对象，*this.x* 的值为 *10*。



接下来是箭头函数以对象的方式被调用的时候的 *this* 的指向，如下：

```js
var x = 20;
const obj = {
    x: 10,
    test: () => {
        console.log(this); // {}
        console.log(this.x); // undefined
    }
}
obj.test();
// {}
// undefined
```

这里的结果和上面不一样，*this* 打印出来为 { }，而 *this.x* 的值为 *undefined*。

为什么呢？

实际上刚才我们有讲过，箭头函数的 *this* 指向与普通函数不一样，它的 *this* 指向始终是指向的外层作用域。==所以这里的 *this* 实际上是指向的全局对象。==

如果证明呢？

方法很简单，将这段代码放入浏览器运行，在浏览器中用 *var* 所声明的变量会成为全局对象 *window* 的一个属性，如下：

<img src="https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2021-09-28-052059.png" alt="image-20210928132058878" style="zoom:50%;" />



接下来我们再来看一个例子，来证明箭头函数的 *this* 指向始终是指向的外层作用域。

```js
var name = "JavaScript";
const obj = {
    name: "PHP",
    test: function () {
        const i = function () {
            console.log(this.name);
            // i 是以函数的形式被调用的，所以 this 指向全局
            // 在浏览器环境中打印出 JavaScript，node 里面为 undeifned
        }
        i();
    }
}
obj.test(); // JavaScript
```

==接下来我们将 i 函数修改为箭头函数，如下：==

```js
var name = "JavaScript";
const obj = {
    name : "PHP",
    test : function(){
        const i = ()=>{
            console.log(this.name);
            // 由于 i 为一个箭头函数，所以 this 是指向外层的
            // 所以 this.name 将会打印出 PHP
        }
        i();
    }
}
obj.test();// PHP
```

==最后需要说一点的就是，箭头函数不能作为构造函数，如下：==

```js
const Test = (name, age) => {
    this.name = name;
    this.age = age;
};
const test = new Test("xiejie", 18);
// TypeError: Test is not a constructor
```



## 真题解答



- *this* 的指向哪几种 ？

> 参考答案：
>
> 总结起来，*this* 的指向规律有如下几条：
>
> - 在函数体中，非显式或隐式地简单调用函数时，在严格模式下，函数内的 *this* 会被绑定到 *undefined* 上，在非严格模式下则会被绑定到全局对象 *window/global* 上。
> - 一般使用 *new* 方法调用构造函数时，构造函数内的 *this* 会被绑定到新创建的对象上。
> - 一般通过 *call/apply/bind* 方法显式调用函数时，函数体内的 *this* 会被绑定到指定参数的对象上。
> - 一般通过上下文对象调用函数时，函数体内的 *this* 会被绑定到该对象上。
> - 在箭头函数中，*this* 的指向是由外层（函数或全局）作用域来决定的。



-*EOF*-