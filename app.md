# App

This module provides a series of functions for interacting with Apps.

Like `starting an app`, `start an activity`, `send a broadcast`, `send a picture`, `send emails`.

## app.versionCode
* {number}

current app version code, like `160`

```
toastLog(app.versionCode);
```

## app.versionName
* {string}

current app version name, like `3.0.0 Beta` 

```
toastLog(app.verionName);
```

## app.autojs.versionCode
* {number}

OpenAuto.js app version code, like `160`

## app.autojs.versionName
* {string}

OpenAuto.js app version name, like `3.0.0 Beta` 

## app.launchApp(appName)
* `appName` {string}

Start an App by its name.

If that App doesn't exist, we return false, else we return true.

```
launchApp("Chrome");
```

## app.launch(packageName)
* `packageName` {string}

Start an App by its package name.

If that App doesn't exist, we return false, else we return true.

```
launch("com.android.chrome");
```

## app.launchPackage(packageName)
* `packageName` {string}

Same API as `app.launch(packageName)`

## app.getPackageName(appName)
* `appName` {string}

Get app package name by using app name.

If we can not find that app, we return `null`.

```
var name = getPackageName("Chrome"); //return "com.android.chrome"
```

## app.getAppName(packageName)
* `packageName` {string} 

Get app name by using app package name.

If we can not find that app, we return `null`.

```
var name = getAppName("com.android.chrome"); //return "Chrome"
```

## app.openAppSetting(packageName)
* `packageName` {string}

Open the detail or setting page of an app.

If we can't find that app, return false, else return true.

## app.viewFile(path)
* `path` {string}

Open a file.

If we can't find a suitable app to open it, we raise `ActivityNotException`.

```
app.viewFile("/sdcard/1.txt");
```

## app.editFile(path)
* `path` {string}

Edit a file.

If we can't find a suitable app to edit it, we raise `ActivityNotException`.

```
app.editFile("/sdcard/1.txt/);
```

## app.uninstall(packageName)
* `packageName` {string}

```
//uninstall an app
app.uninstall("com.tencent.mm");
```

## app.openUrl(url)
* `url` {string}

Open an url with a browser.

If no browser was found, we raise `ActivityNotException`.

## app.sendEmail(options)
*  `options` {Object} including:
  * `email` {string} | {Array} Receiver email address.
  * `cc` {string} | {Array} Cc recipient's email address.
  * `bcc` {string} | {Array} Bcc recipient's email address.
  * `subject` {string} Title
  * `text` {string} Content
  * `attachment` {string} attachment file path.

If no email app was avaliable, we raise `ActivityNotException`.

```
//send email to 10086@qq.com and 10001@qq.com.
app.sendEmail({
    email: ["10086@qq.com", "10001@qq.com"],
    subject: "This is the title",
    text: "This is the content"
});
```

## app.startActivity(name)
* `name` {string} OpenAuto.js's activity name. Optional value is:
    * `console` OpenAuto.js console logger
    * `settings` OpenAuto.js setting page

Start specific OpenAuto.js page, for example the value 'console' will start the logger page in OpenAuto.js.

```
app.startActivity("console");
```


# 进阶: 意图Intent

Intent(意图) 是一个消息传递对象，您可以使用它从其他应用组件请求操作。尽管 Intent 可以通过多种方式促进组件之间的通信，但其基本用例主要包括以下三个：

* 启动活动(Activity)：
    Activity 表示应用中的一个"屏幕"。例如应用主入口都是一个Activity，应用的功能通常也以Activity的形式独立，例如微信的主界面、朋友圈、聊天窗口都是不同的Activity。通过将 Intent 传递给 startActivity()，您可以启动新的 Activity 实例。Intent 描述了要启动的 Activity，并携带了任何必要的数据。

* 启动服务(Service)：
    Service 是一个不使用用户界面而在后台执行操作的组件。通过将 Intent 传递给 startService()，您可以启动服务执行一次性操作（例如，下载文件）。Intent 描述了要启动的服务，并携带了任何必要的数据。

* 传递广播：
    广播是任何应用均可接收的消息。系统将针对系统事件（例如：系统启动或设备开始充电时）传递各种广播。通过将 Intent 传递给 sendBroadcast()、sendOrderedBroadcast() 或 sendStickyBroadcast()，您可以将广播传递给其他应用。

本模块提供了构建Intent的函数(`app.intent()`), 启动Activity的函数`app.startActivity()`, 发送广播的函数`app.sendBroadcast()`。

使用这些方法可以用来方便的调用其他应用。例如直接打开某个QQ号的个人卡片页，打开某个QQ号的聊天窗口等。

```
var qq = "2732014414";
app.startActivity({ 
    action: "android.intent.action.VIEW", 
    data:"mqq://im/chat?chat_type=wpa&version=1&src_type=web&uin=" + qq, 
    packageName: "com.tencent.mobileqq", 
});

```

