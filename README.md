
# Material Design for Android Developers

## 1 Android 设计简介
### 1.1 物理独立像素与密度独立像素

#### 1.1.1  屏幕分辨率，也就是屏幕上的像素数量，屏幕分辨率是在购买设备时经常考量个一个要素，但它在针对Android的设计方面并没有太多的用处，因为从像素角度出发考虑屏幕问题，忽略了物理尺寸的概念，这对于触摸设备而言是尤为重要的。Android 为每一个设备生成合适像素的资源而不缩放，这需要一个系统的方式来处理不同屏幕上的资源。

![density-independent pixels](https://youngtr.github.io/images/density-independent-pixels.png)

在Android中，规定以160dpi为基准，1dip=1px，如果密度是320dpi，则1dip=2px，以此类推。


### 1.2 密度桶

![density buckets](https://youngtr.github.io/images/density-buckets.png)

### 1.3 常见的设计模式

选择应用程序的结构和导航方案，取决于应用程序里的内容，比较好的做法是绘制实体关系图，这会显示应用程序中的对象以及它们之间的关系。

* Toolbar

![Toolbar](https://youngtr.github.io/images/tool-bar.png)

* Appbar

![App bar](https://youngtr.github.io/images/appbar.png)

* Tabs

![Tabs](https://youngtr.github.io/images/tabs.png)

* Navigation Drawer

![Navigation Drawer](https://youngtr.github.io/images/navigation-drawer.png)

* Scroll and pagind

![Scroll and pagind](https://youngtr.github.io/images/scroll-and-pagind.png)

* List to details

![image](https://youngtr.github.io/images/list-to-details.png)

* Mutipane

![image](https://youngtr.github.io/images/mutipane.png)


## 2 表面

Material Design 中的一种关键材料——纸张平面（paper surfaces）。Material Design 试图描述 UI的构成，使用纸张这个隐喻，以人们的现实生活经验为基础，使 UI 更加容易被人理解。（有形性）

### 2.1 表面简介

在 Material Design 中，想象UI是由一张张数字纸张构成的，我们称之为平面(surfaces)。这些平面具有表明实行为的实体属性。屏幕上的一切都在其中的一个平面上，包括所有的文字、图标、照片、按钮等任何 UI 元素。这些平面有一小部分的物理性，足够用来显示事物之间的差异性和相关性。它利用的是我们快速识别物体的本能，使用的是现实世界的文字、色彩和光线等等。

![surface](https://youngtr.github.io/images/surface-2d.png)


平面还存在于 3D 空间中，在不同的空间高度上有不同的宽度和平面高度。这些平面层层叠加，并在较低的平面上投下阴影。


![surface](https://youngtr.github.io/images/surface-3d.png)


一般来说，物体离我们越近就越容易在视觉上引起我们的注意，根据物理的尺寸以及它们覆盖和投射阴影的方式，我们能区分哪些物体离我们更近。我们可以在UI中使用深度队列，将注意力引导至重要的元素。

### 2.2 使用平面

一个平面就是一个容纳内容的容器，它能实现与其它元素的分组和分离,该如何使用平面呢？


例如，我们有针对应用栏的平面，还有针对每个条目的平面，但是这些造成了视觉上的不连贯，将每个条目放在不同的平面上，会减缓你向下浏览列表的速度。

![image](https://youngtr.github.io/images/surface-item.png)

一个更利索的方法就是在单一平面上运用微弱的分割线来分割内容。


![image](https://youngtr.github.io/images/surface-item2.png)

相反地，在这个例子中，将每个特别不同的条目放置在各自独立的平面上可使你进行逐一阅览。


![image](https://youngtr.github.io/images/surface-item3.png)


一般来讲，如果内容属于同类，浏览和对比就十分重要，所以应该将它们放在同一平面上，如果需要展现不同类型的条目，将它们放在各自的平面上是最为合适的。

但是要注意，屏幕上一次性出现过多的独立平面会分散注意力，从经验上讲，最好不要一次性在屏幕上出现**5个**以上的平面。


### 2.3 实现平面


Android 布局文中可以使用 **elevation** 属性来设置平面的高度值。高度时指平面与背面之间的距离，数值越大，阴影越大。

![image](https://youngtr.github.io/images/surface-elevation.png)


[不同模块的标准高度](https://material.io/guidelines/material-design/elevation-shadows.html)


### 2.4 FAB

#### 2.4.1 什么是FAB?

Material Design 的标志性设计模式之一就是悬浮操作按钮，简称 F-A-B或者FAB。这是一种色彩鲜明的圆形图标按钮，漂浮在应用的内容上方，促使进行重要操作和传递屏幕字符的一种方式。由于该按钮漂浮在其他内容的上方，所以它总是处于可用的状态，时刻告诉用户它的重要性。

![image](https://youngtr.github.io/images/fab.png)


FAB 具有标准的尺寸和高度，它们的直径为 40dp 或 56dp，通常静止高度为 6dp，当它被按下时，这一高度将达到 12dp。

![image](https://youngtr.github.io/images/fab-size.png)


注意应当避免在应用中过度使用FAB,在每个屏幕中仅使用一个 FAB,不是每个屏幕都需要一个 FAB。

#### 2.4.2 添加 FAB

* 1.build.gradle

```
dependencies {
	compile fileTree(dir: 'libs', include: ['*.jar'])
	compile 'com.android.support:appcompat-v7:22.2.0'
	compile 'com.android.support:design:22.2.0'
}
```

* 2.activity-main.xml

 
![image](https://youngtr.github.io/images/fab-xml.png)


* 3.style.xml

将 Material 的实例替换成 AppCompat


![image](https://youngtr.github.io/images/fab-style.png)




#### 2.4.3 向 FAB 添加水波/表面高度

在 Material Design 中，响应触摸的视觉反馈主要有两种形式，第一种是微弱的波纹效果，从指尖向外扩散，一直延伸到所在平面的边界；第二种，对于无边界的元素，波纹将延伸至足够远的位置，使你感受到元素的大小。



布局文件：


```
 	<ImageButton
        android:id="@+id/fab"
        android:layout_width="56dp"
        android:layout_height="56dp"
        android:layout_margin="10dp"
        android:background="@drawable/oval_ripple"
        android:elevation="6dp"
        android:src="@drawable/fab_plus"
        android:stateListAnimator="@animator/fab_raise" />

```

statelistAnimator 属性表示点击的过渡动画：

```
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_enabled="true" android:state_pressed="true">
        <objectAnimator
            android:duration="1000"
            android:propertyName="translationZ"
            android:valueTo="8dp"
            android:valueType="floatType"
            />
    </item>
    <item>
        <objectAnimator
            android:duration="1000"
            android:propertyName="translationZ"
            android:valueTo="0dp"
            android:valueType="floatType"
            />
    </item>
</selector>
```

### 2.5 纸张转换

材料平面有一些可以赋予它们生命的独特属性，使你的应用程序能够与用户建立联系。材料平面可以被人们创建和摧毁，它可以改变形状、分裂或重聚。

![wave](https://youngtr.github.io/images/wave-2d.gif)

同样，平面上的墨水组件可以抬升，并形成自己的平面。例如，一个列表项抬升并扩展后成了详情页。

![wave](https://youngtr.github.io/images/wave-3d.gif)


这些材料属性能够帮助你创建沉浸式的应用程序，用来响应交互操作，而非跳转到新的状态。使用 

ViewAnimationUtils.createCircularReveal(View view,int centerX,  int centerY, float startRadius, float endRadius) 创建转换动画，例如

```
	boolean isVeggie = ((ColorDrawable)view.getBackground()) != null && ((ColorDrawable)view.getBackground()).getColor() == green;

            int finalRadius = (int)Math.hypot(view.getWidth()/2, view.getHeight()/2);

            if (isVeggie) {
                text1.setText(baconTitle);
                text2.setText(baconText);
                view.setBackgroundColor(white);
            } else {
                Animator anim = ViewAnimationUtils.createCircularReveal(view, (int) view.getWidth()/2, (int) view.getHeight()/2, 0, finalRadius);
                text1.setText(veggieTitle);
                text2.setText(veggieText);
                view.setBackgroundColor(green);
                anim.start();
            }
```


![transform](https://youngtr.github.io/images/transform.gif)



### 2.6 响应滚动事件


***这个后面详细描述***

![滚动事件](https://youngtr.github.io/images/action.gif)



## 3 图形设计


### 3.1 网格和关键线

Material Design 使用 8dp 网格来对其组件，文本在 4dp 的基线网格中进行对齐。

![网格](https://youngtr.github.io/images/8dp-grid.png)


图像、图标大小、间距、外边框和内边框的都是 8dp 的倍数，对于文本而言，文本高度时 4 的倍数，所有数据为 20。这些 8dp 和 4dp 的网格允许我们轻轻松松地运用分组定律，使我们的 UI 有序、平衡并且和操作系统的其余部分协调一致。

![网格](https://youngtr.github.io/images/8dp-grid2.png)

keylines

![网格](https://youngtr.github.io/images/keylines.png)

### 3.2 颜色和材料设计调色板

我们能从物品的颜色和外观中推断出信息，颜色能告诉我们某个特定的食物是熟了还是变质了，或者我们的电池电量是不是快要用完了。颜色可以用来引导注意力或表明层次和结构。

Material Design 调色板包括主色和辅色，如果已经创建了品牌颜色，请使用它们！


### 3.3 使用颜色

选择一款具有代表性的主色用来展现应用的品牌定位或品牌个性，可以将这种颜色用在大的区块内，比如应用栏，使你的应用被人一眼认出来。
选在一款强调颜色，这种颜色更鲜亮，饱和度更高，用来将用户的注意力引导到特定的元素上，比如悬浮操作按钮。


![使用颜色](https://youngtr.github.io/images/user-color.png)


### 3.4 调色板

要创建整个UI光是两种颜色还不够，我们可以将这些颜色按照亮度进行分解，从而构建出自己的调色板。


![image](https://youngtr.github.io/images/color-paletttte.png)

这是 Material Design 中的浅蓝色色样，Material Design 向这一色度范围制定了数值，色度低的数值小，色度高的数值大。

对主色的亮标尺进行定标，也就是这里的色度 500，用前缀 A 代表强调色，表示更为饱和的颜色。

建议始终使用主色的三种色相和一种强调色，这样调色板才能既简单又丰富。

![user-color](https://youngtr.github.io/images/user-color-paletttte.png)

Android Studio 中定义

![user-color](https://youngtr.github.io/images/user-color-xml.png)

### 3.5 字体

![font metrics](https://youngtr.github.io/images/font.png)

[单击此处可详细了解字体解剖。](http://typedia.com/learn/only/anatomy-of-a-typeface/)


### 3.6 使用图像

图像能传递信息，个性化用户体验，使用的图像将强烈影响并提升你的品牌效应。

![user image](https://youngtr.github.io/images/user-image.png)

注意图片应该与描述信息相匹配，例如展示人物信息时，一个标签或者一个通用的图形更能传递信息，在呈现照片时，请确保你使用的是高质量的图像。

**插图**

如果我们要传达照片无法体现抽象概念或比喻，插图会是个很好的方法。在创建插图时，请务必做到清晰明确，避免过度修饰，只要有你想表达的聚焦点和信息即可。

![user illustration](https://youngtr.github.io/images/user-illustration.png)

尽管插图的具体样式取决于自己，但最好能在一系列插图之间保持一致性，使他们能够相互关联起来，例如使用统一视角、调色板或者纹理。

**图标**

图标应方便识别并在你的 UI 中起到解释的作用，最好在常见任务中使用平台图标,如搜索或者分享，因为用户对此非常熟悉。

[关于创建图标的更多信息](https://www.google.com/design/spec/style/icons.html)

[materialdesignicons.com](https://materialdesignicons.com/)


### 3.7 背景保护

如果背景与页面元素，如标题、图标颜色差不多时，页面元素可能就看不清楚了。对于覆盖的图标或者文字，可以巧妙地利用图像上的阴影将它们从背景中区分出来，对于文字我们可以使用**渐变色**"纱幕"来解决这个问题。图像和文本之间一个半透明的层，可以提供对比度和清晰度。

![gradient](https://youngtr.github.io/images/user-gradient.png)
