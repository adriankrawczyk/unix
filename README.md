### awk
```
# The -F option allows you to choose the separator. The default separator is a space.
# For example, in the /etc/passwd file, the structure looks something like this:
# specu:x:1000:1000:Dawid Focht,,,:/home/specu:/bin/bash
# Here, the separator is a colon.
# Sample task - print all usernames with UID greater than 100
cat /etc/passwd | awk -F: '{if($3 > 100) print $1}'
```
### ls
```
# Basic command. Use only if specified that subdirectories do not need to be searched.
# Parameters:
# -l - the most important parameter, displays details of files in the directory in a list format.
# -a - displays all files, including hidden ones (starting with a dot). Note: also displays . and ..
# -A - same as above, but does not display . and ..
# -s - also shows the block count
# -i - displays the inode number
# -d - displays inode numbers for all listed files
# Image explaining the structure of the ls output

```
### find
```
# File search utility. Extensive, check the documentation for specific parameters and syntax.
# If not explicitly stated to search recursively (including subdirectories), it's easier to use ls.

```
### wc
```
# Counts lines, characters, words, and more (in the output).
```
### sort
```
# Sorts the output.
```
### uniq
```
# Removes duplicate lines (usually needs to be sorted first).
```
### head -nx
```
# Displays the first x lines. Using a negative number displays all except the last x lines.
# CAUTION! -1 displays all, and -2 displays all except the last one.

```
### tail -nx
```
# Same as head, but counts from the end.
```
### ps
```
# Displays information about processes.
```
### grep x
```
# One of the most important commands. Filters output based on the pattern x.
```
### Protips
```
# Searching in the manual: type ?, then the searched phrase.
# Use n and shift+n to navigate between search results.
# The $$ variable stores the PID of the current terminal.

```
### Unix info
```
[Unix One-Liners](https://git.iiet.pl/1-rok/UNIXy/blob/master/one_liners.md)
```

