# The Landscape of Mobile Testing Tools
* There is a whole slew of tools available to assist you in automating your mobile apps. Even though Appium is the most popular cross-platform mobile automation tool, it's good to have at least an overview of the other options out there.*

| Mobile Automation Tools |  |
| ----- | ---- |
| Appium | https://appium.io |
| XCUITest | https://developer.apple.com/videos/play/wwdc2019/413/ & https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/testing_with_xcode/chapters/09-ui_testing.html|
| Espresso | https://developer.android.com/training/testing/espresso |
| UiAutomator | https://developer.android.com/training/testing/other-components/ui-automator |
| Earl Grey | https://github.com/google/EarlGrey |
| Detox | https://github.com/wix/Detox |




Mobile automation is a bit newer than web automation in general, but there have still been a whole slew of mobile automation tools released in the last decade. Most of them are not around any longer, and so thankfully we don't need to cover them. Appium is by far the most generally applicable and popular mobile automation testing tool, but it is not the only one.

Just like we mentioned in the video on the landscape of web testing, choosing whether to use a given tool is a very context- and situation-dependent process. Just because Appium is the most popular doesn't mean it will work the best in every situation. So it's good to understand a bit of the lay of the land, and the advantages and disadvantages of each tool on offer.

First let's talk about XCUITest. XCUITest is a framework developed by Apple for the purpose of testing the UI of iOS apps. It only works on iOS, so it is not a cross-platform framework. When you write code for XCUITest tests, you write it in Objective-C or Swift, since those are the languages supported by Apple for iOS development. You typically write and run XCUITests inside of XCode, which is Apple's IDE for iOS development. Because Apple controls each piece of this equation, there is the possibility for some very nice integration between the IDE and the tests. There is a built in test runner, and it's relatively straightforward to build and compile your tests alongside the latest version of your app, since the test code and the app code live together in the same codebase.

XCUITest exposes an API that gives us access to basic UI automation primitives, like finding elements, tapping them, performing basic gestures on the screen, and so on.

The main advantages of XCUITest are that it is officially supported by Apple, and that it has great integration with Xcode. That's about it. There are some cloud test service vendors that support XCUITest, so if you write your tests in this framework, you will have the option of running your tests at scale on several platforms.

I should say one other thing about XCUITest so it's in your mind for later, which is that Appium actually uses XCUITest under the hood for Appium's own iOS automation support. So in a sense, XCUITest isn't really an alternative to Appium for iOS, though writing test code for XCUITest directly is very different than using it from within Appium. But more on that later!

Next let's discuss Espresso. Espresso is an automation library from Google, designed to work with Android applications. Like XCUITest, it is single-platform. Also like XCUITest, it is designed to work well inside Google's official Android IDE, called Android Studio. Espresso also gives us basic UI automation primitives, like finding views and performing actions on them. There are some more substantial differences between Espresso and XCUITest, however. First of all, Espresso tests must be written in either Java or Kotlin, because those are the languages that Google supports for Android development. Secondly, Espresso is built around a different method of UI testing. Tools like XCUITest, or even Appium, are often called "black-box" automation tools, because they force us as testers to think about the application as a "black box." We can't see inside it.

Now, an application is not actually a black box. A developer of the app has access to the source code which highlights all the internal components and moving parts inside the app. But these internal elements are not visible to users. Users interact with applications from a black-box perspective. To them, the app is all surface, and no interior. Many UI testing frameworks take the same approach. And why not, since this is also how users interact with the app?

Well, it turns out that by granting the test suite some access to the internal code methods or internal states of an application, you can sometimes make testing faster or more convenient. Test frameworks that provide access to application-internal methods or functionality are called "gray-box" frameworks. They can still interact with the app as a user would, by finding elements and tapping on things. But they can also do things a user could never do, like trigger a specific function inside the app by its name in the source code.

The designers of Espresso felt that by making it a gray-box framework, they could avoid some of the common bad habits or bad experiences that can sometimes accompany UI tests. For example, since Espresso tests run at least partially inside your app as the app is running, they know when your app is busy working on something. So if your test code tries to, say, find or tap on a button at that precise moment, Espresso can tell that test command to hold on for a moment, wait for the app to finish its own business, and then allow the test command to proceed. This makes life easier on you as the test author, since you don't have to worry about being sure that the app is in an appropriate state for you to interact with it.

