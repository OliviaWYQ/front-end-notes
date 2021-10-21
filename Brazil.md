# Brazil notes

## make brazil faster

You can use something like this to create a Ram Disk.

After that you can create build and env directories on the Ram Disk (In my case /Volumes/Build RAM Disk/) I created a 2GB Ram Disk as I only have 8GB Ram on my mac, you could create a bigger one depending on how much Ram you have.
```
mkdir /Volumes/Build\ RAM\ Disk/build
mkdir /Volumes/Build\ RAM\ Disk/env
```
Then in your workspace remove the build directories and create symlinks to the build directories on the Ram Disk
```
rm -rf build env
ln -s /Volumes/Build\ RAM\ Disk/env env
ln -s /Volumes/Build\ RAM\ Disk/build build
```
After this your builds will be much faster and your system should no longer hang during builds. If this works for you then writing a shell script that attaches your current workspace to the Ram Disk should be trivial.

## brazil error

1.error message: system(axle-platform-build): failed to run                           
               *** Be sure to declare a build-tool dependency on the package that               
  *** defines the 'axle-platform-build' command, and that the command is marked as executable.  
             Failed to run command: 'axle-platform-build' with arguments 'clean'

Todo: 
```
brazil ws sync --md
```

2.error message: SEVERE com.amazon.brazil.pkgcacher.CachingException: [UNKNOWN_ERROR] Error occurred while caching AL2_x86_64-NodeJS-8.x.319784.0-Catalog. DiskSpaceLimitException: Disk Usage is above 95%. Caching failed with /Users/yiqiawan/brazil-pkg-cache/tmp/download9033165582557653018/Catalog.
 Please see https://builderhub.corp.amazon.com/docs/brazil/user-guide/howto-package-cache-cleanup.html to clean up your disk.

Todo:
```
brazil-package-cache clean

brazil-package-cache clean --days 0 --keepCacheHours 0

brazil-package-cache stop && \
mv ~/brazil-pkg-cache ~/brazil-pkg-cache-old && \
rm -rf ~/brazil-pkg-cache-old &

if still no work:
sudo rm -rf /local/brazil-pkg-cache
sudo rm -rf ~/brazil-pkg-cache
sudo rm -rf ~/brazil-pkg-cache-old

if still no work:
toolbox uninstall brazilcli
toolbox install brazilcli

if still no work:
brazil prefs --global --key packagecache.edgeCache --value auto
brazil-package-cache stop && brazil-package-cache start

if the problem comes from mac system:
Write 20gb of data from /dev/random to a file in /tmp. This forces macOS to start purging unused capacity.
sudo dd if=/dev/urandom of=/tmp/target-file bs=100m count=200
```

3.brazil stuck on:[NodeJS-8.x/runtime] Building symlink farm of 8 packages from package cache
2021-10-20 00:55:53 INFO [NodeJS-8.x/runtime] Caching runtime components of dependencies

Todo:
```
toolbox update brazilcli
brazil prefs --global --key packagecache.edgeCache --value auto
brazil-package-cache stop && brazil-package-cache start --debug
```

4.brazil error: WARNING Lost connection to package cache daemon. Retrying request.
```
brazil-package-cache enable_edge_cache
```

## alias

alias bb="brazil-build"

alias bws="brazil ws"

alias bbr="brazil-build release"

alias abb='brazil ws clean; brazil-recursive-cmd --allPackages brazil-build release'

bb fix do both format-fix and lint-fix

## rebuild all packages
```
 brazil-recursive-cmd --allPackages brazil-build
```

## permission
```
kinit -f && mwinit -o
```

## Add local package to node_modules
```
npm install --save ../path/to/mymodule
```

## What to do when brazil-build fails

First try to sync the latest content for all packages
```
brazil ws sync
brazil ws sync --md
```
if it still fails, clean the workspace and build every package
```
brazil-recursive-cmd brazil-build clean
brazil ws clean
brazil ws sync
brazil ws sync --md
brazil-build clean
brazil-build release
```

## When Android configuring stucks on 0% and then fails

```
cat ~/brazil-pkg-cache/s3proxy.config
```
change this content into a proper one and save 

For example:
```
vim ~/brazil-pkg-cache/s3proxy.config
```
change the first line into
```
http://braziledgecache-cn-north-1.corp.amazon.com:6081
:wq
```
restart brazil package cache
```
brazil-package-cache stop
brazil-package-cache clean --days 0 --keepCacheHours 0 
brazil-package-cache start
```
```
brazil-package-cache stop && brazil-package-cache start --debug
```
```
brazil-package-cache disable_edge_cache
brazil-package-cache enable_edge_cache
```

## Instruction for enabling BrazilCDN

0. Ensure you are using BrazilCLI version 2.0.202844.0 or higher. For older versions, please update your BrazilCLI using instructions here.
```
brazil --version
```
1. Opt in BrazilCDN by setting up the BrazilCLI preference:
```
brazil prefs --global --key packagecache.useBrazilCdn --value true
```
2. As BrazilCDN doesn't require usage of edge caches,  run following commands to ensure edge caches are not enabled:
```
brazil prefs --global --key packagecache.disableEdgeCache --value true
brazil prefs --global --key packagecache.edgeCache --delete --force
```
3. Refresh your Midway token (if you haven't done so already):
```
mwinit
```
4. Restart brazil package cache daemon:
```
brazil-package-cache stop && brazil-package-cache start
```

## When a single package always fails

delete it and download a new one
```
cd <path-to-src>
rm -rf <package-name>
brazil ws use -p <package-name>
```

## Debug mode

```
cd <path-to-AxleReactNative>
brazil-build start

cd <path-to-package>
brazil-build server-axle
```

## dyld: Library not loaded: /usr/local/opt/icu4c/lib/libicui18n.67.dylib

```
brew upgrade

brew cleanup

```

