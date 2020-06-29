# colors

> Stability: 2 - Stable

How can you represent a color in OpenAuto.js?

You use "#AARRGGBB" or "#RRGGBB".

AA means Alpha tunnel, RR means red tunnel，GG means green tunnel, BB means blue tunnel.

> You can also use 32bit int `0xAARRGGBB` to represent a color.

## colors.parseColor(colorStr)
* `colorStr` {string} color string, like "#112233"
* return {number}

Return the corresponding number color.

## colors.toString(color)
* `color` {number} int color number
* return {string}

Return the corresponding color string. ("#AARRGGBB")

## colors.red(color)
* `color` {number} | {string}
* return {number}

Return the red tunnel value, it's in range of [0, 255].

## colors.green(color)
* `color` {number} | {string}
* return {number}

Return the green tunnel value, it's in range of [0, 255].

## colors.blue(color)
* `color` {number} | {string}
* return {number}

Return the blue tunnel value, it's in range of [0, 255].

## colors.alpha(color)
* `color` {number} | {string}
* return {number}

Return the Alpha tunnel value, it's in range of [0, 255].

## colors.argb(alpha, red, green, blue)
* `alpha` {number}
* `red` {number}
* `green` {number}
* `blue` {number}
* return {number}

Return the number representation of this color.

## colors.rgb(red, green, blue)
* red {number}
* green {number}
* blue {number}
* return {number}

Return the number representation of this color.

The Alpha tunnel would be 255 (untransparent).

