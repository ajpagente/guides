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
`-n` suppresses standard output as sed will display the contents of the file as well as the result of the sed command.\
`p` is the print command.\
The example prints the first 5 lines of the file
```
sed -n '1,5 p' /etc/passwd
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
