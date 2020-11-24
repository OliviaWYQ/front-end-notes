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

    Open Xcode -> Open Developer Tool -> Accessibility Inspector.

    Go to System Preferences -> Sevurity & Privacy -> Allow Accessibility Inspector to control your computer.

    Open Accessibility Inspector and select the specific device: Simulator - iPhone 8.

    Select Accessibility Inspector -> Inspection -> Enable Point to Inspect.

    Then It can read the content inside the simulator
