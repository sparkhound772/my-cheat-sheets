### Anslut

`ssh USER@IP`

Eller ännu bättre

`ssh -i ~/.ssh/KEY USER@IP`

så specificeras nyckel. Annars testas alla nycklar tror jag vilken kan riskera utlåsning.

`-p PORT`

ifall annan port än 22 används.

### Cacha nyckel tillfälligt

Är ssh-agent igång?

`ps aux | grep ssh-agent`

Starta annars med

`eval "$(ssh-agent)"`

Cacha

`ssh-add ~/.ssh/KEY`

### Skapa nycklar

`ssh-keygen`

alternativt

`ssh-keygen -t ed25519 -C "KOMMENTAR"`

Var varsam så att namnet på nyckeln som skapas inte redan finns, för då skrivs den över.

Välj ed25519 (kortare och säkrare).

Skapa passhprase (säkrare då det inte gör lika mycket om den privata nyckeln blir stulen. Anges sedan på klientsidan vid anslutning, men nyckeln kan även cachas så att man slipper uppge passphrase på ett tag).

### Överför publik nyckel till server-host

Antingen klipp och klistra publik nyckel till 

*~/.ssh/authorized_keys* 

eller kör

`ssh-copy-id -i ~/.ssh/KEY.pub USER@IP`

### Filer (klientsidan)

*~/.ssh/known_hosts* <br>
Innehåller fingeravtryck för godkända hosts. Förhindrar att man råkar ansluta till en annan host men med samma IP-adress.

Ok att radera, ny host-entry skapas vid ny inloggning.

*~/.ssh/id_ed25519* 

Privat nyckel. Kan döpas till valfritt.

*~/.ssh/id_ed25519.pub*

Publik nyckel. Kan döpas till valfritt. Sista ordet i filen utgör valfri kommentar (som till och med kan raderas).

*~/.ssh/config* 

```
Host VALFRITT
    Hostname IP-adress
    Port 22
    User root
```

Tillåter anslutning med bara hostnamn.
Flera hosts kan läggas till i filen.

*/etc/ssh/sshd_config*

Globala inställningar (överskuggas av *~/.ssh/config*).

### Filer (hostsidan)

*~/.ssh/authorized_keys* 

Som namnet säger.

*/etc/ssh/sshd_config*

`PermitRootLogin no`

`PasswordAuthentication no`

`systemctl restart sshd`

*/etc/ssh/ssh_host_*

Första gången man ansluter och blir tillfrågad om man vill acceptera fingeravtryck (eller något) så skapas dessa tydligen.

Om man klonar en server följer dessa med vilket kan göra klienten förvirrad (p.g.a. annorlunda IP-adress t.ex.).

Var försiktig med att radera dessa tydligen.

### Loggar

`systemctl status ssh` <br>
`journalctl -fu ssh` <br>
`tail -f /var/log/auth.log`

Inte samma i alla system men på ett ungefär.

### Härdning

Inaktivera lösenords- och root-inloggning (se ovan om *sshd_config*).

### Övrigt

Använd `ssh -v` för detaljerad output.

Olika nycklar till olika servrar är säkrare. Om en blir stulen så kompromissas ej de andra. Dock kanske rimligt att ha samma till sina egna servrar. Men har man många nyckar så bör man specificera vilken man vill använda vid anslutning, annars testas alla och man kan bli utlåst.

### Källor

Dessa antackningar togs under inlärning från följande video: https://www.youtube.com/watch?v=YS5Zh7KExvE
