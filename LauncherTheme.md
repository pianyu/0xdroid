# Introduction #

0xLab improve the Launcher of Android. You may install many themes into system, pick up one theme then apply to Launcher to change look and feel.

A theme includes images of Folder Icon, Bottom Bar, Handler and Wallpaper. Of course, you may design your own theme and distribute it to another 0xdroid user.

# Select Theme #

0xLab prepared a [Christmas Theme](http://0xdroid.googlecode.com/files/Theme_Christmas.apk) for you. Lets use it for demonstration.

```
$ wget http://0xdroid.googlecode.com/files/Theme_Christmas.apk    # Download Theme
$ adb push Theme_Christmas.apk /system/app    # Install Theme
```
  * Click **Add Item** at BottomBar, choose **Theme Selector**
> ![![](http://lh4.ggpht.com/_tBgWxrFmN1c/SytOC0qhBdI/AAAAAAAAD-Q/DTJRCFXI-aI/s800/theme_howto_1.png)](http://lh4.ggpht.com/_tBgWxrFmN1c/SytOC0qhBdI/AAAAAAAAD-Q/DTJRCFXI-aI/s800/theme_howto_1.png)
  * Choose you theme, press **Apply**
> ![![](http://lh5.ggpht.com/_tBgWxrFmN1c/SytODLeFA3I/AAAAAAAAD-U/Thw-yknEJXM/s800/theme_howto_2.png)](http://lh5.ggpht.com/_tBgWxrFmN1c/SytODLeFA3I/AAAAAAAAD-U/Thw-yknEJXM/s800/theme_howto_2.png)
  * Restart Launcher to regenerate views of Launcher and wait for few seconds.
> ![![](http://lh3.ggpht.com/_tBgWxrFmN1c/SytODLNnBZI/AAAAAAAAD-Y/4c6g-8PLSAg/s800/theme_howto_3.png)](http://lh3.ggpht.com/_tBgWxrFmN1c/SytODLNnBZI/AAAAAAAAD-Y/4c6g-8PLSAg/s800/theme_howto_3.png)

  * This is original screenshot of 0xdroid.
> ![![](http://lh5.ggpht.com/_tBgWxrFmN1c/SytSB7fKEYI/AAAAAAAAD-w/l8-xbveD8jY/s800/0xdroid_0x3.png)](http://lh5.ggpht.com/_tBgWxrFmN1c/SytSB7fKEYI/AAAAAAAAD-w/l8-xbveD8jY/s800/0xdroid_0x3.png)

  * After you apply the Christmas theme, Merry Christmas!
> ![![](http://lh6.ggpht.com/_tBgWxrFmN1c/SytP9GtyRAI/AAAAAAAAD-k/4ubCqXRcvGY/s800/0xdroid_xmas_1.png)](http://lh6.ggpht.com/_tBgWxrFmN1c/SytP9GtyRAI/AAAAAAAAD-k/4ubCqXRcvGY/s800/0xdroid_xmas_1.png)

> ![![](http://lh3.ggpht.com/_tBgWxrFmN1c/SytP9OhHnPI/AAAAAAAAD-o/y8HF9E-PI7s/s800/0xdroid_xmas_2.png)](http://lh3.ggpht.com/_tBgWxrFmN1c/SytP9OhHnPI/AAAAAAAAD-o/y8HF9E-PI7s/s800/0xdroid_xmas_2.png)

# Design Theme #
If you are a art designer, you may create your own theme by editing Christmas theme.

  * Download the tarball and extract it.
```
$wget http://0xdroid.googlecode.com/files/theme_christmas.tar
$tar xvf theme_christmas.tar
```
  * Edit the name of theme
    * change **org.zeroxlab.theme.christmas** to any name you want
    * **DO NOT** remove **com.android.launcher.THEME**, it tells ThemeSelector "I am theme package"
```
<manifest
    xmlns:android="http://schemas.android.com/apk/res/android"
    package="org.zeroxlab.theme.chiristmas">

    <!-- This flag is needed for ThemeSelector -->
    <uses-permission android:name="com.android.launcher.THEME" />
</manifest>
```

  * change the package name at Android.mk from Theme\_Christmas to any name you want.
```
LOCAL_PACKAGE_NAME := Theme_Christmas
```

  * Change images under **res/drawable**
  * Rebuild this package and distribute it