# Mercurial

## Files
### Adding a new file
```
1. hg add <file>
2. hg commit -m "Insert commit message here"
3. hg push
```
1. Track the file
2. Commit the tracking change
3. Push to repository

### Removing an existing file
For situations where in you have a tracked file and want to delete the file.
```
1. rm <file>
2. hg remove <file>
3. hg commit -m "Insert commit message here"
4. hg push
```
1. Delete the file. On `hg status`, there will be a `!` before the deleted file's name.
2. Untrack the file
4. Commit the tracking change
5. Push to repository

## Merge
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
4. Push to repository

## Branch
### Create a branch from another branch
```
1) hg update <parent branch>
2) hg branch <new branch>
```
1. Set the current branch to the parent branch (ie. the branch you want to branch from)
2. Create a new branch from the current branch

### Determine a branch's parent 
This method will also give you the changeset for the branch/tag.
```
hg log -r "parents(min(branch(<tag or branch)))"
```

## Versioning
### Create a tag
```
1) hg update <branch>
2) hg tag <tag name>
3) hg push
```
1. Set the current branch to the branch you want to tag.
2. Tag (Mercurial automatically commits the tag)
3. Push the tag to the repository

## Reverting Changes
### Remove untracked files
This method has been tested on MacOS.
```
hg status -un | xargs rm
```

## Logs
### View changes in a revision
To view the changes in the files in a revision.
The revision can be the short number or long number. A revision is presented in the format: `<short>:<long>`
```
hg log -p -r <revision>
```

## Miscellaneous
### Bypass certificate checks
It is not recommended to bypass certificate checks. This method should not be used if you are able to check the repository certificate.
Say you want to clone without checking certificate using the `--insecure` option: `hg clone https:\<repo goes here> --insecure`
