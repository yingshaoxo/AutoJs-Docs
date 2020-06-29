# Console

> Stability: 2 - Stable

It's a console for loging.

You can print messages to it by using `log()`, `print()`.

## console.show()

Show the console as a floating window. (Needs the floating window permission)

## console.hide()

Hide the floating console.

## console.clear()

Clear console text.

## console.log([data][, ...args])#
* `data` {any}
* `...args` {any}

Print text to console with a '\n'.

```js
const count = 5;

// print 'count: 5' to console
console.log('count: %d', count);

// print 'count: 5' to console
console.log('count:', count);
```

See more at `util.format()`

## print(text)
* text {string} | {Object} What you want to print

Equivalent to `log(text)`.

## console.verbose([data][, ...args])
* `data` {any}
* `...args` {any}

Similar to `console.log`, but with grey color.

## console.info([data][, ...args])
* `data` {any}
* `...args` {any}

Similar to `console.log`, but with green color.

## console.warn([data][, ...args])
* `data` {any}
* `...args` {any}

Similar to `console.log`, but with blue color.

## console.error([data][, ...args])
* `data` {any}
* `...args` {any}

Similar to `console.log`, but with red color.

## console.assert(value, message)
* value {any}
* message {string} the error message

If the value == false, we'll stop the running of script.

```js
var a = 1 + 1;
console.assert(a == 2, "You'll never see this error message");
```

## console.time([label])
* `label` {String} distinguish different timer

Start a timer. It is used to calculate a time interval.

## console.timeEnd(label)
* `label` {String} 计时器标签

End a timer, It will print out the time interval to console since you call `console.time`.

It is based on millisecond.

```js
console.time('sum_function');
var sum = 0;
for(let i = 0; i < 100000; i++){
    sum += i;
}
console.timeEnd('sum_function');

// it'll print out "sum_function: xxx ms"
```

## console.trace([data][, ...args])
* `data` {any}
* `...args` {any}

Similar to `console.log`, but it'll print out information about the parent function who called this function.

```js
console.trace('Show me');

// Show me
//  at <test>:7
```

## console.input(data[, ...args])
* `data` {any}
* `...args` {any}

Get input from console. We use the `eval` to do the pre-processing.

```js
var n = console.input("Please input a number:"); 
//after you type 123
toast(n + 1);
//it shows 124
```

**May not work at some devices**

## console.rawInput(data[, ...args])
* `data` {any}
* `...args` {any}

Get raw input string from console. 

```js
var n = console.input("Please input a number:"); 
//after you type 123
toast(n + 1);
//it shows 1231
```

**May not work at some devices**

## console.setSize(w, h)
* `w` {number} width
* `h` {number} height

Set the console window size.

```js
console.show();
console.setSize(device.width / 2, device.height / 2);
```

## console.setPosition(x, y)
* `x` {number} 
* `y` {number}

Set the console window position

```js
console.show();
console.setPosition(100, 100);
```

## console.setGlobalLogConfig(config)
* `config` {Object}
    * `file` {string} log file path
    * `maxFileSize` {number} Max file size, default value is 512*1024 (512KB)
    * `rootLevel` {string} log level, default value is "ALL", it can be "OFF", "DEBUG", "INFO", "WARN", "ERROR", "FATAL"
    * `maxBackupSize` {number} default value is 5
    * `filePattern` {string} log format. See more at [PatternLayout](http://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/PatternLayout.html)

Logger settings.

If you want to save your log file to "/sdcard/1.txt", you do this:

```js
console.setGlobalLogConfig({
    "file": "/sdcard/1.txt"
});
```
