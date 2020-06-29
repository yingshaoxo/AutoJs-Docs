# Global variable and functions

You can use global variable or functions at anywhere within your script.

You can use any built-in Javascript functions, like `setInterval`, `setTimeout`.

Except the following: (see more at [module](modules.html))
* exports
* module
* require()

## sleep(n)
* `n` {number} Milliseconds

Stop running for n milliseconds.

1 second == 1000 milliseconds.

```
//pause for 5 seconds
sleep(5000);
```

## currentPackage()
* return {string}

Return the current running package name. (we do it by check the lastest running app)

## currentActivity()
* return {string}

Return the current running Activity name. (we do it by check the lastest running activity)

## setClip(text)
* `text` {string}

Set clipboard text.

```
setClip("Hello world");
```

## getClip()
* return {string}

Get clipboard text

```
toast("This is what in your clipboard:" + getClip());
```

## toast(message)
* message {string} text that you want to show

This function may block the script process. If you are in a loop, and you keep print something, you can not stop this script instantly, for example:
```js
for(var i = 0; i < 100; i++){
  toast(i);
}
```

Add sleep to fix it:
```js
for(var i = 0; i < 100; i++){
  toast(i);
  sleep(2000);
}
```

Change this function to fix it:
```js
var _toast_ = toast;
toast = function(message){
  _toast_(message);
  sleep(2000);
}
for(var i = 0; i < 100; i++){
  toast(i);
}
```

## toastLog(message)
* message {string} 

Show text and do a log.

Equivalent to `toast(message);log(message)`.  See more at `console.log()`.

## waitForActivity(activity[, period = 200])
* `activity` Activity name
* `period` loop interval（in milliseconds）

Wait until specific Activity showup. 

## waitForPackage(package[, period = 200])
* `package` package name
* `period` loop interval（in milliseconds）

Wait until specific app showup. 

For example, `waitForPackage("com.twitter.android")` will block the process until twitter start.

## exit()
Instantly stop the running of this script.

We do it by raising `ScriptInterrupttedException`.

## random(min, max)
* `min` {number}
* `max` {number}
* return {number}

Return a number between min and max. 

For example, random(0, 2) will return a number within [0, 1, 2].

## random()
* return {number}

return a float between [0, 1).

## requiresApi(api)
* `api` Android version number

For example, `requiresApi(19)` means that this script is only usable at Android 4.4 or higher.

We'll raise error if the requirements not meet.

Android Version vs API table:

 Version：     API Level

 Android 7.0：  24

 Android 6.0：  23

 Android 5.1：  22

 Android 5.0：  21

 Android 4.4W：  20

 Android 4.4：  19

 Android 4.3：  18

## requiresAutojsVersion(version)
* `version` {string} | {number} OpenAuto.js version number or name

For example, `requiresAutojsVersion("3.0.0 Beta")` means that this script is only usable at OpenAuto.js 3.0.0 Beta or higher.

We'll raise error if the requirements not meet.

You can use `app.autojs.versionCode` and `app.autojs.versionName` to get current OpenAuto.js version number and version name.

## runtime.requestPermissions(permissions)
* `permissions` {Array}

Dynamically require android permission:
```
//Ask for GPS permission
runtime.requestPermissions(["access_fine_location"]);
```

Currently, we only have two permissions in Manifest:
* `access_fine_location` GPS permission
* `record_audio` recording permission

You can use APk editor or compile this software by yourself to add more permissions.

See more permissions at [Permissions Overview](https://developer.android.com/guide/topics/permissions/overview).

## runtime.loadJar(path)
* `path` {string} jar file path

Load jar file, after successfully loading, you would be able to use classes under that jar file:
```
// load jsoup.jar
runtime.loadJar("./jsoup.jar");
// use jsoup to parse html
importClass(org.jsoup.Jsoup);
log(Jsoup.parse(files.read("./test.html")));
```

([Jsoup](https://jsoup.org/download))

## runtime.loadDex(path)
* `path` {string} dex file path

Load dex file, after successfully loading, you would be able to use classes under that dex file:

> It would be faster by loading dex than jar

## context

An instance of `android.content.Context`.

> You can't use this context to create UI.
