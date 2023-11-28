# One-linery

## pliki

### /etc

0. Ile jest osób w `/etc/passwd` o nazwisku Nowak?

    ```bash
     cat /etc/passwd | awk -F: '{print $5}' | grep -i 'nowak' | wc -l
    ```

0. Jaki jest najmniejszy numer grupy w systemie

    ```bash
     cat /etc/group | awk -F: '{print $3}' | sort -n | head -1
    ```

0. Jaki jest największy numer grupy w systemie

    ```bash
     cat /etc/group | awk -F: '{print $3}' | sort -nr | head -1
    ```

0. Podać ilość użytkowników o UID < 1000

    ```bash
     cat /etc/passwd | awk -F: '{if($3 < 1000) print "cokolwiek"}' | wc -l
    ```

0. Ile jest w systemie grup, które są grupą podstawową dla co najmniej jednego użytkownika?

    ```bash
     cat /etc/passwd | awk -F: '{print $4}' | sort | uniq | wc -l
    ```

0. Ile jest w systemie grup, które nie są grupą podstawową dla co najmniej jednego użytkownika?

    ```bash
     echo $((`cat /etc/group | wc -l` - `cat /etc/passwd | awk -F: '{print $4}' | sort -n | uniq | wc -l`))
    ```

0. Ile grup w systemie nie jest grupami dodatkowymi dla żadnego użytkownika?

    ```bash
     cat /etc/group | awk -F : '{print $4}' | grep ^$ | wc -l
    ```

0. Numer grupy podstawowej największej liczby użytkowników

    ```bash
     cat /etc/passwd | awk -F: '{ print $4 }' | sort -n | uniq -c | sort -nr | head -1 | awk '{ print $2 }'
    ```

0. Użytkownik o największym UID (wypisać to UID)

    ```bash
     cat /etc/passwd | awk -F: '{ print $3 }' | sort -nr | head -
    ```

0. Użytkownicy, których nazwa składa się z dokładnie 8 znaków.

    ```bash
     grep -cE -e '^[^:]{8}:' /etc/passwd
    ```

0. Zakładając, że w odpowiedniej kolumnie odpowiedniego pliku jest zdefiniowane imię i nazwisko użytkownika, znajdź ile jest osób o nazwisku Kowalski.

    ```bash
     cat /etc/passwd | awk -F: '{print $5}' | grep -i kowalski | wc -l
    ```

0. Podaj liczbę lokalnych użytkowników którzy nie mogą się zalogować (/sbin/nologin jako shell)

    ```bash
     cat /etc/passwd | awk -F: '{if($7=="/usr/sbin/nologin") print $7}' | wc -l
    ```

0. Podaj liczbę grup w systemie

    ```bash
     cat /etc/group | awk -F '{print $3}' | wc -l
    ```

0. Podać grupę o najwyższym numerze, która jest grupą podstawową dla przynajmniej jednego użytkownika

    ```bash
     cat /etc/passwd | awk -F '{print $3}' | sort -n | uniq | sort -nr | head -1
    ```

### inne

0. Podaj nazwę pliku w katalogu domowym o największym rozmiarze

    ```bash
    ls -al ~ | grep '^-' | awk '{print $5,$9}' | sort -n | tail -n1 | awk '{print $2}'
    ```

0. Podaj nazwę pliku w katalogu domowym o największej ilości bloków

    ```bash
     ls -als ~ | awk '{print $2,$1,$10}' | grep "^-" | awk '{print $2,$3}' | sort -nr | head -1 | awk '{print $2}'
    ```

0. Podaj ilość katalogów w podanym katalogu (bez katalogów) których nazwa zaczyna się na s

    ```bash
     ls -la $KATALOG | grep '^d' | awk '{print $9}' | grep '^s' | wc -l
    ```

0. Podaj polecenie, ktorym zmieni się uprawnienia katalogu `katalog` z `drwsr-xr-x` na `dr-xr-xr-t`

    ```bash
     chmod u-ws,o+t katalog # nie próbujcie cwaniakować z octalem, w niektórych implementacjach chmod nie resetuje SUID
    ```

0. Znajdź plik w swoim katalogu domowym, który był najdawniej modyfikowany.

    ```bash
     ls -lt ~ | grep '^\-' | tail -1 | awk '{print $9}'
    ```

0. Ile katalogów znajduje się w /usr/include?

    ```bash
     find /usr/include -type d | wc -l
    ```

0. Jaki jest inode (iwęzeł) katalogu domowego?

    ```bash
     ls -id ~ | awk '{print $1}'
    ```

0. Ile jest plików w /usr/include, wraz z podkatalogami, które mają w nazwie td i których nazwy kończą się na .h?

    ```bash
     find /usr/include -type f -name "*td*.h" | wc -l
    ```

0. Ile jest plików w /usr/include (bez podkatalogów), których nazwa składa się z 6 liter, zaczyna się na "m" i kończy na ".h"?

    ```bash
     find /usr/include/* -prune -name "m???.h" | wc -l
    ```

0. Ile plików regularnych jest w twoim katalogu domowym (wraz z podkatalogami)?

    ```bash
     find ~ -type f | wc -l
    ```

0. Ile jest plików w /usr/include, bez podkatalogów, które zaczynają się na `st` i których nazwy kończą się na `.h`?

    ```bash
     find /usr/include -maxdepth 1 -type f | awk -F/ '{print $4}' | grep '^st' | grep '.h$' | wc -l
    ```

0. Ile jest plików w /usr/include, bez podkatalogów, które mają w nazwie td i których nazwy kończą się na .h?

    ```bash
     find /usr/include -type f -maxdepth 1 -name "*td*.h" | wc -l
    ```

