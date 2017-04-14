---
title: 前端踩坑
date: 2017-04-07 14:54:07
tags:
---

撸码时遇到得一些问题，记录下来，以免掉坑

#### 1、inline-block元素自带的4px边距
设置父元素
```
font-size:0;letter-spacing:-4px;
```
然后设置子元素正常的font-size和letter-spacing;

#### 2、移动端JS给页面设置scrollTop出现闪屏问题，移动端IOS safari浏览器，某些情况下页面无法滑动
给body加上属性：
```
-webkit-overflow-scrolling: touch;
```

#### 3、移动端ios浏览器/ios端微信浏览器，使用$(document).on()绑定事件失效
给要绑定的元素加个一个空的onclick=""，或者给该元素加上
```
cursor: pointer;
```

#### 4、某些手机自带浏览器不支持css属性缩写
css属性尽量分开写，比如
```
background: url(xxx.jpg) no-repeat 0 0/100% 100%;
```
改为
```
background: url(xxx.jpg) no-repeat;
background-position: 0 0;
background-size: 100% 100%;
```

#### 5、js中使用加减运算浮点数的时候，可能出现的精度丢失问题
例如0.1+0.2=0.30000000000000004，得到的结果不等于0.3，可以截取小数点位置后，再做比较

#### 6、$(obj)[0]，不能使用jq的方法
这样取到的元素不是jq对象了，需要重新使用$($(obj)[0])处理后，才能使用jq的方法

#### 7、vuejs的filter属性，定义了Vue.filter()之后，使用v-text="str | filter"过滤会报错：filter is not defined
使用\{ \{ str | filter \} \}可正常使用，原因不明

#### 8、移动端IOS safari浏览器，给div绑定点击事件，出现页面未响应
把div改为a标签，并加上href属性

#### 9、overflow：hidden可能会影响移动端界面滑动不流畅
尽量少用，或可以使用iScroll插件;

#### 10、某些安卓手机自带浏览器 fixed 底部遮住页面
在被遮住的层的最大父级容器 加上
```
padding-bottom: 1px
```

#### 11、在line-heigth：1 手机页看  文字会被截取一端
可以在全局加上
```
padding:1px；
```

#### 12、安卓和ios文字上下居中不一样，安卓会向上2px
可判断出安卓系统后，再需要居中的文本加上
```
padding-top：2px；
```

#### 13、默认图用css完成
可用两层相对定位控制层级显示，底部写默认图，上面写背景图，当背景图没有的时候，看到的就是默认图。

#### 14、浏览器默认会根据当前屏幕方向和内容自动调整内容的字体大小，导致横屏后字体变大
css设置如下：
```
-webkit-text-size-adjust : none ;
-moz-text-size-adjust : none ;
-ms-text-size-adjust : none ;
text-size-adjust : none;
```

#### 15、移动端 border-radius:100%,不圆。
保证圆的大小为双整数

#### 16、移动页面在 UC 浏览器，获取跳转地址被拦截
UC 是把所有 body 为空的 POST 请求全部改为 GET，所以在所有空 POST 请求中都加一个其实无用的参数 { f: 1 }，就可以防止 UC 把这个 POST 请求。

#### 17、移动页面在 UC 浏览器，会莫名的移除底部元素
```
<div class="footer">
```
元素在上线之后，会很随机的出现和消失，没有规律。可以改class名称, footer 改为 xxx-footer 后发现问题解决了。

#### 18、vue和jq以及jq插件混用时，出现jq事件绑定失败和jq插件调用无效的情况
先定义vue实例，然后把jq事件和jq插件的调用写到vue延迟回调方法里，
```
Vue.nextTick(function(){});
```