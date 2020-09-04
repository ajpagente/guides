# All About Shells :shell:

## Bash
### Environment
* Check that you are using bash: `echo $BASH`
  * If you are running bash, you will get the path to bash
  
### Commands and Arguments
* The first word is a __command__
* Everything that follows the command is an __argument__
* An argument that starts with a dash is an __option__

### Getting Help
* Manual pages: `man`
  * Move down a page: `space`
  * Move back a page: `b`
  * Search: `/<word to search>`, repeat typing `/` to find the next occurrence
  * Exit: `q`

### File Management
* View file content (dumps file content): `cat <file>`
* View file content and allow browsing: `less <file>`
  * Move down a page: `space`
  * Move back a page: `b`
  * Search: `/<word to search>`, repeat typing `/` to find the next occurrence
  * Exit: `q`
* Initialize the terminal: `reset`
  * Use this for example if you `cat` a binary file and the terminal gets "confused"
* Find out the file type: `file <file>`
* Show the file types of all files in the current directory: `file *`
* Delete a file: `rm <file>`
* Rename file: `mv <file> <new filename>`
* Create multiple directories: `mkdir <directory 1> <directory 2>`
* Move file to a directory: `mv <file> <directory>`
* Delete a non-empty directory: `rm -r <directory>`
* Create a empty file: `touch <file>`
  * If the file exists, a new file is NOT created. Touch modifies the modification and access date.  
  
#### Opening File in macOS
* Open a file with the default GUI application for the file type: `open <file>`
* Open the current directory in Finder: `open .`
* Choose the application to open the file: `open -a Preview image.jpg`
* Open the directory in VSCode: `open -a 'Visual Studio Code' .`

#### About Filenames
* Filenames can contain just about anything
  * Except `/`
  * Hidden files start with a dot
* Case sensitivity
  * Linux filenames are case sensitive
  * macOS filenames are NOT case sensitive by default
* Extensions are optional
##### Filename Do's and Don'ts
* Use letters, numbers, `-` and `_`
  * If you want to be really safe, don't use uppercase letters
* Try to avoid using spaces
##### Quoting,Escaping,Completion
* __Backslash__ escapes a single character
* __Single quotes__ escapes all characters between them
* Don't use __double quotes__, for now...

#### Paths
* Absolute paths start with a `/`
* Relative paths is resolved relative to the current working directory

#### Copying Files
* List directory content recursively: `ls -R`
* Copy file in a directory to the current directory: `cp <directory>/<file> .`
* Copy and rename: `cp <file> <new filename>`
* Copy multiple files to a directory: `cp <file 1> <file 2> <directory>`
* Copy all files to a directory: `cp * <directory>`

#### Copying Directories
* Copy directory and all its contents: `cp -R <source directory> <destination directory>`
* Copy multiple directories and all its contents: `cp -R <source directory 1> <source directory 2> <destination directory>`
* [macOS] Adding a slash to a directory name ie. `cp -R <director>/ <destination directory>` only copies the directory contents

#### Moving Files
* Move files to another directory: `mv <file 1> <file 2> <destination directory>`
* Move directories to another directory: `mv <directory 1> <directory 2> <destination directory>`

#### Deleting Files
* Delete a file: `rm <file>`
* Delete all files in the current directory: `rm *`
* Delete empty directory: `rmdir <directory>`
* Recursively delete the directroy and all of its contents: `rm -r <directory>`

#### Safety switch `-i`
* `-i` prompts before overwriting or deleting a file
* Examples: `cp -i`,`mv -i`,`rm -i`

### Using Bash Effectively
#### Wildcards
* __Star__ `*` matches anything and nothing
  * List all files in the current directory: `ls *`
  * List all files that starts with `a`: `ls a*`
  * List all files that ends with `a`: `ls *a`
  * List all files with `at` in the filename: `ls *at*`
  * Move all text files ie. files with the extension `txt`: `mv *txt <destination directory>`
  * List all directories which starts with `D` (bash is case-sensituive) and ends with `s`: `ls -d D*s`