## colors.isSimilar(color2, color2[, threshold, algorithm])
* `color1` {number} | {string}
* `color1` {number} | {string}
* `threshold` {number} The default value is 4. The range is 0~255. The smaller, The more similar. If this value == 0, return true only if the two-color totally the same.
* `algorithm` {string} The default one is "diff", options are:
    * "diff": ~~差值匹配.与给定颜色的R、G、B差的绝对值之和小于threshold时匹配.~~
    * "rgb": ~~rgb欧拉距离相似度.与给定颜色color的rgb欧拉距离小于等于threshold时匹配.~~
    * "rgb+": ~~加权rgb欧拉距离匹配([LAB Delta E](https://en.wikipedia.org/wiki/Color_difference)).~~
    * "hs": ~~hs欧拉距离匹配.hs为HSV空间的色调值.~~
* return {Boolean}

Check if two colors are similar.

## colors.equals(color1, color2)
* `color1` {number} | {string}
* `color1` {number} | {string}
* return {Boolean}

Check if two colors are identical.

```js
log(colors.equals("#112233", "#112234"));
log(colors.equals(0xFF112233, 0xFF223344));
```

# colors.BLACK

black, #FF000000

# colors.DKGRAY  

dark gray，#FF444444

# colors.GRAY  

gray，#FF888888

# colors.LTGRAY  

light gray，#FFCCCCCC

# colors.WHITE  

white，#FFFFFFFF

# colors.RED  

red，#FFFF0000

# colors.GREEN  

green，#FF00FF00

# colors.BLUE  

blue，#FF0000FF

# colors.YELLOW  

yellow，#FFFFFF00

# colors.CYAN  

cyan，#FF00FFFF

# colors.MAGENTA  

magenta，#FFFF00FF

# colors.TRANSPARENT  

transparent，#00000000

# Images

> Stability: 2 - Stable

The images module provides some common picture processing functions in mobile devices, including screenshots, pictures reading, picture cropping, rotation, binarization, color and image search, etc.

Warning: Too many usages of images may cause memory leaking.

You can recycle it to overcome this problem:
```js
// read an image
var img = images.read("./1.png");
//image processing
... 
// recycle that image
img.recycle();
```

> You don't have to recycle images that was captured by `caputerScreen()`.

## Image processing

## images.read(path)
* `path` {string} path of that image

Return an Image object.

If that file doesn't exist or reading error, we return null.

## images.load(url)
* `url` {string} image url

Return an Image object from an image link.

If that file doesn't exist or reading error, we return null.

## images.copy(img)
* `img` {Image}
* return {Image}

Copy an image, return a fresh new one. So you can do some process that won't affect the old image.

## images.save(image, path[, format = "png", quality = 100])
* `image` {Image}
* `path` {string} where to save
* `format` {string} options are:
    * `png`
    * `jpeg`/`jpg`
    * `webp`
* `quality` {number} picture quality, it's a number between [0, 100].

Save an image to local storage.

```js
//save an image with half quality
var img = images.read("/sdcard/1.png");
images.save(img, "/sdcard/1.jpg", "jpg", 50);
app.viewFile("/sdcard/1.jpg");
```

## images.fromBase64(base64)
* `base64` {string} base64 representation of an image
* return {Image}

Decode base64 data and return an image object.

If error we return null.

## images.toBase64(img[, format = "png", quality = 100])
* `image` {image}
* `format` {string} options are:
    * `png`
    * `jpeg`/`jpg`
    * `webp`
* `quality` {number} picture quality, it's a number between [0, 100].
* return {string}

Encode an image using base64.

## images.fromBytes(bytes)
* `bytes` {byte[]} bytes array

Decode an bytes array, and return the result image object.

If error, we return null.

## images.toBytes(img[, format = "png", quality = 100])
* `image` {image}
* `format` {string} options are:
    * `png`
    * `jpeg`/`jpg`
    * `webp`
* `quality` {number} picture quality, it's a number between [0, 100].
* return {byte[]}

Encode image object to bytes array.

## images.clip(img, x, y, w, h)
* `img` {Image}
* `x` {number} Up-left corner x
* `y` {number} Up-left corner y
* `w` {number} Box width
* `h` {number} Box height
* return {Image}

Cut the area of size w * h from the up-left corner position (x, y) of the img, and return the new image of the cut area.

```js
var src = images.read("/sdcard/1.png");
var clipped = images.clip(src, 100, 100, 400, 400);
images.save(clip, "/sdcard/clipped.png");
```

## images.resize(img, size[, interpolation])
* `img` {Image}
* `size` {Array} [width, height] or [length]
* `interpolation` {string} Defaults to "LINEAR"，options are:
    * `LINEAR`
    * `NEAREST`
    * `AREA`
    * `CUBIC`
    * `LANCZOS4`
    See more at [InterpolationFlags](https://docs.opencv.org/3.4.4/da/d54/group__imgproc__transform.html#ga5bb5a1fea74ea38e1a5445ca803ff121)

* return {Image}

Resize an image, and return the resized image.

For example, resize an image to 200*300:
```js
images.resize(img, [200, 300])
```

See more at [Imgproc.resize](https://docs.opencv.org/3.4.4/da/d54/group__imgproc__transform.html#ga47a974309e9102f5f08231edc7e7529d).

## images.scale(img, fx, fy[, interpolation])
* `img` {Image} 
* `fx` {number} width scale
* `fy` {number} height scale
* `interpolation` {string} Defaults to "LINEAR"，options are:
    * `LINEAR`
    * `NEAREST`
    * `AREA`
    * `CUBIC`
    * `LANCZOS4`
    See more at [InterpolationFlags](https://docs.opencv.org/3.4.4/da/d54/group__imgproc__transform.html#ga5bb5a1fea74ea38e1a5445ca803ff121)

* return {Image}

Resize an image by scale number, and return the new image.

For example, scale an image to half:
```js
images.scale(img, 0.5, 0.5)
```

See more at [Imgproc.resize](https://docs.opencv.org/3.4.4/da/d54/group__imgproc__transform.html#ga47a974309e9102f5f08231edc7e7529d).

## images.rotate(img, degress[, x, y])
* `img` {Image}
* `degress` {number}
* `x` {number} center x，defaults to the center point of that image
* `y` {number} center y，defaults to the center point of that image
* return {Image}

Rotate the image counterclockwise by certain degrees, then return the rotated image object.

For example, to rotate an image 90 degrees counterclockwise, you do `images.rotate(img, 90)`.

## images.concat(img1, image2[, direction])
* `img1` {Image}
* `img2` {Image}
* direction {string} concatenate direction，defaults to "RIGHT"，options are:
    * `LEFT` img2 at the left of img1
    * `RIGHT` img2 at the right of img1
    * `TOP` img2 at the top of img1
    * `BOTTOM` img2 at the bottom of img1
* return {Image}

Concatenate two images. Return the new image object.

## images.grayscale(img)
* `img` {Image}
* return {Image}

Grayscale the picture, and return the grayscaled picture.

## image.threshold(img, threshold, maxVal[, type])
* `img` {Image}
* `threshold` {number}
* `maxVal` {number} max value
* `type` {string} defaults to "BINARY"，see more at [ThresholdTypes](https://docs.opencv.org/3.4.4/d7/d1b/group__imgproc__misc.html#gaa9e58d2860d4afa658ef70a9b1115576), options are:
    * `BINARY` 
    * `BINARY_INV` 
    * `TRUNC`
    * `TOZERO`
    * `TOZERO_INV`
    * `OTSU`
    * `TRIANGLE` 
    
* return {Image}

Threshold the picture and return the processed image.

For example:
```
images.threshold(img, 100, 255, "BINARY")
```

It turns any pixel who greater than 100 to 255, less than 100 to 0. So in the end, this picture will only contains two values, 0 and 255, black and white.

See more at [threshold](https://docs.opencv.org/3.4.4/d7/d1b/group__imgproc__misc.html#gae8a4a146d1ca78c626a53577199e9c57).

## images.adaptiveThreshold(img, maxValue, adaptiveMethod, thresholdType, blockSize, C)
* `img` {Image}
* `maxValue` {number} max value
* `adaptiveMethod` {string} options are:
    * `MEAN_C` ~~计算出领域的平均值再减去参数C的值~~
    * `GAUSSIAN_C` ~~计算出领域的高斯均值再减去参数C的值~~
* `thresholdType` {string} options are:
    * `BINARY`
    * `BINARY_INV` 
* `blockSize` {number}
* `C` {number} ~~偏移值调整量~~
* return {Image}

Do an automated threshold, and return the processed image.

See more at [adaptiveThreshold](https://docs.opencv.org/3.4.4/d7/d1b/group__imgproc__misc.html#ga72b913f352e4a1b1b397736707afcde3).

## images.cvtColor(img, code[, dstCn])
* `img` {Image}
* `code` {string} color space type，options are [ColorConversionCodes](https://docs.opencv.org/3.4.4/d8/d01/group__imgproc__color__conversions.html#ga4e0972be5de079fed4e3a10e24ef5ef0):
    * `BGR2GRAY`
    * `BGR2HSV ` 
    * `...`
* `dstCn` {number} Number of color channels of the target image. It can be ignored.
* return {Image}

对图像进行颜色空间转换，并返回转换后的图像.
Image color space conversion. Similar with opencv' version of cvtColor.

See more at [cvtColor](https://docs.opencv.org/3.4.4/d8/d01/group__imgproc__color__conversions.html#ga397ae87e1288a81d2363b61574eb8cab).

## images.inRange(img, lowerBound, upperBound)
* `img` {Image}
* `lowerBound` {string} | {number}
* `upperBound` {string} | {number}
* return {Image}

Binarize the picture, the colors outside the lowerBound~upperBound range will become 0, and the colors within that range will become 255.

> An example, `images.inRange(img, "#000000", "#222222")`.

## images.interval(img, color, interval)
* `img` {Image}
* `color` {string} | {number}
* `interval` {number}
* return {Image}

Binarize the picture, the colors outside the range of (color - interval, color + interval) becomes 0, and the colors within that range becomes 255. (The addition and subtraction of color here are for each channel)

> For example, `images.interval(img, "#888888", 16)`. Every tunnel's value is 0x88，after calculation, it becomes [0x78, 0x98]. What this function does is to let color within [#787878, #989898] to #FFFFFF，outside this range to #000000.

## images.blur(img, size[, anchor, type])
* `img` {Image} 
* `size` {Array} the kernel size，like [3, 3]
* `anchor` {Array} defaults to the center of that image
* `type` {string} defaults to "DEFAULT"，options are:
    * `DEFAULT` same as BORDER_REFLECT_101
    * `CONSTANT` iiiiii|abcdefgh|iiiiiii with some specified i
    * `REPLICATE` aaaaaa|abcdefgh|hhhhhhh
    * `REFLECT` fedcba|abcdefgh|hgfedcb
    * `WRAP` cdefgh|abcdefgh|abcdefg
    * `REFLECT_101` gfedcb|abcdefgh|gfedcba
    * `TRANSPARENT` uvwxyz|abcdefgh|ijklmno
    * `REFLECT101` same as BORDER_REFLECT_101
    * `ISOLATED` do not look outside of ROI
* return {Image}

Blur an image, return the processed image.

See more at [blur](https://docs.opencv.org/3.4.4/d4/d86/group__imgproc__filter.html#ga8c45db9afe636703801b0b2e440fce37).

## images.medianBlur(img, size)
* `img` {Image}
* `size` {Array} the kernel size, like [3, 3]
* return {Image}

MedianBlur an image, return the processed image.

See more at [blur](https://docs.opencv.org/3.4.4/d4/d86/group__imgproc__filter.html#ga564869aa33e58769b4469101aac458f9).

## images.gaussianBlur(img, size[, sigmaX, sigmaY, type])
* `img` {Image}
* `size` {Array} the kernel size, like [3, 3]
* `sigmaX` {number} can be ignored
* `sigmaY` {number} can be ignored
* `type` {string} defaults to "DEFAULT"，see `images.blur`
* return {Image}

GaussianBlur an image, return the processed image.

See more at [GaussianBlur](https://docs.opencv.org/3.4.4/d4/d86/group__imgproc__filter.html#gaabe8c836e97159a9193fb0b11ac52cf1).

## images.matToImage(mat)
* `mat` {Mat} Mat object in opencv
* return {Image}

Convert Mat object to Image object.

## 找图找色

## images.requestScreenCapture([landscape])
* `landscape` {boolean} 布尔值， 表示将要执行的截屏是否为横屏.如果landscape为false, 则表示竖屏截图; true为横屏截图.

向系统申请屏幕截图权限，返回是否请求成功.

第一次使用该函数会弹出截图权限请求，建议选择“总是允许”.

这个函数只是申请截图权限，并不会真正执行截图，真正的截图函数是`captureScreen()`.

该函数在截图脚本中只需执行一次，而无需每次调用`captureScreen()`都调用一次.

**如果不指定landscape值，则截图方向由当前设备屏幕方向决定**，因此务必注意执行该函数时的屏幕方向.

建议在本软件界面运行该函数，在其他软件界面运行时容易出现一闪而过的黑屏现象.  

示例:
```
//请求截图
if(!requestScreenCapture()){
    toast("请求截图失败");
    exit();
}
//连续截图10张图片(间隔1秒)并保存到存储卡目录
for(var i = 0; i < 10; i++){
    captureScreen("/sdcard/screencapture" + i + ".png");
    sleep(1000);
}

```

该函数也可以作为全局函数使用.

## images.captureScreen()

截取当前屏幕并返回一个Image对象.

没有截图权限时执行该函数会抛出SecurityException.

该函数不会返回null，两次调用可能返回相同的Image对象.这是因为设备截图的更新需要一定的时间，短时间内（一般来说是16ms）连续调用则会返回同一张截图.

截图需要转换为Bitmap格式，从而该函数执行需要一定的时间(0~20ms).

另外在requestScreenCapture()执行成功后需要一定时间后才有截图可用，因此如果立即调用captureScreen()，会等待一定时间后(一般为几百ms)才返回截图.

例子:

```
//请求横屏截图
requestScreenCapture(true);
//截图
var img = captureScreen();
//获取在点(100, 100)的颜色值
var color = images.pixel(img, 100, 100);
//显示该颜色值
toast(colors.toString(color));
```

该函数也可以作为全局函数使用.

## images.captureScreen(path)
* `path` {string} 截图保存路径

截取当前屏幕并以PNG格式保存到path中.如果文件不存在会被创建；文件存在会被覆盖.

该函数不会返回任何值.该函数也可以作为全局函数使用.

## images.pixel(image, x, y)
* `image` {Image} 图片
* `x` {number} 要获取的像素的横坐标.
* `y` {number} 要获取的像素的纵坐标.

返回图片image在点(x, y)处的像素的ARGB值.  

该值的格式为0xAARRGGBB，是一个"32位整数"(虽然JavaScript中并不区分整数类型和其他数值类型).

坐标系以图片左上角为原点.以图片左侧边为y轴，上侧边为x轴.

## images.findColor(image, color, options)
* `image` {Image} 图片
* `color` {number} | {string} 要寻找的颜色的RGB值.如果是一个整数，则以0xRRGGBB的形式代表RGB值（A通道会被忽略）；如果是字符串，则以"#RRGGBB"代表其RGB值.
* `options` {Object} 选项

在图片中寻找颜色color.找到时返回找到的点Point，找不到时返回null.

选项包括:
* `region` {Array} 找色区域.是一个两个或四个元素的数组.(region[0], region[1])表示找色区域的左上角；region[2]*region[3]表示找色区域的宽高.如果只有region只有两个元素，则找色区域为(region[0], region[1])到屏幕右下角.如果不指定region选项，则找色区域为整张图片.
* `threshold` {number} 找色时颜色相似度的临界值，范围为0~255（越小越相似，0为颜色相等，255为任何颜色都能匹配）.默认为4.threshold和浮点数相似度(0.0~1.0)的换算为 similarity = (255 - threshold) / 255.

该函数也可以作为全局函数使用.

一个循环找色的例子如下:
```
requestScreenCapture();

//循环找色，找到红色(#ff0000)时停止并报告坐标
while(true){
    var img = captureScreen();
    var point = findColor(img, "#ff0000");
    if(point){
        toast("找到红色，坐标为(" + point.x + ", " + point.y + ")");
    }
}

```

一个区域找色的例子如下:
```
//读取本地图片/sdcard/1.png
var img = images.read("/sdcard/1.png");
//判断图片是否加载成功
if(!img){
    toast("没有该图片");
    exit();
}
//在该图片中找色，指定找色区域为在位置(400, 500)的宽为300长为200的区域，指定找色临界值为4
var point = findColor(img, "#00ff00", {
     region: [400, 500, 300, 200],
     threshold: 4
 });
if(point){
    toast("找到啦:" + point);
}else{
    toast("没找到");
}
```

## images.findColorInRegion(img, color, x, y[, width, height, threshold])

区域找色的简便方法.

相当于
```
images.findColor(img, color, {
     region: [x, y, width, height],
     threshold: threshold
});
```

该函数也可以作为全局函数使用.

## images.findColorEquals(img, color[, x, y, width, height])
* `img` {Image} 图片
* `color` {number} | {string} 要寻找的颜色
* `x` {number} 找色区域的左上角横坐标
* `y` {number} 找色区域的左上角纵坐标
* `width` {number} 找色区域的宽度
* `height` {number} 找色区域的高度
* 返回 {Point}

在图片img指定区域中找到颜色和color完全相等的某个点，并返回该点的左边；如果没有找到，则返回`null`.

找色区域通过`x`, `y`, `width`, `height`指定，如果不指定找色区域，则在整张图片中寻找.

该函数也可以作为全局函数使用.

示例:
(通过找QQ红点的颜色来判断是否有未读消息)
```
requestScreenCapture();
launchApp("QQ");
sleep(1200);
var p = findColorEquals(captureScreen(), "#f64d30");
if(p){
    toast("有未读消息");
}else{
    toast("没有未读消息");
}
```

## images.findMultiColors(img, firstColor, colors[, options])
* `img` {Image} 要找色的图片
* `firstColor` {number} | {string} 第一个点的颜色
* `colors` {Array} 表示剩下的点相对于第一个点的位置和颜色的数组，数组的每个元素为[x, y, color]
* `options` {Object} 选项，包括:
    * `region` {Array} 找色区域.是一个两个或四个元素的数组.(region[0], region[1])表示找色区域的左上角；region[2]*region[3]表示找色区域的宽高.如果只有region只有两个元素，则找色区域为(region[0], region[1])到屏幕右下角.如果不指定region选项，则找色区域为整张图片.
    * `threshold` {number} 找色时颜色相似度的临界值，范围为0~255（越小越相似，0为颜色相等，255为任何颜色都能匹配）.默认为4.threshold和浮点数相似度(0.0~1.0)的换算为 similarity = (255 - threshold) / 255.


多点找色，类似于按键精灵的多点找色，其过程如下:
1. 在图片img中找到颜色firstColor的位置(x0, y0)
2. 对于数组colors的每个元素[x, y, color]，检查图片img在位置(x + x0, y + y0)上的像素是否是颜色color，是的话返回(x0, y0)，否则继续寻找firstColor的位置，重新执行第1步
3. 整张图片都找不到时返回`null`

例如，对于代码`images.findMultiColors(img, "#123456", [[10, 20, "#ffffff"], [30, 40, "#000000"]])`，假设图片在(100, 200)的位置的颜色为#123456, 这时如果(110, 220)的位置的颜色为#fffff且(130, 240)的位置的颜色为#000000，则函数返回点(100, 200).

如果要指定找色区域，则在options中指定，例如:
```
var p = images.findMultiColors(img, "#123456", [[10, 20, "#ffffff"], [30, 40, "#000000"]], {
    region: [0, 960, 1080, 960]
});
```

## images.detectsColor(image, color, x, y[, threshold = 16, algorithm = "diff"])
* `image` {Image} 图片
* `color` {number} | {string} 要检测的颜色
* `x` {number} 要检测的位置横坐标
* `y` {number} 要检测的位置纵坐标
* `threshold` {number} 颜色相似度临界值，默认为16.取值范围为0~255.
* `algorithm` {string} 颜色匹配算法，包括:
    * "equal": 相等匹配，只有与给定颜色color完全相等时才匹配.
    * "diff": 差值匹配.与给定颜色的R、G、B差的绝对值之和小于threshold时匹配.
    * "rgb": rgb欧拉距离相似度.与给定颜色color的rgb欧拉距离小于等于threshold时匹配.
 
    * "rgb+": 加权rgb欧拉距离匹配([LAB Delta E](https://en.wikipedia.org/wiki/Color_difference)).
    * "hs": hs欧拉距离匹配.hs为HSV空间的色调值.

返回图片image在位置(x, y)处是否匹配到颜色color.用于检测图片中某个位置是否是特定颜色.


一个判断微博客户端的某个微博是否被点赞过的例子:
```
requestScreenCapture();
//找到点赞控件
var like = id("ly_feed_like_icon").findOne();
//获取该控件中点坐标
var x = like.bounds().centerX();
var y = like.bounds().centerY();
//截图
var img = captureScreen();
//判断在该坐标的颜色是否为橙红色
if(images.detectsColor(img, "#fed9a8", x, y)){
    //是的话则已经是点赞过的了，不做任何动作
}else{
    //否则点击点赞按钮
    like.click();
}
```

## images.findImage(img, template[, options])
* `img` {Image} 大图片
* `template` {Image} 小图片（模板）
* `options` {Object} 找图选项

找图.在大图片img中查找小图片template的位置（模块匹配），找到时返回位置坐标(Point)，找不到时返回null.

选项包括:
* `threshold` {number} 图片相似度.取值范围为0~1的浮点数.默认值为0.9.
* `region` {Array} 找图区域.参见findColor函数关于region的说明.
* `level` {number} **一般而言不必修改此参数**.不加此参数时该参数会根据图片大小自动调整.找图算法是采用图像金字塔进行的, level参数表示金字塔的层次, level越大可能带来越高的找图效率，但也可能造成找图失败（图片因过度缩小而无法分辨）或返回错误位置.因此，除非您清楚该参数的意义并需要进行性能调优，否则不需要用到该参数.

该函数也可以作为全局函数使用.

一个最简单的找图例子如下:
```
var img = images.read("/sdcard/大图.png");
var templ = images.read("/sdcard/小图.png");
var p = findImage(img, templ);
if(p){
    toast("找到啦:" + p);
}else{
    toast("没找到");
}
```

稍微复杂点的区域找图例子如下:
```
auto();
requestScreenCapture();
var wx = images.read("/sdcard/微信图标.png");
//返回桌面
home();
//截图并找图
var p = findImage(captureScreen(), wx, {
    region: [0, 50],
    threshold: 0.8
});
if(p){
    toast("在桌面找到了微信图标啦: " + p);
}else{
    toast("在桌面没有找到微信图标");
}
```
## images.findImageInRegion(img, template, x, y[, width, height, threshold])

区域找图的简便方法.相当于:
```
images.findImage(img, template, {
    region: [x, y, width, height],
    threshold: threshold
})
```

该函数也可以作为全局函数使用.

## images.matchTemplate(img, template, options)
**[v4.1.0新增]**
* `img` {Image} 大图片
* `template` {Image} 小图片（模板）
* `options` {Object} 找图选项:
    * `threshold` {number} 图片相似度.取值范围为0~1的浮点数.默认值为0.9.
    * `region` {Array} 找图区域.参见findColor函数关于region的说明.
    * `max` {number} 找图结果最大数量，默认为5
    * `level` {number} **一般而言不必修改此参数**.不加此参数时该参数会根据图片大小自动调整.找图算法是采用图像金字塔进行的, level参数表示金字塔的层次, level越大可能带来越高的找图效率，但也可能造成找图失败（图片因过度缩小而无法分辨）或返回错误位置.因此，除非您清楚该参数的意义并需要进行性能调优，否则不需要用到该参数.
* 返回 {MatchingResult}

在大图片中搜索小图片，并返回搜索结果MatchingResult.该函数可以用于找图时找出多个位置，可以通过max参数控制最大的结果数量.也可以对匹配结果进行排序、求最值等操作.

# MatchingResult
**[v4.1.0新增]**
## matches
* {Array} 匹配结果的数组.

数组的元素是一个Match对象:
* `point` {Point} 匹配位置
* `similarity` {number} 相似度

例如: 
```
var result = images.matchTemplate(img, template, {
    max: 100
});
result.matches.forEach(match => {
    log("point = " + match.point + ", similarity = " + match.similarity);
});
```

## points
* {Array} 匹配位置的数组.

## first()
* 返回 {Match}

第一个匹配结果.如果没有任何匹配，则返回`null`.

## last()
* 返回 {Match}

最后一个匹配结果.如果没有任何匹配，则返回`null`.

## leftmost()
* 返回 {Match}

位于大图片最左边的匹配结果.如果没有任何匹配，则返回`null`.

## topmost()
* 返回 {Match}

位于大图片最上边的匹配结果.如果没有任何匹配，则返回`null`.

## rightmost()
* 返回 {Match}

位于大图片最右边的匹配结果.如果没有任何匹配，则返回`null`.

## bottommost()
* 返回 {Match}

位于大图片最下边的匹配结果.如果没有任何匹配，则返回`null`.

## best()
* 返回 {Match}

相似度最高的匹配结果.如果没有任何匹配，则返回`null`.

## worst()
* 返回 {Match}

相似度最低的匹配结果.如果没有任何匹配，则返回`null`.

## sortBy(cmp)
* cmp {Function}|{string} 比较函数，或者是一个字符串表示排序方向.例如"left"表示将匹配结果按匹配位置从左往右排序、"top"表示将匹配结果按匹配位置从上往下排序，"left-top"表示将匹配结果按匹配位置从左往右、从上往下排序.方向包括`left`（左）, `top` （上）, `right` （右）, `bottom`（下）.
* {MatchingResult}

对匹配结果进行排序，并返回排序后的结果.

```
var result = images.matchTemplate(img, template, {
    max: 100
});
log(result.sortBy("top-right"));
```

# Image

表示一张图片，可以是截图的图片，或者本地读取的图片，或者从网络获取的图片.

## Image.getWidth()

返回以像素为单位图片宽度.

## Image.getHeight()

返回以像素为单位的图片高度.

## Image.saveTo(path)
* `path` {string} 路径

把图片保存到路径path.（如果文件存在则覆盖）

## Image.pixel(x, y)
* `x` {number} 横坐标
* `y` {number} 纵坐标

返回图片image在点(x, y)处的像素的ARGB值.  

该值的格式为0xAARRGGBB，是一个"32位整数"(虽然JavaScript中并不区分整数类型和其他数值类型).

坐标系以图片左上角为原点.以图片左侧边为y轴，上侧边为x轴.

##

# Point

findColor, findImage返回的对象.表示一个点（坐标）.

## Point.x 

横坐标.

## Point.y

纵坐标.