## app.intent(options)
* `options` {Object} 选项，包括：
    * `action` {string} 意图的Action，指意图要完成的动作，是一个字符串常量，比如"android.intent.action.SEND"。当action以"android.intent.action"开头时，可以省略前缀，直接用"SEND"代替。参见[Actions](https://developer.android.com/reference/android/content/Intent.html#standard-activity-actions)。

    * `type` {string} 意图的MimeType，表示和该意图直接相关的数据的类型，表示比如"text/plain"为纯文本类型。

    * `data` {string} 意图的Data，表示和该意图直接相关的数据，是一个Uri, 可以是文件路径或者Url等。例如要打开一个文件, action为"android.intent.action.VIEW", data为"file:///sdcard/1.txt"。

    * `category` {Array} 意图的类别。比较少用。参见[Categories](https://developer.android.com/reference/android/content/Intent.html#standard-categories)。

    * `packageName` {string} 目标包名

    * `className` {string} 目标Activity或Service等组件的名称

    * `extras` {Object} 以键值对构成的这个Intent的Extras(额外信息)。提供该意图的其他信息，例如发送邮件时的邮件标题、邮件正文。参见[Extras](https://developer.android.com/reference/android/content/Intent.html#standard-extra-data)。

    * `flags` {Array} intent的标识，字符串数组，例如`["activity_new_task", "grant_read_uri_permission"]`。参见[Flags](https://developer.android.com/reference/android/content/Intent.html#setFlags%28int%29)。

      **[v4.1.0新增]**

    * `root` {Boolea} 是否以root权限启动、发送该intent。使用该参数后，不能使用`context.startActivity()`等方法，而应该直接使用诸如`app.startActivity({...})`的方法。

      **[v4.1.0新增]**

根据选项，构造一个意图Intent对象。

例如：
```
//打开应用来查看图片文件
var i = app.intent({
    action: "VIEW",
    type: "image/png",
    data: "file:///sdcard/1.png"
});
context.startActivity(i);
```

需要注意的是，除非应用专门暴露Activity出来，否则在没有root权限的情况下使用intent是无法跳转到特定Activity、应用的特定界面的。例如我们能通过Intent跳转到QQ的分享界面，是因为QQ对外暴露了分享的Activity；而在没有root权限的情况下，我们无法通过intent跳转到QQ的设置界面，因为QQ并没有暴露这个Activity。

但如果有root权限，则在intent的参数加上`"root": true`即可。例如使用root权限跳转到Auto.js的设置界面为：
```
app.startActivity({
    packageName: "org.autojs.autojs",
    className: "org.autojs.autojs.ui.settings.SettingsActivity_",
    root: true
});
```

另外，关于intent的参数如何获取的问题，一些intent是意外发现并且在网络中传播的（例如跳转QQ聊天窗口是因为QQ给网页提供了跳转到客服QQ的方法），如果要自己获取活动的intent的参数，可以通过例如"intent记录"，"隐式启动"等应用拦截内部intent或者查询暴露的intent。其中拦截内部intent需要XPosed框架，或者可以通过反编译等手段获取参数。总之，没有简单直接的方法。

更多信息，请百度[安卓Intent](https://www.baidu.com/s?wd=android%20Intent)或参考[Android指南: Intent](https://developer.android.com/guide/components/intents-filters.html#Types)。


## app.startActivity(options)
* `options` {Object} 选项

根据选项构造一个Intent，并启动该Activity。

```
app.startActivity({
    action: "SEND",
    type: "text/plain",
    data: "file:///sdcard/1.txt"
});
```

## app.sendBroadcast(options)
* `options` {Object} 选项

根据选项构造一个Intent，并发送该广播。

## app.startService(options)
* `options` {Object} 选项

根据选项构造一个Intent，并启动该服务。

## app.sendBroadcast(name)
**[v4.1.0新增]**
* `name` {string} 特定的广播名称，包括：
    * `inspect_layout_hierarchy` 布局层次分析
    * `inspect_layout_bounds` 布局范围

发送以上特定名称的广播可以触发Auto.js的布局分析，方便脚本调试。这些广播在Auto.js发送才有效，在打包的脚本上运行将没有任何效果。

```
app.sendBroadcast("inspect_layout_bounds");
```

## app.intentToShell(options)

**[v4.1.0新增]**

* `options` {Object} 选项

根据选项构造一个Intent，转换为对应的shell的intent命令的参数。

例如: 
```
shell("am start " + app.intentToShell({
    packageName: "org.autojs.autojs",
    className: "org.autojs.autojs.ui.settings.SettingsActivity_"
}), true);
```

参见[intent参数的规范](https://developer.android.com/studio/command-line/adb#IntentSpec)。

## app.parseUri(uri)

**[v4.1.0新增]**

* `uri` {string} 一个代表Uri的字符串，例如"file:///sdcard/1.txt", "https://www.autojs.org"
* 返回 {Uri} 一个代表Uri的对象，参见[android.net.Uri](https://developer.android.com/reference/android/net/Uri)。

解析uri字符串并返回相应的Uri对象。即使Uri格式错误，该函数也会返回一个Uri对象，但之后如果访问该对象的scheme, path等值可能因解析失败而返回`null`。

需要注意的是，在高版本Android上，由于系统限制直接在Uri暴露文件的绝对路径，因此如果uri字符串是文件`file://...`，返回的Uri会是诸如`content://...`的形式。

## app.getUriForFile(path)

**[v4.1.0新增]**

* `path` {string} 文件路径，例如"/sdcard/1.txt"
* 返回 {Uri} 一个指向该文件的Uri的对象，参见[android.net.Uri](https://developer.android.com/reference/android/net/Uri)。

从一个文件路径创建一个uri对象。需要注意的是，在高版本Android上，由于系统限制直接在Uri暴露文件的绝对路径，因此返回的Uri会是诸如`content://...`的形式。
