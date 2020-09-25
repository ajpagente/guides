# grep
grep allows you to search output or files.

## Enabling color
Enable color to easily see matching words
```
grep --color=auto <additional parameters>
```

## Searching for string in files
Search for "pam_login" in all files in _/etc/pam.d_ directory
```
grep pam_login /etc/pam.d/*
```

## Using regular expressions
The regular expression filters a line starting with lowercase a to z or an underscore.
```
grep '^[a-z_]' <additional parameters>
```

## Useful parameters
* `-i` for case-insensitive search
* `-v` for inverse match wherein non-matching lines is shown
* `-c` count occurences
* `-A` specifies how many lines after the match we want to include. Example, `-A2` means 2 lines
* `-B` specifies how many lines before the match we want to include
* `-C` specifies how many lines before and after the match we want to include


# sed
## Commands
### Print
`p` will print the pattern space (matched lines)\
* __Suppressing standard output__
`-n` suppresses standard output as sed will display the contents of the file as well as the result of the sed command\
__Example__
```
sed -n 'p' /etc/passwd
```

* __Specifying a range__
Adding a range will only print matched lines
__Example__: Prints the first 5 lines of the file
```
sed -n '1,5 p' /etc/passwd
```
__Example__: Prints the the 5th line until the end of the file
```
sed -n '5,$ p' /etc/passwd
```
* __Specifying regular expressions__
__Example__: Display lines beginning with _root_
```
sed -n '/^root/ p' /etc/passwd
```

### Substitute
The substitute command is your searech and replace tool\
The first character following the `s` represents the delimiters, often the `/` is used\
The format is `sed '[range] s/<string>/<replacement>/' <file>`\
Only the first occurrence in the of the string is replaced. To perform a global replace, add the `g` option\
__Example__: Replace the beginning of line 6-9 with 4 spaces. Perform a global replace.
```
sed '6,9 s/^/    /g' file.sh
```
__Example__: For all lines that begins with "gret", replace "/bin/bash" with "/bin/sh". The delimiter is `@`, print the result to stdout.
```
sed -n '/^gret/ s@/bin/bash@/bin/sh@p' /etc/passwd
```

### Append, Insert, Delete
* __Append__ a new line after a line: `a`
```
sed '/^server 3/ a server ntp.example.com' /etc/ntp.conf
```
* __Insert__ a new line before a line: `i`
```
sed '/^server 0/ i server ntp.example.com' /etc/ntp.conf
```
* __Delete__ lines: `d`
Delete line beginning with "server 0.ubuntu" to "server 9.ubuntu". `\s` stands for a single whitespace. `\.` escapes the dot character.
```
sed '/^server\s[0-9]\.ubuntu/ d' /etc/ntp.conf
```

### Multiple sed expressions
* Multiple expressions can be written on the command line by including brace brackets within the quoted sed instructions\
```
sed '{
/^server 0/ i ntp.example.com
/^server\s[0-9]\.ubuntu/ d
}' /etc/ntp.conf
```
* For code reuse implement sed files
The sed file can be referenced with the `-f` option
```
cat ntp.sed
/^server 0/ i ntp.example.com
/^server\s[0-9]\.ubuntu/ d

sed -f ntp.sed /etc/ntp.conf
```

## Using regular expressions
```
sed -n '/^user/ p' /etc/passwd
```

## Deleting lines based on regular expressions
`^#` means lines beginning with `#`\
`^$` means empty lines\
`d` is the delete command
```
sed '/^#/ d ; /^$/ d' /etc/ntp.conf
```

## Inline editing
sed does not edit the file by default. To edit the file use `-i`.
To created a backup before editing, use `-i.bak` which created a backup file named <file>.bak
```
sed -i.bak '/^#/ d ; /^$/ d' /etc/ntp.conf
```
  
# awk
## Basic structure
The basic structure of awk is `awk '{<command>}' <file>`\
The example prints the file content
```
awk '{print}' /etc/passwd
```

## Programming with awk
### Example 1
`BEGIN` marks the start of the program\
`END` marks the end of the program\
`print "passwd"` prints _passwd_\
`print` prints the file content\
`print NR` prints the number of lines
```
awk 'BEGIN {print "passwd"} {print} END {print NR}' /etc/passwd
```

### Example 2
`print NR, $0` prints the line number then the line. `NR` is a counter that increments on each line in the file.
```
awk 'BEGIN {print "passwd"} {print NR, $0} END {print NR}' /etc/passwd
```

### Example 3
Say `ifconfig` returns `eth0  Link encap:Ethernet  HWaddr 00:0C:29:17:1B:27`\
We want to get the hardware address without the `:` separator\
`-F":"` indicates a colon separator\
`/Hwaddr/` regex that filters only line with `Hwaddr`\
`print $3 $4 $5 $6 $7` displays the 3rd to 7th item after the nth colon which in this case prints `0C29171B27`\
`$1` is `eth0  Link encap`\
`$2` is `Ethernet  HWaddr 00`
```
ifconfig eth0 | awk -F":" '/Hwaddr/{print $3 $4 $5 $6 $7}'
```