0. Podaj ile jest plików regularnych w katalogu /usr/include (do końca drzewa, czyli bierzmy pod uwagę pliki w podkatalogach), które mają rozmiar większy niż 12000B.

    ```bash
     find /usr/include -type f -exec ls -l {} \; | awk '{ if ($5>12000) print $0}' | wc -l
    ```

0. Znajdź liczbę plików regularnych w /usr/include (bez podkatalogów) które zaczynają sią na m i kończą na .h oraz których rozmiar nie przekracza 12KB.

    ```bash
     find /usr/include -maxdepth 1 -type f -name ”m*.h” -execls -l {} \ ; | awk '{if($5<12000) print $9}' | wc -l
    ```

0. Wypisać rozmiar największego pliku z $HOME (łącznie z podkatalogami i plikami ukrytymi).

    ```bash
     find ~ -type f -printf "%s \ n" | sort -nr | head -1
    ```

0. Podaj numer i-węzła opisującego /tmp

    ```bash
     ls -id /tmp | cut -d" " -f1
    ```

0. Podaj numer i-węzła katalogu domowego

    ```bash
     ls -id ~ | cut -d" " -f1
    ```

0. Podać liczbę plików w /usr/bin o wielkości do 1MB

    ```bash
     find /usr/bin -size -1M | wc -l
    ```

## procesy


0. Pidaj PID procesu zastopowanego, który zużywa najwięcej pamięci wirtualnej

    ```bash
     ps -eo s= -o vsz= -o pid= | grep "^[Tt]" | awk '{print $2,$3}' | sort -nr | head -1 | awk '{print $2}'
    ```

0. Podać nazwę użytkownika, który ma najwięcej procesów z zerowym NICE

    ```bash
     ps -eo %n%U | awk '{if($1=="0") print $1 " " $2}' | sort | uniq -c | sort -nr | head -1 | awk '{print $3}'
    ```

0. Podać ilość procesów, których rodzicem jest proces o numerze 1

    ```bash
     ps -eo %P | sort | awk '{if($1=="1") print $1}' | wc -l
    ```

0. Podać PIDy trzech procesów, które mają najwięcej pamięci wirtualnej

    ```bash
     ps -eo %z%p | sort -nr | head -3 | awk '{print $2}'
    ```

0. Napisać, ile razy od początku root zalogowal się do innych terminali (treść niepewna)

    ```bash
     last root | head -n-2 | wc -l
    ```

0. Ile jest procesów, których ojcem jest proces o PID 1?

    ```bash
     ps -el | awk '{print $5}' | grep ^1$ | wc -l
    ```

0. Znajdź użyszkodnika w systemie, który ma urchomioną największą liczbę procesów

    ```bash
     ps aux | tail -n+2 | awk '{print $1}' | sort | uniq -c | sort -nr | head -1 | awk '{print $2}'
    ```

0. Ile procesów w systemie ma parametr NICE większy od zera?

    ```bash
     ps -le | tail -n+2 | awk '{if ($8>0) print $0}' | wc -l
    ```

0. Ile jest procesów, które posiadają terminal?

    ```bash
     ps aux | tail -n+2 | awk '{if ($7!="?") print $0}' | wc -l
    ```

0. Ile procesów w całym systemie ma ujemną wartość parametru NICE? (W innych latach trafiała się wersja z dodatnią)

    ```bash
     ps -eo %n | awk '{if ($1<0) print $1}' | wc -l
    ```

0. Ile procesów potomnych ma bieżący interpreter poleceo? PID bieżącego interpretera poleceo: echo $$.

    ```bash
     ps -le | awk '{print $5}' | grep ^$$$ | wc -l
    ```

0. Liczba uśpionych procesów

    ```bash
     ps -el | tail -n +2 | awk '$2 == "S" { print $2; } ' | wc – l
    ```

0. PID procesu zajmującego najwięcej pamięci wirtualnej (VSZ)

    ```bash
     ps aux | tail -n +2 | awk '{ print $5" "$2 }' | sort -nr | head -1 | awk '{ print $2 }'
    ```

0. PID procesu zajmującego najwięcej pamięci rezydentnej 

    ```bash
     ps aux | awk '{print $5 " " $2}' | sort -nr | head -1 | awk '{print $2}'
    ```

0. PID procesu użytkownika root zajmującego najwięcej pamięci rezydentnej i nie ma terminala

    ```bash
     ps aux | awk '{if($1=="root") print $6 " " $7}' | awk '{if($2=="?") print $1}' | sort -nr | head -1
    ```

0. Znajdź proces, który zużył najwięcej czasu procesora

    ```bash
     ps -le | tail -n+2 | awk '{print $13” ”$14}' | awk -F : '{print 3600*$1+60*$2+$3” ”$4}' | sort -nr | head -n+1 | awk '{print $2}'
    ```

0. Znajdź proces, który został włączony najwcześniej

    ```bash
     ps -eo %x%c | sort | tail -2 | head -1 | awk '{print $2}'
    ```

0. Ile procesów potomnych ma bieżący terminal (ID bieżącego terminala jest przechowywana w zmiennej systemowej $$) (Ta komenda policzy też procesy uruchomione właśnie w celu liczenia - tj.  'ps' i 'wc')

    ```bash
     ps --ppid=$$ --no -headers | wc – l
    ```

0. Ile procesów potomnych procesu o PID 1 ma bieżący terminal?

    ```bash
     ps T o ppid= | awk '{if($1 == 1) print "cokolwiek"}' | wc -l
    ```


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
[link](https://git.iiet.pl/1-rok/UNIXy/blob/master/one_liners.md)
[link2](https://docs.google.com/document/d/1CDcqa5q-lHuMH--PQsvO4JcE3U3N4ru-U-B9IdNGx_A/edit?usp=sharing)
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


