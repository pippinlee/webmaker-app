# Developing on Android

## Install Android Debug Bridge (ADB)


<iframe width="775" height="436" src="https://www.youtube.com/embed/-d28E21PuRc" frameborder="0" allowfullscreen></iframe>

For this project you will need the SDK command line tools. You can download and install from [developer.android.com](https://developer.android.com/sdk/index.html) or via brew:

```bash
brew install android-platform-tools
```

Depending on where you have installed it, you may need to add the following to your .bash_profile:  (`ANDROID_HOME` should refer to wherever you installed the SDK)

```bash
export ANDROID_HOME=~/Library/Android/sdk
export PATH=${PATH}:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
```

Open a new window and type:
```
adb version
```
If you see something like `Android Debug Bridge version 1.0.32` you have adb installed properly. If you don't, see [this page on MDN](https://developer.mozilla.org/en-US/Firefox_OS/Debugging/Installing_ADB) for more help.

## Install Android 19 (4.4) SDK platform

<iframe width="775" height="436" src="https://www.youtube.com/embed/10XXnYteAqA" frameborder="0" allowfullscreen></iframe>

We'll also need to download the Android 19. To do this we'll download the SDK manager from [developer.android.com](https://developer.android.com/sdk/index.html).

You'll also need to make sure Java and Java Development Kit are install in order to run the `Android` command.


## Turn on remote debugging on your device

<iframe width="775" height="436" src="https://www.youtube.com/embed/idRdI2iN2Ek" frameborder="0" allowfullscreen></iframe>

- Enable USB debugging on your phone. ([Check out this guide](http://www.phonearena.com/news/How-to-enable-USB-debugging-on-Android_id53909) if you need help)
- Plug it into your computer via USB and run `adb devices` to make sure your device is recognized

## Install Cordova

`npm install -g cordova`

## Set up Webmaker App

- clone [mozilla/webmaker-app](https://github.com/mozilla/webmaker-app)
- run `npm install` and then `gulp dev` to build/watch changes
- to be able to make changes in this app and be able to build a new version in Cordova, **you will also need to run `npm link`** in the root of this directory

## Remote debugging via Chrome dev tools (4.4 only)

<iframe width="775" height="436" src="https://www.youtube.com/embed/JM1y3hyUU1Q" frameborder="0" allowfullscreen></iframe>

One of the best ways to debug the Webmaker app is through Chrome's developer tools.


## Remote debugging via logcat (works on 4.2+)


<iframe width="775" height="436" src="https://www.youtube.com/embed/FfgT4XtLuq4" frameborder="0" allowfullscreen></iframe>




## Set up the Cordova Wrapper
- clone `mozilla/webmaker-app-cordova`
- `npm install`
- `npm start`

This should build your project for the first time and attempt to launch the app on your phone (assuming it is plugged in and available through `adb`)

In order to complete the link to your local copy of `mozilla/webmaker-app`, run the following command once in the root of this directory:

```
npm link webmaker
```

After you do that, all you need to do to re-build the app is run the following every time you make a change:

```
npm run android
```


## Other tips

### Android WebView Browser

You may also want to download [WebView Developer Browser](https://play.google.com/store/apps/details?id=com.webviewbrowser&hl=en) from the Google Play store so that you can quickly run the web version of webmaker-app. This is the browser Cordova uses on Android 4.2.

### Setting up an emulator profile for 4.2

If you don't have an Android device, you can test on an Android emulator for 4.2. First, run the following to check what targets are available:

```
android list targets
```

You will want to use `android-17`. Choose a name for your profile and run the following to create an avd:

```
android create avd -n myemulator -t android-17
```

Go ahead and use hardware defaults when it prompts you. Now, you can use your emulator when building and running webmaker app with the following commands:

```
cordova prepare
cordova run android --target myemulator
```

