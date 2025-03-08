## How to Dumbify Your Android Smartphone

**Note:** This guide has been updated with tips from [@eridorFR](https://github.com/lingeringwillx/How-to-Dumbify-Your-Android-Smartphone/issues/4).

#### Warnings

1- **THERE IS A POTENTIAL OF BRICKING YOUR PHONE OR LOSING YOUR PERSONAL DATA HERE. FOLLOW THIS GUIDE AT YOUR OWN RISK.**

2- The Android ecosystem could change in the future in a way that would break the tools used in this guide, so I don't know if this guide will continue working in the long term.

#### Steps

1- Backup any data or media that you want to keep.

2- Download [ADB and Fastboot](https://developer.android.com/tools/releases/platform-tools).

3- Download and install LineageOS by following the guide for your [device](https://wiki.lineageos.org/devices).

4- Download and install [MindTheGapps](https://wiki.lineageos.org/gapps/). 

5- Enable developer options by going to *About phone* and clicking on *Build number* several times.

6- Go to System -> Developer Options and enable USB debugging and Rooted debugging

7- Uninstall Google Play, Google Search, and the web browser using adb:

```
adb shell pm uninstall -k --user 0 com.android.vending
adb shell pm uninstall -k --user 0 com.google.android.googlequicksearchbox
adb shell pm uninstall -k --user 0 org.lineageos.jelly
```

8- Disable the ability to create multiple users:

Create a text file named local.prop with the following content:

```
fw.show_multiuserui=0
fw.max_users=1
```

After that push the file to Android:

```
adb root
adb push local.prop data/local.prop
adb shell chmod 644 data/local.prop
```

Restart the phone for the changes to take effect.

9- Optional: If you want to make it harder to install any apps, you can disable the package installer:

```
adb root
adb shell pm disable com.android.packageinstaller/.PackageInstallerActivity
```

#### Installing Apps

You can install apps either by:

1- Temporarily re-installing the Play store:

```
adb shell cmd package install-existing com.android.vending
```

2- By Downloading and installing the [Aurura Store](https://f-droid.org/packages/com.aurora.store/) then uninstalling it once it's longer needed.

3- By using an alternative store or a mirror site such as F-Droid, ApkMirror, Uptodown, or APKPure.


#### Disadvantages of using this setup

This setup comes with a lot of disadvantages that you should be aware of:

1- It's possible to install time-consuming apps through sideloading.

2- You will inevitably come across a situation where you need to install a certain app but you won't be able to.

3- Some apps won't work with an unlocked bootloader (such as banking apps).

4- Good luck trying to explain to people why your phone doesn't have all the features and capabilities that people expect it to have.
