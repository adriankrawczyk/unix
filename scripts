1. Wylistuj wszystkie podane parametry
#!/bin/bash
echo "Liczba argumentow: $#"
if [ $# -eq 0 ]; then
	echo "Skrypt bez argumentow"
else
	licznik=0
	while [ $1 ]; do
		echo "Argument $licznik to $1"
		shift
		licznik=`expr $licznik + 1`
	done
fi
2. Monitoruj liczbę procesów (bez procesu liczącego)
#!/bin/bash
while [ 1 ]; do
	lproc=`ps aux | wc -l`
	lproc=`expr $lproc - 1`
	echo "Liczba procesow: $lproc"
	sleep 2
done
3.Wypisz opis użytkownika o podanym UID
#!/bin/bash
if [ $# -lt 1 ]; then
	echo -n "Podaj UIDs: "
	read uid
else
	uid=$*
fi
for uzytek in $uid; do
	opis=`cat /etc/passwd | cut -f3,5 -d: | grep ^$uzytek: | cut -f2 -d:`
if [ $opis ]; then
        echo "Uzytkownik $uzytek to $opis"
else
        echo "Uzytkownik $uzytek bez opisu"
fi

done

4.Wypisz opis użytkowników o podanych UIDach
#!/bin/bash
for plik in .* * ; do
# plik / katalog
	if [ -d $plik ]; then
		opis='d'
	else
		opis='-'
	fi
# prawo odczytu
	if [ -r $plik ]; then
		opis=$opis'r'
	else
		opis=$opis'-'
	fi
# prawo zapisu
	if [ -w $plik ]; then
		opis=$opis'w'
	else
		opis=$opis'-'
	fi
# prawo wykonywania
	if [ -x $plik ]; then
		opis=$opis'x'
	else
		opis=$opis'-'
	fi
	echo "$opis   $plik"
done
5.Wyświetl prawa dostępu do danego pliku z punktu widzenia procesu basha
#!/bin/bash

if [ -z "$2" -o ! -r "$1" ]; then
echo "Skladnia: $0 [plik] [rozmiar kawalka]"
exit 1
fi

SIZE=`ls -l $1 | awk '{print $5}'`

if [ $2 -gt $size ]; then
echo "Rozmiar kawalka musi byc mniejszy od rozmiaru pliku"
exit 2
fi

CHUNK=$2
TOTAL=0
PASS=0
while [ $TOTAL -lt $SIZE ]; do
PASS=`expr $PASS + 1`
echo "Tworzenie $1.$PASS..."
dd conv=noerror if=$1 of=$1.$PASS bs=$CHUNK skip=`expr $PASS - 1` count=1 2>/dev/null
TOTAL=`expr $TOTAL + $CHUNK`
done

echo "Liczba utworzonych kawalkow: $PASS pliku $1"
6.Podziel plik na kawałki o zadanym rozmiarze
#!/bin/bash
# skrypt co 10 sec. wypisuje liczbe procesow
# po otrzymaniu ^c konczy dzialanie z komunikatem
                                                                                
trap 'echo "Otrzymalem sygnal 3"; exit 1' 3
trap 'echo "Otrzymalem sygnal 2"; exit 1' 2
                                                                                
SLEEP_TIME=2
while [ 1 ]
do
        lproc=`ps ax | wc -l`
        lproc=`expr ${lproc} - 1`
        echo "Dziala ${lproc} procesow"
        sleep ${SLEEP_TIME}
done

2016/2017 - Zestaw 5 - Programowanie w językach interpreterów poleceń

Skrypt wypisuje liczbę argumentów, z którymi został uruchomiony. Jeżli został uruchomiony
bez argumentów to wypisuje stosowny komunikat. Skrypt w kolejnych liniach wypisuje
wszystkie argumenty z którymi został uruchomiony poprzedzając każdy z nich napisem
argument nr. x  gdzie x jest numerem argumentu.

#!/usr/bin/env bash
# Piotr Janczyk, 2017

if (($# == 0)); then
    echo "Brak argumentów"
else
    for ((i=1; i <= $#; i++)); do
        echo "$i: ${!i}"
    done
fi

W pętli nieskończonej, co 3 sekundy skrypt wypisuje liczbę procesów uruchomionych w
systemie. Zakończenie działania - kombinacja klawiszy Control-C.

#!/usr/bin/env bash
# Piotr Janczyk, 2017

while [[ 1 ]]; do
    echo "$(ps -e -o pid= | wc -l)"
    sleep 3
done

Skrypt jako argument wywołania otrzymuje UID. Jeżli został uruchomiony bez argumentu,
to doczytuje go z klawiatury. Skrypt korzystając z pliku /etc/passwd wypisuje zawartość 5.
kolumny linii opisującej użytkownika o podanym UID.

#!/usr/bin/env bash
# Piotr Janczyk, 2017

if (($# < 1)); then
    echo -n "Podaj UID: "
    read uid
else
    uid=$1
fi

echo "$(awk -F : -v uid=$uid '$3==uid { print $5 }' /etc/passwd)"

Jak w punkcie poprzednim, ale należy uwzględnić przypadek, w którym w linii komend
podano lub należy przeczytac kilka argumentów - UID kilku użytkowników.

#!/usr/bin/env bash
# Piotr Janczyk, 2017

if (($# < 1)); then
    read -p "Podaj UID użytkowników: " -a uids;
else
    uids=("$@")
fi

for uid in "${uids[@]}"; do
    echo "$(awk -F : -v uid="$uid" '$3==uid { print $5 }' /etc/passwd)"
done

Skrypt wypisuje z katalogu w którym został uruchomiony nazwy wszystkich plików i katalogów z zaznaczeniem, czy jest to plik regularny czy katalog. Dla plików podaje prawa
dostępu użytkownika (rwx), który uruchomił skrypt.

#!/usr/bin/env bash
# Piotr Janczyk, 2017

shopt -s nullglob # wymagane, aby "*" działała poprawnie dla braku plików
shopt -s dotglob # wymagane, aby zostały uwzględnione ukryte pliki

for file in *; do
    echo -n "$file, "
    if test -d "$file"; then
        echo "katalog"
    else
        echo -n "plik, "
        test -r "$file" && echo -n "r" || echo -n "-"
        test -w "$file" && echo -n "w" || echo -n "-"
        test -x "$file" && echo -n "x" || echo -n "-"
        echo ""
    fi
done

* Skrypt ma podzielić plik na kawałki (zawartość dużego pliku ma zostac zapisana do
plików o rozmiarach odpowiednio mniejszych). Skrypt musi zostać uruchomiony z dwoma
argumentami. Pierwszy to nazwa pliku, który ma zostać podzielony, a drugi to rozmiar pojedynczego
kawałka (mniejszego pliku) w bajtach. Do kopiowania najprościej użyć polecenia
dd w postaci:

#!/usr/bin/env bash
# Piotr Janczyk, 2017

if (($# != 2)); then
    echo "Składnia:  zad-6.sh PLIK ROZMIAR_CZĘŚCI"
    exit
fi

file="$1"
part_size="$2"
file_size=$(stat --format="%s" "$1")
parts=$(( (file_size + part_size - 1) / part_size )) # liczba części zaokrąglona w górę

for ((i=0; i < parts; i++)); do
    part_name="$file.part$((i+1))"
    echo "$part_name"
    dd conv=noerror if="$file" of="$part_name" bs=$part_size skip=$i count=1 2>/dev/null
done

echo "Plik $file został podzielony na $parts części"

Dla interpretera poleceń bash należy napisać skrypt który w pętli nieskończonej co sekundę
wypisuje napis ciagle zyje. W przypadku otrzymania sysgnalu USR1 lub USR2 wypisuje napis
dostalem sygnal USRx - gdzie x jest numerem otrzymanego sygnału (wskazówka: instrukcja
trap).

#!/usr/bin/env bash
# Piotr Janczyk, 2017

trap 'echo "Dostałem sygnał USR1"' SIGUSR1
trap 'echo "Dostałem sygnał USR2"' SIGUSR2

while [[ 1 ]]; do
    echo "Ciągle żyję"
    sleep 3
done
