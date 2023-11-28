
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
#• -l - najważniejszy parametr, wypisuje szczegóły plików w danym katalogu w formie
#listy
#• -a - wypisuje wszystkie pliki razem z ukrytymi(tj. Zaczynające się kropką) –
#UWAGA – wypisuje również pliki . I ..
#• -A - to samo co wyżej, tylko nie wypisuje plików . I ..
#• -s – pokazuje również ilość bloków
#• -id – wyświetla numer węzła i-node danego katalogu
#• -d – wyświetla numery węzłów i-node dla wszystkich listowanych plików
#obrazek tłumaczący strukturę wyniku ls 

```
Find
```
# File search utility. Extensive, check the documentation for specific parameters and syntax.
# If not explicitly stated to search recursively (including subdirectories), it's easier to use ls.
# -type x – wyszukiwanie tylko plików o typie x (d-katalog, f-zwykły plik, l –
#dowiązanie symboliczne(symlink))
#• -name „nazwa” - wyszukiwanie plików o konkretnej nazwie. Można używać
#specjalnych znaków tak jak w innych wyszukiwarkach typu *,?,[]
#• -maxdepth x – zagnieżdżenie wyszukiwań – czyli ile katalogów w głąb
#wyszukiwać. np. jeśli damy 1 wyszuka pliki tylko w danym katalogu, jeśli 0
#wynikiem będzie tylko nazwa katalogu w którym szukamy
#• -exec x ;\ - gdzie x jest poleceniem które wykonujemy dla każdego znalezionego
#pliku. Nawiasy klamrowe przekazują do polecenia nazwę tego pliku. np. aby
#wyświetlić zawartość każdego pliku w katalogu domowym (bez podkatalogów)
#mamy polecenie: find ~ -type f -maxdepth 1 -exec cat {} \;
#• -printf „szablon” - jeden z ważniejszych parametrów na kolokwium, przy tym
#często trzeba zaglądnąć do manuala(przy tym parametrze w manie, są objaśnione
#wszystkie symbole), bo ciężko zapamiętać każdy symbol. Stosując go nie
#wyświetlamy nazw plików, tylko to co chcemy np. rozmiar, ilość bloków, albo
#właściciela.
#Przykładowo, jeśli chcemy dla danego katalogu wyświetlić nazwy wszystkich
#plików wraz z rozmiarem i właścicielem(oddzielone spacją) mamy polecenie:
#find ~ -maxdepth 1 -printf "%f %s %u \n"
#gdzie %f to nazwa pliku, %s to rozmiar w bajtach, %u to nazwa właściciela, a \n to
#załamanie linii(taki enter)
#• -size – wyświetla tylko pliki o określonym rozmiarze np. pliki w /usr/bin o wielkości
#do 1MB: find /usr/bin -size -1M

