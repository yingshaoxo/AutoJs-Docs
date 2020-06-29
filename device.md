# Device

> Stability: 2 - Stable

This module has provided information about the device you are using.

## device.width 
* {number}

## device.height 
* {number}

## device.buildId
* {string}

Either a changelist number, or a label like "M4-rc20".

## device.broad 
* {string}

The name of the underlying(mother) board, like "goldfish".

## device.brand
* {string}

The consumer-visible brand with which the product/hardware will be associated, if any.

Such as "Xiaomi", "google".

## device.device
* {string}

The name of the industrial design.

## deivce.model
* {string}

The end-user-visible name for the end product.

## device.product
* {string}

The name of the overall product.

## device.bootloader
* {string}

The system bootloader version number.

## device.hardware
* {string}

The name of the hardware (from the kernel command line or /proc).

## device.fingerprint
* {string}

A string that uniquely identifies this build.  Do not attempt to parse this value.

## device.serial
* {string}

A hardware serial number, if available. Alphanumeric only, case-insensitive.

## device.sdkInt
* {number}

The user-visible SDK version of the framework; its possible values are defined in Build.VERSION_CODES.

## device.incremental
* {string}

The internal value used by the underlying source control to represent this build. E.g., a perforce changelist number or a git hash.

## device.release
* {string}

The user-visible version string. E.g., "8.0" or "7.1.1".

## device.baseOS
* {string}

The base OS build the product is based on.

## device.securityPatch
* {string}

The user-visible security patch level.

## device.codename
* {string}

The current development codename, or the string "REL" if this is a release build.

## device.getIMEI()
* {string}

Return IMEI.

## device.getAndroidId()
* {string}

Return Android ID.

## device.getMacAddress()
* {string}

Return MAC address if it got WLAN access. Else return null.

## device.getBrightness()
* {number}

Return current brightness. Range in [0, 255].

## device.getBrightnessMode()
* {number}

Return the brightness mode: auto or manual.

## device.setBrightness(b)
* `b` {number} brightness, a number between 0 and 255

Set current brightness. Range in [0, 255].

Only works when the phone brightness in manual mode.

## device.setBrightnessMode(mode)
* `mode` {number} 0 is manul，1 is auto

Set current brightness mode.

## device.getMusicVolume()
* {number}

Return current music volume value.

## device.getNotificationVolume()
* {number}

Return current notifacation volume value.

## device.getAlarmVolume()
* {number}

Return current alarm volume value.

## device.getMusicMaxVolume()
* {number} 

Return max music volume value.

## device.getNotificationMaxVolume()
* {number} 

Return max notifacation volume value.

## device.getAlarmMaxVolume()
* {number} 

Return max alarm volume value.

## device.setMusicVolume(volume)
* `volume` {number} 

Set current music volume value.

## device.setNotificationVolume(volume)
* `volume` {number}

Set current notifacation volume value.

## device.setAlarmVolume(volume)
* `volume` {number} 

Set current alarm volume value.

## device.getBattery()
* {number} 0.0 to 100.0

Return current battery value.

## device.isCharging()
* {boolean}

Return true is the phone is in charging.

## device.getTotalMem()
* {number}

Return device total memory. 

The Unit is B.

1MB = 1024 * 1024B.

## device.getAvailMem()
* {number}

Return current avaliable memory.

The Unit is B.

1MB = 1024 * 1024B.

## device.isScreenOn()
* {boolean}

Check if the screen is on, if so, return true, else return false.

## device.wakeUp()

Wake up the device.

You can use it to light up the screen.

## device.wakeUpIfNeeded()

Wake up the device.

You can use it to light up the screen.

## device.keepScreenOn([timeout])
* `timeout` {number} How many milliseconds you want the screen on. Without this argument, the screen will always on.

We encorage you to use a timeout argument: `device.keepScreenOn(3600 * 1000)`.

> You can use `device.cancelKeepingAwake()` to cancel this action.

## device.keepScreenDim([timeout])
* `timeout` {number} How many milliseconds you want the screen on. Without this argument, the screen will always on.

Keep the screen on but allowing it to be dim.

> You can use `device.cancelKeepingAwake()` to cancel this action.

## device.cancelKeepingAwake()

Cancel the `device.keepScreenOn()` action.

## device.vibrate(millis)
* `millis` {number} miliseconds

Keep the device vibrate for a few milliseconds.

```
//vibrate for 2 seconds
device.vibrate(2000);
```

## device.cancelVibration()

Cancel the vibration.
