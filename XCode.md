## IOS App
```
cd AxleApp
brazil ws use -p AxleIOS --latest
cd src/AxleIOS
touch Dev.xcconfig
brazil-build xcode-env
rm Podfile.lock
brazil-build release
open AxleIOS.xcworkspace
```

## Ruby settings

### /lib64/ld-linux-x86-64.so.2: No such file or directory

```
toolbox update

brazil setup platform-support

brazil prefs

brew uninstall --ignore-dependencies ruby-build

brew install ruby-build

ruby-build --version

brew install rbenv libyaml libffi

brazil prefs --delete --global --key cli.bin.ruby27
brazil prefs --delete --global --key cli.bin.ruby25
brazil prefs --delete --global --key cli.bin.ruby24
brazil prefs --delete --global --key cli.bin.ruby23
brazil prefs --delete --global --key cli.bin.ruby21
brazil prefs --delete --global --key cli.bin.ruby19

ruby-build 2.7.2 ~/.runtimes/Ruby27x
ruby-build 2.5.7 ~/.runtimes/Ruby25x
ruby-build 2.4.9 ~/.runtimes/Ruby24x
ruby-build 2.3.8 ~/.runtimes/Ruby23x
ruby-build 2.1.8 ~/.runtimes/Ruby21x
ruby-build 1.9.3-p551 ~/.runtimes/Ruby19
```

### You have no preference setting for Ruby 2.3.
```
brew install rbenv ruby-build

which ruby

brazil setup --ruby

paste the path (mine's /usr/bin/ruby)
```


## Testing failure

Testing failed:
	Missing required module 'MobileCryptoiOS'
	Testing cancelled because the build failed.

Product -> Clean (keyboard shortcut ⌘-⇧-K)
Clean your app project, rebuild, and your app will run on the iDevice!


## IOS simulator

press control+command+Z


## IOS Accessibility

Test by accessibility inspector

    1. Open Xcode -> Open Developer Tool -> Accessibility Inspector.

    2. Go to System Preferences -> Sevurity & Privacy -> Allow Accessibility Inspector to control your computer.

    3. Open Accessibility Inspector and select the specific device: Simulator - iPhone 8.

    4. Select Accessibility Inspector -> Inspection -> Enable Point to Inspect.

    5. Then it can read the content inside the simulator

