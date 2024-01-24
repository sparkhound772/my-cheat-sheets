Hitta alla förekomster av filer vars namn innehåller 'vimrc' i hela systemet samt skippa STDERR
`find -type f -name "*vimrc*" 2> /dev/null`

Hitta alla filer som är skrivbara av others
`find / -xdev -type f -perm  -o=w 2> /dev/null`

Hitta alla filer som är exekverbara som root av alla användare (har setuid=1 / u+rws):
`find / -perm -u=s -user root -ls 2> /dev/null`

Hitta alla filer i specificerad katalog
`~$ find ./ -type f`

Hitta alla filer och kataloger i specificerad katalog
`~$ find ./`

Hitta alla bash-script i specificerad katalog
`~$ find ./ -regex .+\.sh`

Hitta allt som matchar sträng INUTI specificerad katalog utan hänsyn till case.
`grep -i hejhej /`

Hitta allt som matchar IPv4-adress inuti någon fil i specificerad katalog rekursivt
`~$ echo 134.55.678.1 > regextest.txt`
`~$ grep -rE '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' ./`

Elegantare alternativ (\d tycks ej fungera)
`grep -rE '\b([1-9]{1,3}\.){3}[1-9]{1,3}\b' ./`

Alternativ
`~$ find ./ -type f -exec grep -E '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' {} +`

Matcha alla funktioner i ett bash-script i Vim
`\(#.*\n\)*[a-z_]\+\s()\s{\_.\{-}}`

Matcha vilken sökväg som helst i Vim
(funkar dock ej med t.ex. ~/fil fast jag trodde det, men borde gå att fixa)
Implementerad i veracrypt-cli-script.sh
`grep -E ^[.~]\?\(\/[^\/]*\)+[^\/]\+`

### Matcha alla rader i ett dokument i Vim som ej börjar med #
Samt substituera och lägg till backticks i början och slutet av dessa rader (skapade det nu då det behövdes för detta dokument). Gör det globalt och bekräfta för varje substitution. 

`:%s/\(^[^#].*\)/`\1/gc`

(ett backtick används i detta exempel som en del av koden men två används även för kodmarkering för markdown för denna fil, vilket kommer skapa fel i hur renderas här - se orenderad version av detta exempel för korrekt text.
