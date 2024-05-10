# 使用说明

## 水印位置 
我们使用 `WatermarkPosition` 这个类的对象来控制具体水印出现的位置。

```java 
   WatermarkPosition watermarkPosition = new WatermarkPosition(double position_x, double position_y, double rotation);
   WatermarkPosition watermarkPosition = new WatermarkPosition(double position_x, double position_y);
```

在函数构造器中，我们可以设定水印图片的横纵坐标，如果你想在构造器中初始化一个水印旋转角度也是可以的， 水印的坐标系以背景图片的左上角为原点，横轴向右，纵轴向下。  
如果需要将定位原点从左上角修改为其他位置，可以稍后给`WatermarkText`或`WatermarkImage`调用`setOrigin(new WatermarkPosition(0.5, 0.5))`方法，
这里x,y都是0到1的浮点数，默认都是0，表示左上角对齐；0.5,0.5则表示中心对齐。

`WatermarkPosition` 同时也支持动态调整水印的位置，这样你就不需要一次又一次地初始化新的位置对象了， androidwm 提供了一些方法：

```java
     watermarkPosition
              .setPositionX(x)
              .setPositionY(y)
              .setRotation(rotation);
```
在全覆盖水印模式(Tile mode)下，关于水印位置的参数将会失效。

|  ![](https://i.loli.net/2018/09/05/5b8f4a970a83e.png)   | ![](https://i.loli.net/2018/09/05/5b8f4a9706788.png) | 
| :-------------: | :-------------: | 
|   x = y = 0, rotation = 15 | x = y = 0.5, rotation = -15  | 

横纵坐标都是一个从 0 到 1 的浮点数，代表着和背景图片的相对比例。


## 字体水印的颜色

你可以在 `WatermarkText` 中设置字体水印的颜色或者是其背景颜色:

```java
    WatermarkText watermarkText = new WatermarkText(editText)
            .setPositionX(0.5)
            .setPositionY(0.5)
            .setTextSize(30)
            .setTextAlpha(200)
            .setTextColor(Color.GREEN)
            .setBackgroundColor(Color.WHITE); // 默认背景颜色是透明的
```

|  ![](https://i.loli.net/2018/09/05/5b8f4ce0cf6ce.png)   | ![](https://i.loli.net/2018/09/05/5b8f4ce11a28c.png) | 
| :-------------: | :-------------: | 
|   color = green, background color = white | color = green, background color = default  | 

## 字体颜色的阴影和字体
你可以从软件资源中加载一种字体，也可以通过方法 `setTextShadow` 设置字体的阴影。

```java
    WatermarkText watermarkText = new WatermarkText(editText)
            .setPositionX(0.5)
            .setPositionY(0.5)
            .setOrigin(new WatermarkPosition(0.5, 0.5))
            .setTextSize(40)
            .setTextAlpha(200)
            .setTextColor(Color.GREEN)
            .setTextFont(R.font.champagne)
            .setTextShadow(0.1f, 5, 5, Color.BLUE);
```

|  ![](https://i.loli.net/2018/09/05/5b8f5c48e2631.png)   | ![](https://i.loli.net/2018/09/05/5b8f5c48e081c.png) | 
| :-------------: | :-------------: | 
|   font = champagne | shadow = (0.1f, 5, 5, BLUE)  | 

阴影的四个参数分别为： `(blur radius, x offset, y offset, color)`.

## 字体大小和图片大小

水印字体和水印图片大小的单位是不同的：
- 字体大小和系统布局中字体大小是类似的，取决于屏幕的分辨率和背景图片的像素，您可能需要动态调整。
- 图片大小是一个从 0 到 1 的浮点数，是水印图片的宽度占背景图片宽度的比例。

|  ![](https://i.loli.net/2018/09/05/5b8f5eb1a7fb0.png)   | ![](https://i.loli.net/2018/09/05/5b8f5eb24d0fd.png) | 
| :-------------: | :-------------: | 
|   image size = 0.3 | text size = 40  | 


## 方法列表
对于 `WatermarkText` 和 `WatermarkImage` 的定制化，我们提供了一些常用的方法:


|   __方法名称__  | __备注__ | __默认值__ |
| ------------- | ------------- | ------------- |
| setPosition  | 水印的位置类 `WatermarkPosition` | _null_ |
| setPositionX  |  水印的横轴坐标，从背景图片左上角为(0,0)  | _0_  |
| setPositionY  |  水印的纵轴坐标，从背景图片左上角为(0,0)  | _0_ |
| setRotation  |  水印的旋转角度| _0_  |
| setOrigin  |  水印的对齐原点| _null_  |
| setOriginX  |  水印的横坐标对齐位置，0~1之间| _0_  |
| setOriginY  |  水印的纵坐标对齐位置，0~1之间| _0_  |
| setTextColor  (`WatermarkText`)  |  `WatermarkText` 的文字颜色 | _`Color.BLACK`_  |
| setTextStyle  (`WatermarkText`)  |  `WatermarkText` 的文字样式| _`Paint.Style.FILL`_  |
| setBackgroundColor  (`WatermarkText`) |  `WatermarkText` 的背景颜色 | _null_  |
| setTextAlpha  (`WatermarkText`) | `WatermarkText` 文字的透明度， 从 0 到 255 | _50_  |
| setImageAlpha  (`WatermarkImage`) | `WatermarkImage` 图片的透明度， 从 0 到 255 | _50_  |
| setTextSize (`WatermarkText`) | `WatermarkText` 字体的大小，单位与系统 layout 相同 | _20_   |
| setSize  (`WatermarkImage`)|  `WatermarkImage` 水印图片的大小，从 0 到 1 (背景图片大小的比例) | _0.2_   |
| setTextFont (`WatermarkText`) | `WatermarkText` 的字体| _default_  |
| setTextShadow  (`WatermarkText`)| `WatermarkText` 字体的阴影与圆角 | _(0, 0, 0)_  |
| setImageDrawable  (`WatermarkImage`)| `WatermarkImage`的图片资源 | _null_ |

`WatermarkImage` 的一些基本属性和`WatermarkText` 的相同。
