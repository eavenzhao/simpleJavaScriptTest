# simpleJavaScriptTest
用JS封装一些简单插件或者实现一些酷炫的动画效果，仅作为个人练习测试使用。

## 写一个轮播图效果
`index.html`
* 思路：
容器宽度为所有图片宽度的总和，图片在容器中向左浮动，水平排列。
通过不断地改变容器的left值实现轮播效果。

* 难点：
1.无限循环的实现。（借助辅助图，当显示在辅助图上时，重新设置容器的left值，使之显示同样的图片。）
2.动画的实现。（不能采用css过渡动画，采用js递归不断改变容器left值，实现动画效果。）

* 缺点：
1.借助辅助图不利于动态渲染。
2.程序没有扩展性，多添加图片程序就挂掉了。
3.......



`index2.html`

* 思路：
将所有的图片重叠定位在同一位置，分别切换各个图片的透明度实现轮播效果

* 优点：
1.简单、无需考虑无限轮播。
2.过渡动画可以在css中直接设置。
3.多添加几张图片也可以正常运行。

`index3.html`
我们封装了一个统一的轮播图插件插件，使用方式：

```js
new Carousel({	 
	oWrapper: '', // 父容器
	timeOut: 2000, // 延时切换时间
	figureW: 600, // 轮播图宽度
	figureH: 400, // 轮播图高度
	figures: [ // 轮播图片集合
	 '../img/xx.jpg',
	 '../img/xx.jpg',
	// ....
	]		
});
```

## canvas星星闪动效果

通过`canvas`画布以及`requestAnimationFrame`方法不断刷新画布实现各种动画效果。

比较重要的一些小知识点：
`save()`和`restore()`这两个方法经常一起使用，它可以使得一些操作仅作用于这两个方法之间，而不会影响其他内容。

```js
// 改变透明度
ctx.globalAlpha = 0.7;

// 绘制图片
// 参数：从画布的(0,0)位置开始
ctx.drawImage(xxImage,0,0,w,h);

// 绘制带填充的矩形
ctx.fillStyle = '#393550';
ctx.fillRect(0,0,w,h);

// 实现帧动画
.drawImage(xxImage,sx,sy,swidth,sheight,x,y,width,height);
//参数：(sx,sy)图片起点，(swidth,sheight)图片上的宽高, (x,y)是canvas上的起点，(width,height)是绘制在canvas上的宽高。

```

大体思路：

```js
document.body.onload = function(){

	init(); // 初始化
	drawLoop(); // 绘制循环
}

function drawLoop(){
	
	// 绘制各种东西
	drawBackground();
	drawGirlImage();
	drawStarImage();
	update();  // 更新一些参数
	requestAnimationFrame(drawLoop); // 不断地去重绘
}
```











