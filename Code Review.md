# Code review notes

## Publish and update code review
create a new code review
```
cd <path-to-package>
cr
```
update
```
cd <path-to-package>
cr -r <CR-id>
```
update with different packages
```
cd <path-to-src>
cr -r <CR-id> -i <package-1> -i <package-2>
```

## How to Merge
need the rebase and wait, when the dry run passes, select "Overide and Merge", only for the packages you have permission to merge

## Put code with different versionset in separate cr
