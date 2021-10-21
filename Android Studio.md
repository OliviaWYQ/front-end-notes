## Android App
```
cd AxleApp
brazil ws use -p AxleAndroid --latest
cd src/AxleAndroid
brazil-build release
```

## Android Studio

### Could not initialize class org.jetbrains.kotlin.gradle.internal.KotlinSourceSetProviderImplKt
```
brazil-build wrapper
```

## Android simulator

press command+M

## Build Error

What went wrong:
Execution failed for task ':stripDebugDebugSymbols'.
No version of NDK matched the requested version 20.0.5594570. Versions available locally: 22.1.7171670

Todo:
Install older NDK android-ndk-r20b-darwin-x86_64.zip to match the version from https://github.com/android/ndk/wiki/Unsupported-Downloads
Extract the file inside folder /Users/yiqiawan/Library/Android/sdk/ndk named 20.0.5594570

## Gradle

go to "Build, Execution & Deployment → Gradle", select "Use local gradle distribution" and enter that same path in the "Gradle home" box instead and hit "Ok"

use gradle from:/Users/yiqiawan/AxleApp/env/GradleTrails-4.0/runtime
