# ADB over WIFI/TCP.

## Why?
Because for some reason you need it. If you don't need it, then just don't do it for sake of doing it.

## Important information
This is newbie friendly - if you know your way around Android you can do it much faster (Terminal and just edit the file). If you are using **Windows** please use *decent program to edit files* (like: ***Notepad++***, not Wordpad/Word).
In theory this should NOT crash your phone/ROM, but there is plenty of strange ROMs... so backup. Create a ***backup***, always.

***WARNING!***

***RUNNING ADB OVER TCP IS INSECURE, EVERYONE CAN ACCESS YOUR PHONE AND DO WHATEVER THEY WANT WITH IT. DO NOT DO IT IN PUBLIC NETWORKS. DO NOT RUN IT ON YOUR NORMAL PHONES***

## What do I need?
- Working USB cable
- adb on your PC and debugging enabled
- ***THIS FILE IS UNIQUE PER DEVICE, NEVER RE-USE IT FOR OTHER DEVICES, ALWAYS DOWNLOAD NEW ONE***

### Steps
1. Connect your phone via USB.
2. Open terminal/cmd.exe and type
``` adb devices ``` to make sure that your device is showing up.
3. Get a *build.prop* file from your device to your current directory
```
adb pull /system/build.prop
```
4. Open freshly downloaded *build.prop* with ***decent*** text editor.
5. At the end of file addd:
```
# MAD
# Disable ADB icon in notifciations area
persist.adb.notify=0
# Enable ADB over TCP on default port 5555
service.adb.tcp.port=5555
```
6. Push changed file to /sdcard/.
```
adb push build.prop /sdcard/
```
7. Mount /system/ and writable.
```
adb shell su -c 'mount -o rw,remount /system'
````
8. copy file from /sdcard/ to /system/.
```
adb shell su -c 'cp /sdcard/build.prop /system/build.prop'
```
9. Mount back /system/ as read-only.
```
adb shell su -c 'mount -o ro,remount /system'
````
10. Reboot device :)