```
Wc
```
# Counts lines, characters, words, and more (in the output).
#-l liczy linie
#-c liczy bajty
#-w liczy słowa
#-m liczy znaki
```
Sort
```
# Sorts the output.
#-n ( uwzględnia sortowanie liczb(chyba)) wydaję mi się, że można spokojnie używać zawsze
#-r odwrotne sortowanie
```
Uniq
```
# Removes duplicate lines (usually needs to be sorted first).
#c wypisuje wraz z liczbą powtórzeń
#-d wypisuje tylko te które się powtórzyły
#-uwypisuje tylko unikatowe linie
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
#x – wyświetla listę w stylu BSD
#u – wyświetla nazwy użytkowników
#t – pokazuje procesy tylko z danego terminala
#e lub a – wyświetla wszystkie procesy(jest jakaś drobna różnica między nimi, ale nie jest to
#chyba istotne)
#o wyświetla specjalny output(podobnie jak printf w poleceniu find) (przykłady znajdziesz na
#https://git.iiet.pl/1-rok/UNIXy/blob/master/one_liners.md)
#l – format długi(wyświetla więcej szczegółów)
```
Grep x
```
# One of the most important commands. Filters output based on the pattern x.
#-v – negacja wyrażenia. Czyli wypisuje wszystkie które nie pasują do wyrażenia
#W grepie można używać wyrażeń regularnych, najważniejsze symbole które powinieneś
#znać to początek linii - ^ i koniec linii - $ . Co do reszty, do nauki polecam interaktywny interpreter
#https://regexr.com/
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
ls
```
# 1. File Type and Permissions:
The first character indicates the file type:
- for regular files
d for directories
l for symbolic links
and more.
The next nine characters represent the file permissions:
The first three characters are for the owner's permissions.
The second three characters are for the group's permissions.
The last three characters are for others' (non-owner, non-group) permissions.
Each group of three characters can have the following values:
r for read permission
w for write permission
x for execute permission
- if the respective permission is not granted.
Example: drwxr-xr-x indicates a directory with read, write, and execute permissions for the owner, and read and execute permissions for both the group and others.
# 2. Number of Hard Links:
This column shows the number of hard links to the file. A hard link is an additional reference to the same inode (data structure on disk) as the original file.
# 3. Owner:
This column displays the username of the file's owner.
# 4. Group:
This column shows the group associated with the file.
# 5. File Size:
Indicates the size of the file in bytes.
# 6. Modification Time:
Displays the date and time when the file was last modified.
# 7. File or Directory Name:
This column contains the name of the file or directory.
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
Linux (/ˈlɪnʊks/ LIN-uuks)[11] is a family of open-source Unix-like operating systems based on the Linux kernel,[12] an operating system kernel first released on September 17, 1991, by Linus Torvalds.[13][14][15] Linux is typically packaged as a Linux distribution (distro), which includes the kernel and supporting system software and libraries, many of which are provided by the GNU Project. Many Linux distributions use the word "Linux" in their name, but the Free Software Foundation uses and recommends the name "GNU/Linux" to emphasize the use and importance of GNU software in many distributions, causing some controversy.[16][17]

Popular Linux distributions[18][19][20] include Debian, Fedora Linux, Arch Linux and Ubuntu. Commercial distributions include Red Hat Enterprise Linux and SUSE Linux Enterprise. Desktop Linux distributions include a windowing system such as X11 or Wayland, and a desktop environment such as GNOME or KDE Plasma. Distributions intended for servers may omit graphics altogether, or include a solution stack such as LAMP. Because Linux is freely redistributable, anyone may create a distribution for any purpose.[21]

Linux was originally developed for personal computers based on the Intel x86 architecture, but has since been ported to more platforms than any other operating system.[22] Because of the dominance of the Linux-based Android on smartphones, Linux, including Android, has the largest installed base of all general-purpose operating systems, as of May 2022.[23][24][25] Although Linux is, as of November 2022, used by only around 2.6 percent of desktop computers,[26] the Chromebook, which runs the Linux kernel-based ChromeOS, dominates the US K–12 education market and represents nearly 20 percent of sub-$300 notebook sales in the US.[27] Linux is the leading operating system on servers (over 96.4% of the top 1 million web servers' operating systems are Linux),[28] leads other big iron systems such as mainframe computers, and is used on all of the world's 500 fastest supercomputers[d] (as of November 2017, having gradually displaced all competitors).[29][30][31]

Linux also runs on embedded systems, i.e. devices whose operating system is typically built into the firmware and is highly tailored to the system. This includes routers, automation controls, smart home devices, video game consoles,[32] televisions (Samsung and LG Smart TVs),[33][34][35] automobiles (Tesla, Audi, Mercedes-Benz, Hyundai and Toyota),[36] and spacecraft (Falcon 9 rocket, Dragon crew capsule and the Perseverance rover).[37][38]

Linux is one of the most prominent examples of free and open-source software collaboration. The source code may be used, modified and distributed commercially or non-commercially by anyone under the terms of its respective licenses, such as the GNU General Public License (GPL). The Linux kernel, for example, is licensed under the GPLv2, with an exception for system calls that allows code that calls the kernel via system calls not to be licensed under the GPL.[39][40][21]
