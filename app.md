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

If we can not find that app, we return null.

```
var name = getPackageName("Chrome"); //return "com.android.chrome"
```

## app.getAppName(packageName)
* `packageName` {string} 

Get app name by using app package name.

If we can not find that app, we return null.

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

## app.intent(options)
* `options` {Object} including:
    * `action` {string} it's a string，like "android.intent.action.SEND". if an action starts with "android.intent.action", you can just use"SEND" instead. More info: [Actions](https://developer.android.com/reference/android/content/Intent.html#standard-activity-actions).

    * `type` {string} MimeType，like "text/plain".

    * `data` {string} Data，it's an Uri. For example, if you want to open a file with the action "android.intent.action.VIEW", the data should be "file:///sdcard/1.txt".

    * `category` {Array} More info: [Categories](https://developer.android.com/reference/android/content/Intent.html#standard-categories).

    * `packageName` {string} target app package name

    * `className` {string} target Activity or Service name

    * `extras` {Object} Intent's Extras. See more at [Extras](https://developer.android.com/reference/android/content/Intent.html#standard-extra-data)。

    * `flags` {Array} intent's flags, it's an array of strings, like `["activity_new_task", "grant_read_uri_permission"]`. See more at [Flags](https://developer.android.com/reference/android/content/Intent.html#setFlags%28int%29)。


    Example:
    ```
    //open an image
    var i = app.intent({
        action: "VIEW",
        type: "image/png",
        data: "file:///sdcard/1.png"
    });
    context.startActivity(i);
    ```

    More info: [Intent filters](https://developer.android.com/guide/components/intents-filters.html#Types).


## app.startActivity(options)
* `options` {Object}
    * ... same with the `app.intent(options)` function
    * `root` {Boolea} weather to start it with root permission.

Create an Intent，and start it as an Activity.

```
app.startActivity({
    action: "SEND",
    type: "text/plain",
    data: "file:///sdcard/1.txt"
});
```

## app.sendBroadcast(options)
* `options` {Object} 

Create an Intent，and send broadcast.

## app.startService(options)
* `options` {Object} 

Create an Intent，and start service.

## app.intentToShell(options)

* `options` {Object}

Create an Intent, and convert it to shell command.

For example:
```
shell("am start " + app.intentToShell({
    packageName: "org.autojs.autojs",
    className: "org.autojs.autojs.ui.settings.SettingsActivity_"
}), true);
```

More info: [intent Spec](https://developer.android.com/studio/command-line/adb#IntentSpec)。

## app.startActivity(name)
* `name` {string} OpenAuto.js's activity name. Optional value is:
    * `console` OpenAuto.js console logger
    * `settings` OpenAuto.js setting page

Start specific OpenAuto.js page, for example the value 'console' will start the logger page in OpenAuto.js.

```
app.startActivity("console");
```

## app.sendBroadcast(name)
* `name` {string} OpenAuto.js inspector name：
    * `inspect_layout_hierarchy` Check layout
    * `inspect_layout_bounds` Check elements

```
app.sendBroadcast("inspect_layout_bounds");
```

## app.parseUri(uri)

* `uri` {string} an Uri string, like"file:///sdcard/1.txt" or  "https://www.google.com"

Return an Uri object, this is the defination of that object: [android.net.Uri](https://developer.android.com/reference/android/net/Uri).

This function will always return an Uri object, even if you give it a wrong string.

For higher Android version, if the uri string is `file://...`, somethng like this `content://...` will be returned.

## app.getUriForFile(path)

* `path` {string} file path, like "/sdcard/1.txt"

Return an Uri object, this is the defination of that object: [android.net.Uri](https://developer.android.com/reference/android/net/Uri).

For higher Android version, if the uri string is `file://...`, somethng like this `content://...` will be returned.