* __Question mark__ `?` matches 1 character
* __Square brackets__ `[]` matches one of the characters in between the opening and closing bracket
  * Example: `[acd_7]`
  * A _caret_ `^` reverses the meaning. 
    * Example `[^art]` matches any character except a,r,t
  * _Ranges_ example: `[a-z],[0-9],[A-C3-6]`

#### Brace Expansion
Brace expansion generates strings
Syntax: __pre{list,of,strings}post__
Examples:
```
touch {a,b,c}.txt => touch a.txt b.txt c.txt
mv file.{jpg,txt} dir => mv file.jpg file.txt dir

Using ranges:
touch {a..c}{1..3}.txt => touch a1.txt a2.txt a3.txt b1.txt (and so on)
```
:information_source: __Brace expansion comes before wildcard expansion__
```
mv *{txt,jpg} Documents => mv *txt *jpg Documents
mv filea?.{jpg,txt} Documents => mv filea?.jpg filea?.txt Documents
```
:memo: Use `echo` to try out brace and wildcard expansion
```
echo a{1..3}
echo D*
```
#### Output Redirection
* Save command output to a file with `>`
```
ls > out.txt
```
* Append command output to a file with `>>`
```
echo buy milk >> out.txt
```

#### Pipes
Allows to pass the output of one command to another command.
```
Sort the output of grep
grep 1978 film.tsv | sort 
```

#### Command Substitution
Replace a command with its output using `$()`
```
echo "hello $(whoami)"
echo "Buy milk" >> "notes$(date).txt"

Older form uses backticks
echo "hello `whoami`"
```
:memo: Use double quotes so output with spaces is taken a one string. This keeps command substitution intact.

#### Movement Keys
:memo: To use `Alt` enable _Use Option as Meta key_ in the Terminal Keyboard preferences
* `Ctrl-a` Start of line
* `Ctrl-e` End of line
* `Ctrl-f` or `Right arrow` Forward 1 character
* `Ctrl-b` or `Left arrow` Backward 1 character
* `Alt-f` or `Command-left` Forward 1 word
* `Alt-b` or `Command-right` Back 1 word

#### Deletion Keys
* `Ctrl-d` or `Del` Delete a character
* `Ctrl-h` or `Backspace` Delete a character backward
* `Alt-d` Delete a word
* `Ctrl-w` or `Alt-backspace` Delete a word backward
* `Ctrl-k` Delete the rest of the line
* `Ctrl-u` Delete from the start of the line

#### Miscellaneous Keys
* `Ctrl-c` Ends a running program
* `Ctrl-d` Exit bash, End `cat > x` 
* `up arrow` or `Ctrl-p` Previous line in history
* `down arrow` or `Ctrl-n` Next line in history
* `Ctrl-r` Search back in history

#### Search history with `Ctrl-r`
* After typing a keyword, keep pressing `Ctrl-r` to cycle through matching items
* Use `Ctrl-c` to exit the search
* To edit/use the command, press any arrow key to exit search

### Filtering and Processing Text
#### Editors
* __nano__
* __vi__
* __emacs__

#### Sorting with `sort`
* Sort the contents of a text file
```
sort <file>
```
* Sort based on the 2nd column. The column must be space separated.
The sorting is based on the ASCII value of the character.
```
sort -k2 <file>
```
* Sort numerically (assuming the reference column is a number)
```
sort -nk2 <file>
```
* Reverse sort
```
sort -rnk2 <file>
```
* Using `uniq` with sort
`uniq` filters out duplicate lines and has the option to count occurence with `-c`.
```
sort -k2 <file> | uniq -c
```

#### Head and Tail
* `head` shows the beginning of an output stream
```
List the directory content sorted by size and only display the first 10 lines of the output
ls -lS | head

To show the first 2 lines
ls -lS | head -n 2
```
* `tail` shows the end of an output stream
``
List the directory content reverse sorted by size and only display the last line of the output
ls -lrS | tail -n 1
```
* `tail` can be used to "follow" a file while it is being updated
```
tail -f auth.log
```

