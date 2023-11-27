### awk
```
    opcja -F pozwala wybrać seperator. Domyślnym seperatorem jest spacja.
    np. dla plików etc/passwd struktura wygląda mniej więcej tak:
    specu:x:1000:1000:Dawid Focht,,,:/home/specu:/bin/bash
    Tutaj seperatorem jest dwukropek.
    Przykładowe zadanie - wypisz wszystkie nazwy użytkowników które mają UID większe od
    100
    komenda - cat etc/passwd | awk -F: ‘{if($3 > 100) print $1}’
```
### ls
```
    Bardzo podstawowa komenda. Na kolokwium używasz tylko jeśli zaznaczono, że nie trzeba
    przeszukiwać podkatalogów.
    Parametry:
    • -l - najważniejszy parametr, wypisuje szczegóły plików w danym katalogu w formie
    listy
    • -a - wypisuje wszystkie pliki razem z ukrytymi(tj. Zaczynające się kropką) –
    UWAGA – wypisuje również pliki . I ..
    • -A - to samo co wyżej, tylko nie wypisuje plików . I ..
    • -s – pokazuje również ilość bloków
    • -id – wyświetla numer węzła i-node danego katalogu
    • -d – wyświetla numery węzłów i-node dla wszystkich listowanych plików
    obrazek tłumaczący strukturę wyniku ls
```
### find
```
    Wyszukiwarka plików, bardzo rozbudowana, dobrze jest wiedzieć gdzie mniej więcej w
    manie(dokumentacji) można szukać konkretnych parametrów i składni do tego polecenia.
    Jeśli w poleceniu nie jest napisane, żeby wyszukiwać rekursywnie(tj. z uwzględnieniem
    podkatalogów), łatwiej będzie użyć ls.
```
### wc
```
    (w wyjściu)liczy linie, znaki,słowa i kilka innych
```
### sort
```
    sortuje wyjście
```
### uniq
```
    usuwa powtarzające się linie(zazwyczaj trzeba posortować wcześniej)
```
### head -nx
```
    wypisuje tylko x pierwszych linijek. Użycie ujemnej liczby linijek wypisuje wszystkie
    minus x. UWAGA! -1 wypisuje wszystkie, a -2 wypisuje dopiero wszystkie prócz jednej
```
### tail -nx
```
    to samo co head tylko liczy od końca
```
### ps
```
    wyświetla info o procesach
```
### grep x
```
    jedna z najważniejszych komend. Filtruje wyjście wg schematu x
```
### Dodatkowe protipy
```
    • wyszukiwanie w manualu: wpisujemy znak ?, następnie wyszukiwana fraza.
    Klawiszami n i shift+n przemieszczamy się między wyszukiwaniami
    • zmienna $$ przechowuje PID aktualnego terminala
```
