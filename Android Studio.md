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
Install NDK to match the version
