## IOS App
```
cd AxleApp
brazil ws use -p AxleIOS --latest
cd src/AxleIOS
touch Dev.xcconfig
brazil-build xcode-env
brazil-build release
open AxleIOS.xcworkspace
```

## IOS simulator

press control+command+Z


## IOS Accessibility

Test by accessibility inspector

    1. Open Xcode -> Open Developer Tool -> Accessibility Inspector.

    2. Go to System Preferences -> Sevurity & Privacy -> Allow Accessibility Inspector to control your computer.

    3. Open Accessibility Inspector and select the specific device: Simulator - iPhone 8.

    4. Select Accessibility Inspector -> Inspection -> Enable Point to Inspect.

    5. Then It can read the content inside the simulator
