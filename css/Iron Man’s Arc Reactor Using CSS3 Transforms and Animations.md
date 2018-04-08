# 使用CSS3变形和动画制作钢铁侠的方舟反应堆
[原文] [Iron Man’s Arc Reactor Using CSS3 Transforms and Animations | CSS-Tricks](https://css-tricks.com/iron-mans-arc-reactor-using-css3-transforms-and-animations/)

好了，钢铁侠迷们，启动你们的代码编辑器，我们将用CSS来制造钢铁侠衣服上的方舟反应堆。下面图片是我们应该制作的结果：

![Iron Man’s Arc Reactor.gif](../assets/Iron%20Man’s%20Arc%20Reactor.gif)

# 页面包装

我们将是我们的方舟反应堆处于全屏黑暗背景下。以下是我们制作全屏包装元素的代码：

``` css
body {
  margin: 0;
}
.fullpage-wrapper {
  height: 100vh;
  background: radial-gradient(#353c44, #222931); //注意此处是径向渐变背景
}
```

为什么我们要在body中声明margin为空？因为在默认情况下，用户代理样式表会为`<body>`设置一些margin。这样可以防止`<body>`中的元素触碰到屏幕的边缘。由于我们希望我们的包装器能覆盖整个屏幕，乃至所有边缘，所以我们通过设置为0来移除了`<body>`元素的margin。

我们为` # 使用CSS3变形和动画制作钢铁侠的方舟反应堆
[原文] [Iron Man’s Arc Reactor Using CSS3 Transforms and Animations | CSS-Tricks](https://css-tricks.com/iron-mans-arc-reactor-using-css3-transforms-and-animations/)

好了，钢铁侠迷们，启动你们的代码编辑器，我们将用CSS来制造钢铁侠衣服上的方舟反应堆。下面图片是我们应该制作的结果：

![Iron Man’s Arc Reactor.gif](../assets/Iron%20Man’s%20Arc%20Reactor.gif)

# 页面包装

我们将是我们的方舟反应堆处于全屏黑暗背景下。以下是我们制作全屏包装元素的代码：

``` css
body {
  margin: 0;
}
.fullpage-wrapper {
  height: 100vh;
  background: radial-gradient(#353c44, #222931); //注意此处是径向渐变背景
}
```

为什么我们要在body中声明margin为空？因为在默认情况下，用户代理样式表会为`<body>`设置一些margin。这样可以防止`<body>`中的元素触碰到屏幕的边缘。由于我们希望我们的包装器能覆盖整个屏幕，乃至所有边缘，所以我们通过设置为0来移除了`<body>`元素的margin。

我们给了`.fullpage-wrapper`设置了视图的整个高度。我们没有定义宽度是因为div默认取父级总宽度。我们可以用另一种方法设置元素的宽高为`100%`，但是随着更多的元素被添加到屏幕上，可能会带来一些缺点。使用视窗单位可以保证我们的包装器始终占据屏幕的全部垂直空间，不管它是什么或者其他元素被添加到布局当中。

我们使用的css的`radial-gradient()`函数为我们的包装器使用了径向渐变。函数包含的参数是颜色的开始和结束点。因为，背景将会是从中心的`#353c44`颜色到`#222931`颜色的变化。很细微的变化，但是感觉很舒服。

<!-- ![](../assets/WX20180404-170830@2x.png =100x20) -->
<img src="../assets/WX20180404-170830@2x.png" width="500">

# 将反应堆容器定于中心

在我们开始创建我们的反应堆之前，我们先为他创建一个容器，并将它置于中心：

```css
.reactor-container {
  width: 300px;
  height: 300px;
  margin: auto;
  border: 1px dashed #888;
}
```

这里给我们了一个300 x 300带有虚线边框的盒子。它的`margin: auto`保证了水平居中。

<img src="../assets/WX20180404-172158@2x.png" width="500">

但是为什么它不能垂直居中呢？

根据CSS2规范，如果我们设置margin左右为auto，那么整个可用空间将会平分给左右的margin。但是，这跟上下的margin不是同一种情况。对于上下的margin，CSS2规范有声明：

> *If margin-top, or margin-bottom are auto, their used value is 0.* <br /> 如果margin-top或者margin-bottom被设为auto，那么他们最终使用的值将是0

然而，我们有一个好消息。flexbox布局遵循了新的布局规则，在Flexbox 规范中有声明说：

> *Prior to alignment via justify-content and align-self, any positive free space is distributed to auto margins in that dimension.* <br /> 在通过`justify-content`和`align-self`对齐之前，任何确认可用的空间都将分配给自动边距

这就意味着如果元素被考虑作为flex元素显示，那么它的各个方向都设置的是`margin:auto`。我们将容器设置为flex容器，并且它的子元素也是flex：
```css
.fullpage-wrapper {
  width: 100%;
  height: 100vh;
  background: radial-gradient(#353c44, #222931);
  display: flex;
}
```
这是更好的方法。
<img src="../assets/WX20180404-172158@2x.png" width="500">
在HTML中还有很多其他的方法可以让元素居中。在CSS-Tricks这里有一篇[居中指南](https://css-tricks.com/centering-css-complete-guide/)可以学习更多的方法。

# 反应堆芯：CSS中的同心圆


#翻译