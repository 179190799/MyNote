# Android 的 Drawable
## Drawable 简介
1. Drawable 是一个抽象类，它是所有 Drawable 对象的基类，每个具体的 Drawable 都是它的子类。
2. Drawable 的内部宽/高这个参数比较重要，通过 getIntrinsicWidth 和 getIntrinsicHeight 这两个方法可以获取到它们。但是并不是所以的 Drawable 都有内部宽/高。Drawable 的内部宽/高不等同于它的大小。Drawable 是没有大小的概念的。

## Drawable 的分类
1. BitmapDrawable
    表示的是一张图片。
    各个属性的含义：

    - android:src
        图片的资源 id。
    - android:antialias
        是否开启抗锯齿功能。
    - android:dither
        是否开启抖动效果。
    - android:filter
        是否开启过滤效果。
    - android:gravity
        gravity属性的可选项：
        ![gravity属性的可选项](http://o8fk8z4sl.bkt.clouddn.com/gravity%E5%B1%9E%E6%80%A7%E7%9A%84%E5%8F%AF%E9%80%89%E9%A1%B9.png)
    - android:mipMap
        纹理映射。
    - android:tileMode
        平铺模式。

        - disable
            表示关闭平铺模式。
        - repeat
            表示的是简单的水平和竖直方向上的平铺效果。
        - mirror
            表示一种在水平和竖直方向上的镜面投影效果。
        - clamp
            表示的效果是图片四周的像素会扩展到周围区域。

2. ShapeDrawable
    通过颜色来构造的图形。

    - android:shape
        表示图形的形状，有四个选项：rectangle(矩形)、oval(椭圆)、line(横线)和 ring(圆环)。
        
        ring的属性值：
        ![ring的属性值](http://o8fk8z4sl.bkt.clouddn.com/ring%E7%9A%84%E5%B1%9E%E6%80%A7%E5%80%BC.png)
    - <corners\>
        表示 shape 的四个角度，只适用于矩形 shape，有如下五个属性
        - andrdoid:radius --- 为四个角同时设定相同的角度，优先级较低，会被其他四个属性覆盖。
        - andrdoid:topLeftRadius --- 设定最上角的角度；
        - andrdoid:topRightRadius --- 设定右上角的角度；
        - andrdoid:bottomLeftRadius --- 设定最下角的角度；
        - andrdoid:bottomRightRadius --- 设定右下角的角度。
    - <gradient\>
        与<solid\>标签是互斥的，其中 solid 表示纯色填充，gradient 表示渐变效果。gradient 有如下几个属性：
        - android:angle --- 渐变的角度，默认为0，其值必须是45的倍数，0表示从左到右，90表示从上到下。
        - android:centerX --- 渐变的中心点的横坐标；
        - android:centerY --- 渐变的中心点的纵坐标；
        - android:startColor --- 渐变的起始色；
        - android:centerColor --- 渐变的中间色；
        - android:endColor --- 渐变的结束色；
        - android:gradientRadius --- 渐变半径，仅当 android:type = "radial"时有效；
        - android:useLevel --- 一般为 false，当 Drawable 作为 StateListDrawable 使用时为 true。
    - <solid\>
        这个标签表示纯色填充，通过 android:color 即可指定 shape 中填充的颜色。
    - <stroke\>
        Shape 的描边，有如下几个属性：
        - android:width --- 描边的宽度，越大则 shape 的边缘就会看起来越粗；
        - android:color --- 描边的颜色；
        - android:dashWidth --- 组成虚线的线段的宽度；
        - android:dashGap: --- 组成虚线的线段之间的间隔，间隔越大则虚线看起来空隙就越大。
        **注意：**如果 android:dashWidth 和 android:dashGap 有任何一个为0，那么虚线的效果将不能生效。
    - <padding\>
        表示空白，是包含它的 View 的空白，有四个属性：
        - android:left;
        - android:top;
        - android:right;
        - android:bottom。
    - <size\> 
        shape 的固有大小，有两个属性：
        - android:width
        - android:height
        分别表示 shape 的宽/高。

3. LayerDrawable
    LayerDrawable 对应于 XML 标签是<layer-list\>，表示一种层次化的 Drawable 集合，通过将不同的 Drawable 放置在不同的层上面从而达到一种叠加后的效果。
    默认情况下，layer-list 中的所有的 Drawable 都会被缩放至 View 的大小，对于 bitmap 来说，需要使用 android:gravity 属性才能控制图片的显示效果。