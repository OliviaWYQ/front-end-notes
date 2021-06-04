# Brazil notes

## alias

alias bb="brazil-build"

alias bws="brazil ws"

alias bbr="brazil-build release"

alias abb='brazil ws clean; brazil-recursive-cmd --allPackages brazil-build release'

bb fix do both format-fix and lint-fix


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


