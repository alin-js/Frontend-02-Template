# DOM API
### 节点类型
* Element（元素型节点，跟标签相对应）
    * HTMLElement
        * HTMLAnchorElement
        * HTMLAppletElement
        * HTMLAreaElement
        * HTMLAudioElement
        * HTMLBaseElement
        * HTMLBodyElement
        * ...
    * SVGElement
        * SVGAElement
        * SVGAltGlyphElement
        * ...
* Document：文档根节点
* CharacterData ：字符数据
    * Text ： 文本节点
        * CDATASection：CDATA节点
    * Comment：注释节点
    * ProcessingInstruction ： 处理信息
* DocumentFragment：文档片段
* DocumentType ： 文档类型


### 元素操作

#### 节点导航
* `parentNode`  父节点
* `childNodes`  子节点
* `firstChild` 第一个子节点
* `lastChild` 最后一个子节点
* `nextSibling` 下一个邻居节点
* `previousSibling` 上一个邻居节点

#### 元素导航
只是寻找元素的，文本节点（比如text，comment等节点都会被忽略）
* `parentElement`
* `children`
* `firstElementChild`
* `lastElementChild`
* `nextElementSibling`
* `previousElementSibling`

#### 修改操作
* `appendChild` 添加节点
* `insertBefore`  插入节点
* `removeChild` 移除节点，在其父节点上进行
* `replaceChild` 替换节点

#### 高级操作
* `compareDocumentPosition` 比较两个节点关系的函数，返回前后的一个关系
* `contains` 检查一个节点是否包含另一个节点的函数
* `isEqualNode` 检查两个节点是否完全相同
* `isSameNode` 检查两个节点是否是同一个节点
* `cloneNode` 复制一个节点，如果传入参数true，会连同子元素做深拷贝

# 事件API
#### 事件的对象模型
**冒泡和捕获**
在一个事件发生时，捕获过程跟冒泡过程总是先后发生，跟你是否监听毫无关联；
在我们实际监听事件时，我建议这样使用冒泡和捕获机制：默认使用冒泡模式，当开发组件时，遇到需要父元素控制子元素的行为，可以使用捕获机制

addEventListener 有三个参数：
* 事件名称；
* 事件处理函数；
* 捕获还是冒泡。

第三个参数不一定是 bool 值，也可以是个对象，它提供了更多选项。
* once：只执行一次。
* passive：承诺此事件监听不会调用 
* preventDefault，这有助于性能。
* useCapture：是否捕获（否则冒泡）。

# Range API
range的基本用法
```
// 创建range
var range = new Range()
range.setStart(element,9);
range.setEnd(element,4);

// 另外一种创建range
var range = document.getSelection().getRangeAt(0)
```

其他api

* `range.setStartBefore`  起点设到某个节点之前
* `range.setEndBefore` 终点设到某个节点之前
* `range.setStartAfter` 起点设到某个节点之后
* `range.setEndAfter`  终点设到某个节点之前
* `range.selectNode` 选中一个元素
* `range.selectNodeContents`  选中一个元素的所有的内容
* `var fragment = range.extractContents()`  // range中的内容取出来
* `range.insertNode(document.createTextNode('aaa'))` // range位置插入一个节点

# CSSOM
 > document.styleSheets 访问css API的方法
 
 Rules

* `document.styleSheets[0].cssRules` 
* `document.styleSheets[0].insertRule("p{color:pink;}",0)`  // 插入css规则
* `document.styleSheets[0].removeRule(0)`  // 移除css规则
* `CSSStyleRule`
    * selectorText String
    * style K-V结构
* `CSSCharsetRule`
* `CSSImportRule`
* `CSSMediaRule`
* `CSSFontFaceRule`
* `CSSPageRule`
* `CSSNamespaceRule`
* `CSSKeyframesRule`
* `CSSKeyframeRule`
* `CSSSupportsRule`


window.getComputedStyle(elt,pseudoElt); // elt:想要获取的元素  pseudoElt: 可选，伪元素

# CSSOM View
### window
window 浏览器窗口：
* `windows.innerHeight，window.innerWidth`  浏览器实际渲染所用的区域的宽和高（重要）
* `windows.outerHeight，window.outerWidth`  浏览器窗口总共占的宽和高(包含工具栏、 状态栏)
* `window.devicePixelRadio`  屏幕的物理像素和代码逻辑像素的一个比值，正常设备是1:1（重要）
* `window.screen`
    * `window.screen.width` 屏幕宽
    * `window.screen.height` 屏幕高
    * `window.screen.availWidth` 可以使用的宽
    * `window.screen.availHeight` 可以使用的高
    
* `window.open('about:blank','blank','width=100,height=100,left:100,right:100')`
* `moveTo(x,y)`  改变窗口位置
* `moveBy(x,y)`
* `resizeTo(x,y)`  改变窗口尺寸
* `resizeBy(x,y)`

### scroll
##### scroll的元素：
* `scrollTop` 当前滚动到的距顶部的位置
* `scrollLeft` 当前滚动到的距左侧的位置
* `scrollWidth` 可滚动内容的最大宽度
* `scrollHeight` 可滚动内容的最大高度
* `scroll(x,y)` 滚动到特定位置
* `scrollBy(x,y)` 在当前的基础上滚动一个差值
* `scrollIntoView()` 强制滚动到屏幕的可见区域

##### window的scroll
* `scrollX` 当前滚动到的距左侧的位置
* `scrollY`  当前滚动到的距顶部的位置
* `scroll(x,y)` 滚动到特定位置
* `scrollBy(x,y)` 在当前的基础上滚动一个差值

### layout
* getClientRects() 获取某个元素生成的所有的盒
* getBoundlingClientRect() 获取某个元素生成的盒

