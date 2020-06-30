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

## Picture finder or Color finder

## images.requestScreenCapture([landscape])
* `landscape` {boolean} if landscape == false, capture vertically; else capture horizontally.

Ask for screenshot permission.

Return true if success.

> Suggest to do this within the auto.js UI.

```
if(!requestScreenCapture()){
    toast("Failed to ask for screenshot permission");
    exit();
}
//capture 10 screenshot and save them to sdcard
for(var i = 0; i < 10; i++){
    captureScreen("/sdcard/screencapture" + i + ".png");
    sleep(1000);
}
```

## images.captureScreen()

Do a screenshot and return an Image object.

If no captureing permission, we will raise SecurityException.

> Capturing inverval time <= 16ms may return a same image.

```
//ask for permission
requestScreenCapture(true);
//screenshot
var img = captureScreen();
//get a color at point (100, 100)
var color = images.pixel(img, 100, 100);
//show the color
toast(colors.toString(color));
```

## images.captureScreen(path)
* `path` {string} page to save that image

Do a screenshot and save image with .PNG format.

## images.pixel(image, x, y)
* `image` {Image}
* `x` {number}
* `y` {number}

Return ARGB value of a pixel at a certain point at image.

The return value is a int number (0xAARRGGBB).

## images.findColor(image, color, options)
* `image` {Image}
* `color` {number} | {string} The RGB value that you want to search. (0xRRGGBB or "#RRGGBB")
* `options` {Object} options are:
    * `region` {Array} [up-left-x, up-left-y, width, height], if no paramater was given, we search for the whole screen.
    * `threshold` {number} 0~255 (the smaller, the more accurate. 0 means only work when color totally match). similarity = (255 - threshold) / 255.

Find color at image.

Return null if no color was found.

An example of color finding:
```js
requestScreenCapture();

//look for #ff0000
while(true){
    var img = captureScreen();
    var point = findColor(img, "#ff0000");
    if(point){
        toast("I found red color, the coordinate is (" + point.x + ", " + point.y + ")");
    }
}

```

An example of color finding at a region:
```js
//read local image /sdcard/1.png
var img = images.read("/sdcard/1.png");
//check if it's loading successfully
if(!img){
    toast("No such image");
    exit();
}
//color finding from point(400, 500) to point(400+300, 500+200)
var point = findColor(img, "#00ff00", {
     region: [400, 500, 300, 200],
     threshold: 4
 });
if(point){
    toast("I found it:" + point);
}else{
    toast("No such a color");
}
```

## images.findColorInRegion(img, color, x, y[, width, height, threshold])

Equivalent to:
```js
images.findColor(img, color, {
     region: [x, y, width, height],
     threshold: threshold
});
```

## images.findColorEquals(img, color[, x, y, width, height])
* `img` {Image}
* `color` {number} | {string} the color you're looking for
* `x` {number} up-left corner x
* `y` {number} up-left corner y
* `width` {number} region width
* `height` {number} region height 
* return {Point}

Find a color at an image.

If found, return the point, if not, return null.

> `x`, `y`, `width`, `height` can be ignored.


```js
requestScreenCapture();
launchApp("Facebook");
sleep(1200);
var p = findColorEquals(captureScreen(), "#f64d30");
if(p){
    toast("Have unread message");
}else{
    toast("No new messages");
}
```

## images.findMultiColors(img, firstColor, colors[, options])
* `img` {Image}
* `firstColor` {number} | {string} The first color point.
* `colors` {Array} Other color points relative to the first point. Each element of this array is `[x, y, color]`.
* `options` {Object} options are:
    * `region` {Array} [up-left-x, up-left-y, width, height], if no paramater was given, we search for the whole screen.
    * `threshold` {number} 0~255 (the smaller, the more accurate. 0 means only work when color totally match). similarity = (255 - threshold) / 255.

The logic:
1. We'll try to find the position of firstColor. Let's say it is `(x0, y0)`.
2. For each elemtnt `[x, y, color]` in colors array，we check if the color of `(x + x0, y + y0)` == color，if so we return `(x0, y0)`，else we go back to step 1.
3. If no firstColor was found, we return `null`

For example，for the code `images.findMultiColors(img, "#123456", [[10, 20, "#ffffff"], [30, 40, "#000000"]])`

Let's assume the color of (100, 200) is #123456, if the color of (110, 220) is #fffff and the color of (130, 240) is #000000，we return (100, 200).

You can also use the option region:
```js
var p = images.findMultiColors(img, "#123456", [[10, 20, "#ffffff"], [30, 40, "#000000"]], {
    region: [0, 960, 1080, 960]
});
```

