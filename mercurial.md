# Mercurial

## Merging
### Merge two branches
Say you want to merge `develop` branch to `default` branch
1. First you need to be in default branch. To switch to default branch:
`hg update default`
2. Perform the merge operation: `hg merge develop`
3. Commit the merge: `hg commit -m "Insert commit message here"`
4. Push to remote repository: `hg push`

## Miscellaneous
### Bypassing certificate checks
It is not recommended to bypass certificate checks. This method is presented for reference and should not be used if you are able to check the repository certificate.
1. Say you want to clone without checking certificate: `hg clone https:\<repo goes here> --insecure`