One big drawback of this gray-box approach is that you can't attach to just any old app and test it in this way. Because the Espresso tests have access to the app source code, they must be run on an app whose source code you have. You can't download an app from the Play Store and run an Espresso test on it, the way you could with Appium or UiAutomator, which we'll talk about later. So Espresso has some pretty big advantages and disadvantages. The main advantages are that it is officially developed and supported by Google, that it has a tight integration with Android Studio for those already using it for app development, and that its gray-box approach opens up doors for faster, more stable, and more convenient tests.

Its main disadvantages are that it is single platform, must be written in one of 2 languages, requires tests to be bundled with the application source code to work, and can't automate anything outside of the application under test. That's it for Espresso, except to say that, like XCUITest, Appium also has the ability to use Espresso for Android testing under the hood.

Now let's turn to UiAutomator. In a sense, UiAutomator doesn't really need to be on this list. It's an older automation technology from Google. Google is now promoting and recommending that testers use Espresso. However, UiAutomator, with its current version of 2, is still a useful tool to know about. It has many of the same characteristics as Espresso. It's produced by Google, only works on Android, and is designed to be written with Java or Kotlin.

The main difference with UiAutomator is that it is a traditional black-box approach to UI testing. It doesn't know anything about your app, or how your app differs from other apps that you might have downloaded from the Play Store. UiAutomator is powered by the accessibility systems of the Android device, so all it knows about are UI elements and actions the user can take on the screen.

One other important aspect of UiAutomator 2 for our purposes in this course is that it is the technology which Appium uses under the hood for its standard Android support. What this means is that, even if you use Appium, you may be using UiAutomator 2 without knowing it. For this reason, it's good to know some of the facts we just shared about its capabilities even if you never use it directly.

Another popular automation technology, this time for iOS is called Earl Grey. It has a name which is thematically quite similar to Espresso, in terms of caffeinated beverages, and that's no accident! Both Espresso and Early Grey were developed by Google. Earl Grey is Google's attempt to bring a technology like Espresso to iOS.

Because of this, many of the features of Espresso that we discussed are also relevant to Earl Grey. Early Grey is an iOS framework that you bundle with your application tests, which provides an API very similar to Espresso's for finding and interacting with views. Given that it is built as an iOS framework, you write tests in a similar way as with XCUITest, that is to say inside Xcode using the XCTest test case classes.

The main benefits of Earl Grey are that, since it is bundled inside your application during test, it can provide the same stability and activity synchronization features as Espresso. Similarly, Earl Grey is quite fast, and because it is hosted within your application you also have access to your own app code, the way you would from a unit test! The main drawbacks are similar to Espresso as well--you can only write tests in Objective-C or Swift for one mobile platform, and you're limited to testing apps whose source code you have. Earl Grey is not a general automation tool, it's really only for testing your specific app. However, you could theoretically combine Earl Grey and XCUITest in the same tests, in order to have some of the benefits of both at the same time.

The last alternative mobile automation tool we'll look at is called Detox. Detox is the newest of all the frameworks we've discussed. It's designed to be especially useful in automating React Native apps, and in some ways is most closely related to the variety of JavaScript-based test frameworks we discussed in the landscape of web browser automation. Detox is a Node.js-based tool, and it requires that you write your tests in JavaScript.

Detox works by building a bridge to Earl Grey for iOS and to Espresso for Android. For this reason, Detox isn't a fundamental automation technology, and is similar to Appium in this way. Detox also has some nice boilerplate for integrating with your React Native app development and testing workflow.

Detox's main benefits are the same as the ones offered by Earl Grey and Espresso: the speed and stability that come from grey-box testing. And the limitations are more or less the same as well: you're forced to use just one programming language, and you're limited to testing apps whose source code you have, since the external frameworks need to be built in. Additionally, at this point Detox only supports simulators and emulators, not real physical devices.

The primary reason to use Detox would be if you're working on a React Native app and want all the tests as well as the app code to be in JavaScript. OK, that's it for Detox!

Of course, we need to say something about Appium! And we'll do that shortly, in a unit dedicated to going into Appium's features and benefits as well as drawbacks. But what we should learn right now is that Appium is really more of a philosophical approach to solving the problem of mobile app automation, rather than a fundamental automation technology. Don't get me wrong--there's an awful lot of code in Appium's codebase, and I wrote a lot of it myself! But the main job of Appium is to make other good automation technologies available in a usable package. As I've mentioned a few times in this unit, Appium actually uses technologies like XCUITest, Espresso, and UiAutomator 2 under the hood. So it doesn't strictly speaking compete with them on the level of automation technology. But hold on for a little bit, because we'll go into more detail about all of this soon.