## images.detectsColor(image, color, x, y[, threshold = 16, algorithm = "diff"])
* `image` {Image}
* `color` {number} | {string} the color you want to detect
* `x` {number} point x
* `y` {number} point y
* `threshold` {number} defaults to 16. The range is 0~255.
* `algorithm` {string} options are:
    * "equal": Identical equal or total equal
    * "diff": Difference matching. Match when the sum of absolute values of R, G, and B differences for a given color is less than threshold.
    * "rgb": rgb Euler distance similarity. Match when the rgb Euler distance of the given color is less than or equal to the threshold.
    * "rgb+": Weighted rgb Euler distance matching. See more at ([LAB Delta E](https://en.wikipedia.org/wiki/Color_difference)).
    * "hs": hs Euler distance matches. hs is the hue value of the HSV space.

Check if the color at image (x,y) macths your color.

Return true if so.

```js
requestScreenCapture();
//find an UI component
var like = id("ly_feed_like_icon").findOne();
//get the center point of that component
var x = like.bounds().centerX();
var y = like.bounds().centerY();
//do a screenshot
var img = captureScreen();
//check if the color at that point matchs #fed9a8
if(images.detectsColor(img, "#fed9a8", x, y)){
    // yes, we do nothing
}else{
    // no, we do a click
    like.click();
}
```

## images.findImage(img, template[, options])
* `img` {Image} parent image
* `template` {Image} target sub image
* `options` {Object} options are:
    * `threshold` {number} similarity. range in [0, 1.0]. the default value is 0.9.
    * `region` {Array} [up-left-x, up-left-y, width, height], if no paramater was given, we search for the whole screen.
    * `level` {number} can be ignored, but the bigger this number, the quicker for image finding

Find a smaller picture at a bigger picture.

If found, we return the up-left Point of the target image，else return null.

A simple example:
```js
var img = images.read("/sdcard/parent.png");
var templ = images.read("/sdcard/child.png");
var p = findImage(img, templ);
if(p){
    toast("I found it:" + p);
}else{
    toast("child image not in parent image");
}
```

A more complex example:
```js
auto();
requestScreenCapture();
var wx = images.read("/sdcard/an_app_icon.png");
//return home
home();
//do screen capture and try to find that icon
var p = findImage(captureScreen(), wx, {
    region: [0, 50],
    threshold: 0.8
});
if(p){
    toast("I found that icon at home page: " + p);
}else{
    toast("I don't see any icon at home page");
}
```

## images.findImageInRegion(img, template, x, y[, width, height, threshold])

Equivalent to:
```
images.findImage(img, template, {
    region: [x, y, width, height],
    threshold: threshold
})
```

## images.matchTemplate(img, template, options)
* `img` {Image} parent image
* `template` {Image} target sub-image
* `options` {Object} options are:
    * `threshold` {number} similarity. range in [0, 1.0]. the default value is 0.9.
    * `region` {Array} [up-left-x, up-left-y, width, height], if no paramater was given, we search for the whole screen.
    * `max` {number} the max number of target sub-image we return，defaults to 5
    * `level` {number} can be ignored, but the bigger this number, the quicker for image finding
* return {MatchingResult}

Similar to `images.findImage(img, template[, options])`, but it can get many sub-images from parent image.

# MatchingResult
## matches
* {Array} array of matches.

`Match` is an object:
* `point` {Point} the up-left corner of the target sub-image
* `similarity` {number} how similar this real sub-image compared to the sub-image you gaving

For exmaple:
```js
var result = images.matchTemplate(img, template, {
    max: 100
});
result.matches.forEach(match => {
    log("point = " + match.point + ", similarity = " + match.similarity);
});
```

## points
* {Array} array of points.

## first()
* return {Match}

Return the first Match.

If no matches at all, we return null.

## last()
* return {Match}

Return the last Match.

If no matches at all, we return null.

## leftmost()
* return {Match}

Return the most left Match within the parent image.

If no matches at all, we return null.

## topmost()
* return {Match}

Return the most top Match within the parent image.

If no matches at all, we return null.

## rightmost()
* return {Match}

Return the most right Match within the parent image.

If no matches at all, we return null.

## bottommost()
* return {Match}

Return the most bottom Match within the parent image.

If no matches at all, we return null.

## best()
* return {Match}

Return the most similar Match within the parent image.

If no matches at all, we return null.

## worst()
* return {Match}

Return the most not similar Match within the parent image.

If no matches at all, we return null.

## sortBy(cmp)
* cmp {Function}|{string} comparing function，or a simple string like "left","top","left-top". "left" means sort from left to right. "top" means sort from top to bottom. "left-top" means sort from left to right and meanwhile from top to bottom.
* return {MatchingResult}

Sort the `MatchingResult`, and return a new `MatchingResult`.

```js
var result = images.matchTemplate(img, template, {
    max: 100
});
log(result.sortBy("top-right"));
```

# Image

Represent an image.

## Image.getWidth()


## Image.getHeight()


## Image.saveTo(path)
* `path` {string} whre to save

Save that image to a place.

## Image.pixel(x, y)
* `x` {number}
* `y` {number}

Return the ARGB color value at point(x,y).

ARGB: 0xAARRGGBB

# Point

Represents a point.

## Point.x 

## Point.y
