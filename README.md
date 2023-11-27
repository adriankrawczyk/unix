Awk
```
# The `-F` option allows you to choose the separator. The default separator is a space.
# For example, in the /etc/passwd file, the structure looks something like this:
# specu:x:1000:1000:Dawid Focht,,,:/home/specu:/bin/bash
# Here, the separator is a colon.
# Sample task - print all usernames with UID greater than 100
cat /etc/passwd | awk -F: '{if($3 > 100) print $1}'
```
Ls
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
Find
```
# File search utility. Extensive, check the documentation for specific parameters and syntax.
# If not explicitly stated to search recursively (including subdirectories), it's easier to use ls.

```
Wc
```
# Counts lines, characters, words, and more (in the output).
```
Sort
```
# Sorts the output.
```
Uniq
```
# Removes duplicate lines (usually needs to be sorted first).
```
Head -nx
```
# Displays the first x lines. Using a negative number displays all except the last x lines.
# CAUTION! -1 displays all, and -2 displays all except the last one.

```
Tail -nx
```
# Same as head, but counts from the end.
```
Ps
```
# Displays information about processes.
```
Grep x
```
# One of the most important commands. Filters output based on the pattern x.
```
Protips
```
# Searching in the manual: type ?, then the searched phrase.
# Use n and shift+n to navigate between search results.
# The $$ variable stores the PID of the current terminal.

```
### Unix info
<a href="doc:introduction" target="_blank">Introduction</a>
man
```
man 5 etc/passwd
```
/etc/passwd
```
# 1. Username (Login name): This is the name used by the system for user login. It must be unique on the system.
# 2. Password (Encrypted or Placeholder): Traditionally, the password used to be stored in this field. However, for security reasons, modern systems store an 'x' character here, and #the actual password information is stored in the /etc/shadow file.
# 3. User ID (UID): A unique numerical identifier assigned to each user. The root user typically has a UID of 0.
# 4. Group ID (GID): The primary group identifier for the user. It corresponds to the group specified in /etc/group.
# 5. User Info (GECOS): This field traditionally contains additional information about the user, such as the user's full name, phone number, etc.
# 6. Home Directory: The absolute path to the user's home directory, where they are placed after logging in.
# 7. Login Shell: The absolute path to the user's default shell, which is started upon login.
```
/etc/group
```
# 1. Group Name: The name of the group, which must be unique.
# 2. Password (Encrypted or Placeholder): Similar to /etc/passwd, this field traditionally held the group password. It is rarely used today and often contains an 'x'.
# 3. Group ID (GID): A unique numerical identifier assigned to the group.
# 4. Group Members: A comma-separated list of usernames that are members of the group.
```


