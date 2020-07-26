# Mercurial

## Merging
### Merge two branches
Say you want to merge `develop` branch to `default` branch.

```
1) hg update default
2) hg merge develop
3) hg commit -m "Insert commit message here"
4) hg push
```
1. You need to be in the target branch (ie. the destination branch) when merging. 
2. Perform the merge operation
3. Commit the merge
4. Push to remote repository

## Miscellaneous
### Bypassing certificate checks
It is not recommended to bypass certificate checks. This method should not be used if you are able to check the repository certificate.
Say you want to clone without checking certificate using the `--insecure` option: `hg clone https:\<repo goes here> --insecure`
