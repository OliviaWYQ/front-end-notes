# Brazil notes

## What to do when brazil-build fail

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

## When Android configuration stuck on 0% and then fail

```
cat ~/brazil-pkg-cache/s3proxy.config
```
change this content into a proper one, save and restart brazil package cache
```
brazil-package-cache stop
brazil-package-cache start
```

## When a single package always fails

delete it and download a new one
```
cd <path-to-src>
rm -rf <package-name>
brazil ws use -p <package-name>
```

