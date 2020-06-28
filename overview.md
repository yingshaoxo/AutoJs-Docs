# Overview

OpenAuto.js uses [JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript) as the programming language. 

Now it is based on [Rhino 1.7.7.2](https://developer.mozilla.org/zh-CN/docs/Mozilla/Projects/Rhino) js engine, it supports ES5 and part of ES6 features.

We basically support two kinds of automation, one is to use `accessibility service`, another is to use `ROOT`.

The main module or class we have is:
* app: start an app, uninstall an app, check an app's usage, edit a text file, visit a website, and so on.
* console: record information, works as a logger.
* device: used to get information about the device, like screen height and width, brightness, volume, and so on.
* engines: used to start other scripts.
* events: listening keypress, listening notification, listening screen touch, and so on.
* floaty: it is used to create a custom floating window.
* files: file creating、read and write.
* http: sending HTTP requests. Like GET, POST.
* images, colors: screenshot, find pictures, find colors, read and save pictures...
* keys: fake a key pressing. Like a Home key, a Back key, and so on.
* shell: run shell commands.
* threads: used to support thread programming.
* ui: Used to create custom UI.

We also support [Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise).
