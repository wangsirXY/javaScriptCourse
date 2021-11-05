# 第四章：JQuery

## javascript 库

> JavaScript 库：即 librark，是一个封好的特定的集合（方法和函数）。
>
> **简单理解：js 文件里，里面对我们原生js代码进行封装，存到里面，可以高效实用这些封装好的功能。**

## JQuery 认知

> JQuery 是一个快速、简洁的 JavaScript 库，其设计的宗旨是 倡导写更少的代码，做更多的事。
>
> **优点：**
>
> 1. 轻量级。核心文件小，不影响页面加载速度
> 2. 跨浏览器兼容
> 3. 链式编程、隐士迭代
> 4. 对事件、样式、动画支持，大大简化了DOM操作
> 5. 支持插件开发。有丰富的第三方插件：树形菜单、日期控件、轮播图 等
> 6. 免费、开源

### 下载地址

- JQuery官网下载地址：https://jquery.com
- 各版本下载地址：https://code.jquery.com
- **jQuery 库下载地址：https://www.bootcdn.cn/**



## $ 符

> $ 是 JQuery 的顶级对象
>
> **$ 是方法，可以加 () 调用**

```javascript
/ 语法格式：
$('css选择器');
```

$ 是 jQuery 的别称

```javascript
/ 底层源码
window.jQuery == window.$;

$('div') === jQuery('div');
```

调用 hide 方法 隐藏 div

```javascript
$(function() {
    // 隐藏 div
    $('div').hide();
    // 显示 div
    $('div').show();
});
```



DOM 对象 和 jQuery对象

> DOM对象获取的对象结构是 对象，jQuery 获取的对象是伪数组，下标0 是当前元素对象

```javascript
// DOM 获取元素对象
let div = document.querySelector('div');

// jQuery 获取元素对象
$('div');
```



## jQuery对象 和 DOM 对象 的转换

### jQuery对象 转 DOM 对象

```javascript
// 获取视频文件，通过转DOM，实现播放
let video = $('video');

// 通过伪数组 获取第一项
div[0].play();

// 通过jQuery封装好的get方法
div.get(0).play();
```



### DOM 对象 转 jQuery对象

```javascript
let video = document.querySelector('video');

// 转 jQuery对象，调用jQuery方法
$(video).play();
```



## 隐士迭代

待补充



## jQuery 选择器

> 原生 js 获取元素的方式很杂，兼容性情况不一致，因此 jQuery 给我们做了封装，使获取元素统一标准。

|    名称    |      用法       |           说明           |
| :--------: | :-------------: | :----------------------: |
| ID 选择器  |    $("#id")     |    获取指定 ID 的元素    |
| 全能选择器 |     $("*")      |       匹配所有元素       |
|  类选择器  |   $(".class")   | 获取同一类 class 的元素  |
| 标签选择器 |    $("div")     | 获取同一类标签的所有元素 |
| 并集选择器 | $("div, p, li") |      旋转轴多个元素      |
| 交集选择器 | $("li.current") |         交集元素         |



## 筛选选择器

> 筛选选择器，是在所有的选项中选择满足条件的进行筛选选择。

|    语法    |     用法      |                    说明                    |
| :--------: | :-----------: | :----------------------------------------: |
|   :first   | $("li:first") |             获取第一个 li 元素             |
|   :last    | $("li:last")  |            获取最后一个 li 元素            |
| :eq(index) | $("li:eq(2)") | 获取到的 li 元素中，选择索引号为 2 的元素  |
|    :odd    |  $("li:odd")  | 获取到的 li 元素中，选择索引号为奇数的元素 |
|   :even    | $("li:even")  | 获取到的 li 元素中，选择索引号为偶数的元素 |

> :eq(index) 方法 访问的是下标，下标从 0 开始

```javascript
$(function () {
	// 选中 ul 中第一个 li 的css样式
    $('ul :first').css('color', '#f00');
    $('ul li').eq(0).css('color', '#f00');
   	
    // 选中 ul 中的偶数个 li
    $('ul li:odd').css('color', '#f00');
    
    // 选中 ul 中的奇数个 li
    $('ul li:even').css('color', '#f00');
    
});
```



## 兄弟元素 判断类名

> sublings：兄弟元素
>
> hasClass：查询是否包含类名

```html
<ul>
    <li>列表</li>
    <li class="item">列表</li>
    <li>列表</li>
</ul>


<script>
	$(function () {
        // 所有的兄弟元素（除了自己，其余兄弟元素全部设置红色
    	$('ul .item').sublings().css('color', '#f00');
        
        // 获取所有li，判断是否有 item 类
        $('div').eq(0).hasClass('item');	// false
        $('div').eq(1).hasClass('item');	// true
    });
</script>
```



## 获取元素的方法

|  方法名   |         说明         |
| :-------: | :------------------: |
| parent(s) | 父元素（所有的父级） |
| children  |        亲儿子        |
|   find    |      所有的后代      |

children 和 find 可以传参数也可以不传参数

```javascript
父元素.children('要查询的子元素');
子元素.find('要查询的父元素');
```



