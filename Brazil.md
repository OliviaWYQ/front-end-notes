# Brazil notes

## What to do when brazil-build fail

First try
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
