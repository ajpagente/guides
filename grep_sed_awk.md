# grep
## Enabling color
Enable color to easily see matching words
```
grep --color=auto <additional parameters>
```

## Using regular expressions
The regular expression filters a line starting with lowercase a to z or an underscore.
```
grep '^[a-z_]' <additional parameters>
```

# sed
## Display the first 5 lines of a file
`-n` suppresses standard output as sed will display the contents of the file as well as the result of the sed command. 
`p` is the print command. 
The example prints the first 5 lines of the file
```
sed -n '1,5 p' /etc/passwd
```

## Using regular expressions
```
sed -n '/^user/ p' /etc/passwd
```