```html
<div class="grand">
    <div class="father">
        <div class="son">儿子</div>
    </div>
</div>


<script>
	$(function () {
        // 获取最近的父元素
        let p = $('.son').parent();
        // 获取所有父级
        let p = $('.son').parents();
        
        // 获取亲儿子
        let f = $('.grand').children();
        // 获取所有后代
        let f = $('.grand').find('div');
    });
</script>
```



## 排他思想

> this 是 DOM 对象，要转成 jQuery 对象

```javascript
$(function () {
    // 所有按钮 绑定点击事件（隐士迭代）
    $('button').click(function () {
        // 当前元素添加颜色
        $(this).css('background', '#f00');
        // 其余兄弟元素去除颜色
        $(this).siblings().css('background', '');
        
        // 简写：链式编程
        $(this).css('background', '#f00').sublings().css('background', '');
    });
};
```



## jQuery 操作 css 的方法

>设置css属性，使用对象套键值的方法进行设置

```javascript
// 语法格式：
$(function () {
	$('标签名').css({
        键: 值,
    });
});
```

==设置css样式时，值为数值的时候，可以不写单位，如果要写单位，必须加上 "" 转字符串==

```javascript
$(function () {
    $('div').css({
        width: 300,
        height: 300,
        margin: '400px',
    });
});
```



## jQuery 操作 类 的方法

|     方法      |   说明   |
| :-----------: | :------: |
|  addClass()   | 添加类名 |
| removeClass() | 删除类名 |
| toggleClass() | 切换类名 |



### 添加删除类名

>addClass 和 removeClass 不影响原有的类名

```javascript
$(function () {
    // 添加类名
    $('标签名').addClass('类名');
    
    // 删除类名
    $('标签名').removeClass('类名');
    
    // 切换类：点击添加类名，再点击删除类名
    $('标签名').toggleClass('类名');
});
```

```javascript
$(function () {
    $('div').click(function () {
        // 添加类名
        $('div').addClass("current");
        
        // 删除类名
        $('div').removeClass("current");
        
        // 切换类名
        $('div').toggleClass('current');
    });
});
```



## jQuery 效果

### 元素的显示和隐藏

|   方法    | 说明 |
| :-------: | :--: |
|  .show()  | 显示 |
|  .hide()  | 隐藏 |
| .toggle() | 切换 |



### 下拉和上拉

|    方法     | 说明 |
| :---------: | :--: |
| slideDown() | 下拉 |
|  slideUp()  | 上拉 |
| slideToggle | 切换 |

==需要引用 stop() 暂停，停止前一个动画，开始新动画。（stop() 必须写在 动画前面）==

```javascript
$('.nav li').hover(function () {
    $(this).children('ul').stop().slideToggle();
});
```



### hover 事件

> hover 有两个参数，第一个是鼠标移入事件，第二个是鼠标移出事件

```javascript
$(function () {
    $('li').hover(function () {
        // 鼠标移入事件
        $(this).siblings().stop().fadeTo(400, 0.5);
    }, function () {
        // 鼠标移出事件
        $(this).siblings().stop().fadeTo(400, 1);
    });
});
```



### 淡入淡出

|     方法     |    说明    |
| :----------: | :--------: |
|   fadeIn()   |    淡入    |
|  fadeOut()   |    淡出    |
| fadeToggle() |  淡入淡出  |
|   fadeTo()   | 修改透明度 |

> 修改透明度，毫秒值和透明度必须写

```javascript
// fadeTo() 语法格式：
fadeTo(毫秒值, 透明度);

dadeTo(1000, 0.5);
```



### 自定义动画

```javascript
/ 语法格式：
$(function () {
    $('标签名').animate({
        键: 值,
    });
});
```



## jQuery 属性操作方法

|         方法         |            说明             |
| :------------------: | :-------------------------: |
|    prop('属性名')    |     获取元素固有属性值      |
| prop('属性名', '值') |     设置元素固有属性值      |
|    attr('属性名')    |    获取元素的自定义属性     |
| attr('属性名', '值') |    设置元素的自定义属性     |
|    data('属性名')    | 获取data-index H5自定义属性 |
| data('属性名', '值') |        数据缓存（）         |



## jQuery 操作元素的方法

|        方法         |           说明           |
| :-----------------: | :----------------------: |
|       html()        |      获取元素的内容      |
| html('标签名+内容') | 设置元素的内容，包含标签 |
|       text()        |    获取元素的文本内容    |
| text('修改的内容')  |    设置元素的文本内容    |



##  jQuery 事件注册

>jQuery 为我们提供了方便的事件注册机制，是开发人员抑郁操作优缺点如下：
>
>- 优点: 操作简单，且不用担心事件覆盖等问题。
>- 缺点: 普通的事件注册不能做事件委托，且无法实现事件解绑，需要借助其他方法。

![register](./assets/register.png)



```javascript
$(function() {
    // 1. 单个事件注册
    $("div").click(function() {
        $(this).css("background", "purple");
    });
    $("div").mouseenter(function() {
        $(this).css("background", "skyblue");
    });
})
```



## jQuery 事件处理

待补充

