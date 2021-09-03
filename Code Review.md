# Code review notes

## Guide

1. random hooks cause crash
2. avoid duplicate functions, and reuse components
3. remember to add detail comments and remove commented lines, update comments, and add comments for all exported items
4. use React.FC instead of a function, and pass props
5. use proper name with detail description
6. avoid exporting unnesscessary function or const
7. use const instead of let if possible
8. avoid global const, use state instead, or it goes out of React updates
9. use switch-case for handling multiple returns
10. not use 'else' in if-else
11. remove exported if not used in other files

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
