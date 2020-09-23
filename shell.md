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
* View file and show non-printing characters: `cat -vet <file>`
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
```
List the directory content reverse sorted by size and only display the last line of the output
ls -lrS | tail -n 1
```
* `tail` can be used to "follow" a file while it is being updated
```
tail -f auth.log
```

#### Count with `wc`
* Show number of lines, words, bytes in a file
```
wc <file>
```
* Show only the number of linesin a file
```
wc -l <file>
```

#### Searching for text with `grep`
* Find the lines with a certain word
```
grep <word> <file>
```
* Find all files with a certain word
```
grep <word> <wildcard + file name pattern>
```
* Case-insensitive search
```
grep -i <word> <wildcard + file name pattern>
```
* Filtering out lines
```
grep -v <filter> <file>
```
* `grep` supports regular expressions (regex)
```
Filter out empty lines
grep -v "^$" <file>
```
* Using extended regex to combine regex patterns
```
Filter out empty lines and lines with a certain pattern
grep -Ev "^$|<filter>" <file>
```
* Other options
  * `-c` counts occurence
  * `-l` shows line number of occurence

#### Searching for files with `find`
* Find files in a directory and all its subdirectory
```
find /usr
```
* Find a file with a certain name
```
find /usr -name <file name>
```
* Find with wildcard
```
find /usr -name '*txt'
```
* Find then execute a command on the found file
```
Find a txt file with the word "curious" and only show the file name
find . -name '*txt` -exec -l curious {} \;
```

#### Replacing characters with `tr`
`tr` does not accept filename as input. You have to use pipe.
* Replacing character
```
Replace uppercase S with lowercase s
cat <file> | tr S s
```
* Another way of redirection
```
Redirect file content to tr
tr S s < <file>
```
* Escaping from the command line
```
Search for semi-colon in a file. Semicolon splits commands in bash so it has to be escaped
grep \; <file>
```
* Replace all tabs with semicolon
```
\t means <tab>. Escape it so <tab> is passed to grep. The output of tr is redirected to a file.
tr \\t \; < <file> > <file>
```

#### Advanced Tools
* `sed`
  * Stream editor
  * Transform text
  * The most common use case is to replace words
  * `sed 's/old/new/g'`
* `awk`
  * Complete programming language
  * Very useful for column-oriented files
* __Perl__, __Python__, __Ruby__

#### Working with column-based text
The following commands can work with column-based text
* `sort`
`sort` assumes space delimiter by default
```
Sort numerically based on second column. Use semicolon delimiter.
sort -nk2 -t\; <file>
```
* `cut`
`cut` assumes tab delimiter by default
```
Cut out lines based on second column. Use semicolon delimiter.
cut -f 2 -d\; <file>
```
* `paste`
`paste` merges corresponding or subsequent lines of files
```
Paste together contents of files ending with "grades"
paste *grades
```
* `join`
`join` performs an ``equality join'' on the specified files and writes the result to the standard output
```
If the key is the same, join simply takes the key and shows the value from all files
join <file 1> <file 2>
```

### Jobs and Processes
#### Background Jobs
* To pause a command press `Ctrl-Z`
* To resume a paused command, type `fg` for foreground
* Send a paused command to the background by typing `bg` for background
* Run a command and send it to the background: `<command> &`. Make sure to put the ampersand at the end. Example if you want to redirect the command's output.

#### Killing Programs and Processes
* Kill foreground programs with `Ctrl-z`
* End any program with `kill`
  * Can only end processes you own
  * Kill by job ID: `kill %<job ID>`
  * Kill by command name: `kill %<command>`
* `bg` and `fg` also works with job ID. Example: `fg %<job ID>`
* List running jobs with `jobs`
* All running programs has a process ID
* Use `ps -e` with `grep` to find the process ID of a running program
* Kill by process ID: `kill <process ID>`
  * "hard" kill with `-KILL` as in `kill -KILL <process ID>`
* Use `xkill` to kill xWindow programs (Linux only). After typing `xkill` you will be prompted to choose the program to kill.
* Use `pkill <part of name>` to kill a program. Be careful as this command is very powerful.

#### Inspecting Processes
* Use `jobs` to list bash jobs for the current shell
* Use `ps` to list running processes
  * `ps` without any option on Linux displays processes running under the current shell
  * `ps` without any option on Mac displays all processes running on a terminal
  * `ps -e` displays all processes on Linux
  * `ps ax` displays all processes on Mac
  * `ps -ef` displays all processes including its owner on Linux
  * `ps aux` displays all processes including its owner on Mac
* `top` list all processes in real time. The most CPU intensive processes are shown on top.
  * On Linux:
    * `u` allows you to enter the process owner in order to filter the output
    * `k` allows you to enter the process ID to kill the process
    
### Customization
#### Aliases
* `alias` displays all set aliases
* To create an alias: `alias ls='ls --color=auto'` (colorize output in Linux) use `ls -GF` for Mac. `F` displays `/` for directories.
  * The above method only applies to the current shell session
* To run the original command use `\<command>`

#### Saving Customization
* `~/.bashrc` and `~/.profile` is present by default in Linux but not in Mac
* `.bashrc` is run when not in a non-login shell (ssh is a login shell)
* `.profile` is run on login shell
* Most people simply run one file from the other. Example in `.profile` add `source ~/.bashrc`
* MacOS Terminal.app runs bash as a login shell

#### Enviroment Variable
* Append to the path: `PATH="$PATH:<path to append>"`
  * To avoid overwriting or bypassing commands, always append your path to the end
* `PS1` is the environment variable for the shell prompt
* By default, `echo $PS1` is set to `\h:\W \u\$` in Mac
  * `\h` stands for host name
  * `\W` stands for current working directory
  * `\u` stands for current logged in user
* Example, append an environment variable to `.bashrc`
  * `echo 'PS1="\h:\W \u [\t] \$"'` >> ~/.bashrc
* `env` lists all environment variables
* When running for example `less`, pressing the `v` key opens the file in an editor. The default editor in Mac is `vim` if the `EDITOR` environment variable is not set.
* A variable is local to the shell. You can export it to make it available to the commands or programs started from bash. Use `export <VARIABLE NAME>`

#### Setting Your Default Shell
* Use `chsh` to change shell. You will be prompted with your password
  * In Linux, you will be prompted to enter the path to the binary of the new shell.
  * In Mac, a file will be opened in your default editor and you can change the Shell value










  








