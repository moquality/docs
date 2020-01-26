# Downloading and Running Tests

Once you have uploaded the recorded test from your Android device, Barista will generate the test and send an email with a link to the test.

From the link, you can download the test in Java for multiple frameworks. Read the corresponding section below for running tests on the framework of your choice.

> **Pre-requisite:**  
>  UI Tests run on a physical android device or an emulator. Connect your device to the computer and make sure you can communicate to it via [adb](https://developer.android.com/studio/command-line/adb.html). Running `adb devices` on the command line should show your phone connected to the computer.

## 1. Espresso

The Espresso test framework is part of the Android testing support library that allows testing single apps. The tests run as an instrumentation test and have access to the app's internals.

* You will first need to set up Espresso for your app's project -- [Follow this tutorial](https://developer.android.com/training/testing/ui-testing/espresso-testing.html). 

  You can refer to the [BasicSample for Espresso source code on GitHub](https://github.com/googlesamples/android-testing/tree/master/ui/espresso/BasicSample) for sample Espresso setup.

* Then, you need to move the test to the `androidTest` folder inside your app. 
* Barista comes with a library that extends Espresso's functionality in allowing you to select elements using additional selectors like XPath, helping take screenshots etc. You will need to download and copy our crema library jar file in the `lib` folder of your Android app. You can then add crema dependency in your app's gradle file to load up the library.

  Download crema from [https://github.com/moquality/crema/releases](https://github.com/moquality/crema/releases)

  The resulting `app/build.gradle` should look like this:

  ```text
  dependencies {
   // Other app dependencies ...

   // Espresso test dependencies
   androidTestCompile 'com.android.support.test:runner:0.5'
   androidTestCompile 'com.android.support.test.espresso:espresso-core:2.2.2'
   androidTestCompile files('libs/crema-1.0.jar')
  }
  ```

* You can run the test from within Android Studio or from gradle by running `./gradlew connectedCheck`

### More info:

* [Official Espresso Reference](https://developer.android.com/training/testing/ui-testing/espresso-testing.html)

## 2. UIAutomator

The UIAutomator framework is also part of the Android testing support library, but also allows testing multiple apps. The tradeoff is that it is slower than Espresso but allows for blackbox testing of the app.

* You will first need to setup UIAutomator for your app's project -- [Follow this tutorial](https://developer.android.com/training/testing/ui-testing/uiautomator-testing.html).

  You can refer to the [BasicSample for UIAutomator source code on GitHub](https://github.com/googlesamples/android-testing/tree/master/ui/uiautomator/BasicSample) for sample UIAutomator setup.

* Paste the test inside the app's `androidTest` folder
* You can run the test from within Android Studio or from gradle by running `./gradlew connectedCheck`

### More info:

* [Official UIAutomator Reference](https://developer.android.com/training/testing/ui-testing/uiautomator-testing.html)

## 3. Appium

Appium is an open source test framework built using the WebDriver protocol. So, just like Selenium, you can write tests in any language with a WebDriver client.

* Appium tests run on your computer and not on the phone. You can install appium using nodejs like:

  ```text
  npm install -g appium
  ```

* To start the appium server, simply run the installed binary.

  ```text
  appium
  ```

* Get the appium java-client and run your test
  * If using Maven or Gradle:
    * Follow [these instructions on the java-client wiki](https://github.com/appium/java-client/blob/master/docs/Installing-the-project.md).
    * Run the test using the build system
  * For command line, use these instructions:
    * First download [all dependencies of java-client](https://jar-download.com/?detail_search=g%3A%22io.appium%22&g=io.appium) or simply build a farJar using instructions in [this PR](https://github.com/appium/java-client/pull/560)\).
    * Compile the generated Appium test in Java against the [Appium java-client](https://github.com/appium/java-client) and [JUnit](http://junit.org/junit4/).

      ```text
      # Unix, Mac OSX
      javac -cp .:lib/java-client-5.0.0-BETA1-all.jar MyTest.java
      ```

      ```text
      # Windows
      javac -cp ".;lib/java-client-5.0.0-BETA1-all.jar" MyTest.java
      ```

    * Run the java test by running this file.

      ```text
      # Unix, Mac OSX
      java -cp .:lib/java-client-5.0.0-BETA1-all.jar MyTest
      ```

      ```text
      # Windows
      java -cp ".;lib/java-client-5.0.0-BETA1-all.jar" MyTest
      ```

### Appium References:

* [Official Appium-Java Tutorial](https://appium.io/slate/en/tutorial/android.html?java#)
* Refer to [Appium test samples in Java](https://github.com/appium/sample-code/tree/master/sample-code/examples/java/)
* Appium's [Java-Client Wiki](https://github.com/appium/java-client/wiki) also has some tutorials

