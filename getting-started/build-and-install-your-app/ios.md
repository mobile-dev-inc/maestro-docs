# iOS

This all assumes you've got Xcode plus Simulator runtimes installed. If you haven't, and want to know how, we've made a video walkthrough:

{% embed url="https://www.youtube.com/watch?v=HX9vcw4Po1s" %}

## Building with Xcode

Maestro currently supports iOS Simulator builds (**.app**), AppStore distribution device builds (**.ipa**) are not currently supported. The easiest way to get an app installed on the simulator is by building and running it from Xcode (make sure that simulator target is selected):

<figure><img src="../../.gitbook/assets/Screenshot 2023-02-15 at 13.46.55.png" alt=""><figcaption></figcaption></figure>

## Default build location

If you want to install the .app manually, the file can be found under the Products folder at Xcode Menu:\
\
**Product -> Show Build Folder in Finder -> Then go to path Products/Debug-iphonesimulator**

The .app file can then be installed on the simulator by simple dragging and dropping the file or via Xcode command line tools by running:

```
xcrun simctl install $DEVICE_UDID /path/to/your/app
```

## Building with Xcode command line tools

To build an app with Xcode command line tools **xcrun xcodebuild** should be used. Here is an example on how to build [Food Truck](https://github.com/apple/sample-food-truck) app for iOS simulator target:

```
xcrun xcodebuild -scheme 'Food Truck' \
-project 'Food Truck.xcodeproj' \
-configuration Debug \
-sdk 'iphonesimulator' \
-destination 'generic/platform=iOS Simulator' \
-derivedDataPath \
build
```

The .app file can be then found under **/build** folder

## Building with Fastlane

If you use [fastlane](https://fastlane.tools/) for your automation pipelines the script should look the following way:

```
xcodebuild(
      configuration: build_config[:configuration],
      scheme: build_config[:scheme],
      workspace: build_config[:xcode_workspace],
      xcargs: "-quiet -sdk 'iphonesimulator' -destination 'generic/platform=iOS Simulator'",
      derivedDataPath: IOS_DERIVED_DATA_PATH # this will contain the .app which we need later on
)
```

## Building with Flutter

If you use Flutter to build your app you can create a debug build for simulators using the following command:

```
flutter build ios --debug --simulator
```

You can then find your app file in the `build/ios/iphonesimulator/` directory.

## Running on a Simulator

Once you've got your .app file, installing it should be as simple as dragging and dropping it onto the running Simulator.
