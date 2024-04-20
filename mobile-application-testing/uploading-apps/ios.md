---
description: >-
  To get started, Scandium requires a .zip or .tar.gz file containing your
  compressed .app bundle.
---

# iOS

Scandium currently only supports iOS Simulator builds (**.app**). A simulator build can be run in the iOS Simulator with Xcode. AppStore distribution device builds (**.ipa**) are not currently supported.

## Finding your .app file

### Using Xcode

The easiest way to get the iOS Simulator build is to run and build your application in Xcode while targeting an iOS Simulator

Once the build is complete and the app is running in the simulator, you can locate the `.app` file by navigating to **Product** -> **Show Build Folder in Finder** -> **Products/Debug-iphonesimulator**

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption><p>Xcode - show build folder in finder</p></figcaption></figure>

### Using Xcode Command Line Tools

You can also generate the iOS Simulator build of your app by building it directly via the command line using `xcodebuild`.

**With .xcodeproj**

```shell
xcodebuild -project '{project_name}.xcodeproj' \
 -scheme '{scheme_name}' \
 -sdk iphonesimulator \
 -configuration Debug
```

**With .xcworkspace**

```shell
xcodebuild -workspace '{your_workspace_name}.xcworkspace' \
 -scheme '{scheme_name}' \ 
 -sdk iphonesimulator \
 -configuration Debug
```

The `app` file can then be found under

```
build/Debug-iphonesimulator/
```

## Compress your app file

Once you have located your `.app` file, Scandium requires it to be in a compressed `zip` or `tar.gz` file e.g.

```
zip -r {app name}.zip {app name}.app
```

## Troubleshooting

If you are having trouble running your uploaded iOS app on Scandium, we recommend trying to run the same app on a simulator provided by Apple in Xcode.

Once your simulator is launched, you can simply drag over the `app` into the simulator window.
