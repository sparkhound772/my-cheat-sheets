## ASYMMETRISK KRYPTERING 

### Skapa och hantera 

Generera nyckelpar:

`gpg --expert --full-gen-key`

I en konsol:

`gpg --expert --pinentry-mode=loopback --full-gen-key`

Exportera publik nyckel för delning och backup:

`gpg --armor --export user-id > pubkey.asc`

Exportera privat nyckel för backup:

`gpg --export-secret-keys --armor user-id > privkey.asc`

Lista nycklar:

`gpg --list-keys`

Lista med signaturer:

`gpg --list-sigs user-id`

Lista privat nyckel:

`gpg --list-secret-key`

<br>

### Andras nycklar och nyckelservrar

Lista fingerprints i nyckelfil för att kunna fastställa äktheten med ägaren innan import:

`gpg --show-keys VeraCrypt_PGP_public_key.asc`

Importera nyckelfil till nyckelknippa:

`gpg --import public-key-file`

Dela med nyckelserver:

`gpg --keyserver hkps://keyserver.ubuntu.com --send-key key-id`

Hämta nyckel från nyckelserver baserat på e-post:

`gpg --keyserver hkps://keyserver.ubuntu.com --search user-id`

Hämta nyckel från nyckelserver baserat på hash/fingerprint/nyckelid (samma saker i olika format bara tror jag):

`gpg --keyserver hkps://keyserver.ubuntu.com --recv-keys key-id`

Hämta fingerprint för nyckel i nyckelknippa:

`gpg --fingerprint user-id`

Signera eventuellt nyckeln efter att du verifierat med ägaren att den är korrekt:

`gpg --sign-key key-id`

Dela eventuellt deras uppdaterade (signerade) nyckel med nyckelserver:

`gpg --keyserver hkps://keyserver.ubuntu.com --send-key key-id`

<br>

### Kryptering, signering och verifiering

Kryptera fil med recipients publika nyckel:

`gpg --recipient user-id --encrypt --armor test-file.txt`

Avkryptera fil:

`gpg --decrypt test-file.txt.asc > decrypted.txt`

Signera fil (detached) med din privata nyckel:

`gpg --detach-sign --armor <file>`

Signera utan kryptering (samt appended) med din privata nyckel:

`gpg --clearsign /path/to/file`

Verifiera signatur med publik nyckel:

`gpg --verify test.asc`

Ännu bättre (specificera även filen vars hash ska jämföras med signerad hash):

`gpg --verify fil.deb.sig fil.deb`

Signera och kryptera (appended):

`gpg --armor --recipient user-id -e --sign /path/to/file`

Verifiera OCH avkryptera (appended):

`gpg --decrypt filename.asc`

<br>

### Återkalla och radera

Generera nytt uppdaterat återkallningscertifikat inför återkallning:

`gpg --output revocation.rev --gen-revoke key-id`

Återkalla nycklar:

`gpg --import revocation.rev`

Meddela återkallning till nyckelservrar:

`gpg --send-key key-id`

Radera privat nyckel:

`gpg --delete-secret-keys key-id`

Radera publik nyckel:

`gpg --delete-key key-id`

<br>

## SYMMETRISK KRYPTERING 

### Diverse exempel 

`echo "This is a secret message" | gpg --symmetric --cipher-algo AES256 --armor --output encrypted.txt.gpg`

Ett default-namn används för krypterad fil:

`gpg --symmetric --cipher-algo AES256 --armor --no-symkey-cache <filename>`

Här väljs filnamn med --output:

`gpg --symmetric --cipher-algo AES256 --armor --no-symkey-cache --output encrypted_file.gpg <filename>`

Avkryptera:

`gpg --decrypt filename.gpg > filename `

Med nyckelfil. Här får man dock fortfarande manuellt välja lösen, så kanske att symmetric_key.txt ej används, och denna metod kan nog då bortses ifrån :

`gpg --gen-random --armor 1 2048 > symmetric_key.txt`
`gpg --symmetric --cipher-algo AES256 --armor --no-symkey-cache --passphrase-file symmetric_key.txt <filename>`

--batch verkar däremot göra att symmetric_key.txt automatiskt används (ingen passphrase prompt):

`gpg --gen-random --armor 1 2048 > symmetric_key.txt`
`gpg --symmetric --cipher-algo AES256 --armor --no-symkey-cache --passphrase-file symmetric_key.txt --batch <filename>`

Komprimera först:

`gpg --gen-random --armor 1 32 > symmetric_key.txt`
`tar -czvf - /path/to/home/folder | gpg --symmetric --cipher-algo AES256 --armor --no-symkey-cache --passphrase-file symmetric_key.txt --batch `

Använd > i stället för --output:

`gpg --gen-random --armor 1 2048 > symmetric_key.txt`
`tar -czvf - /path/to/home/folder | gpg --symmetric --cipher-algo AES256 --armor --batch --no-symkey-cache --passphrase-file symmetric_key.txt > encrypted_home.tar.gz.gpg`

Avkryptera med fil:

`gpg --decrypt --cipher-algo AES256 --passphrase-file symmetric_key.txt --batch --output testfil.txt testfil.txt.asc`

<br>

## Anteckningar

`--encrypt, --symmetric, --sign, --clearsign, och möjligen även --detach-sign kan användas i kombination i viss mån.`

<br>

## Källor

Anteckningar tagna under inlärning från följande artikelserie: https://www.linuxbabe.com/security/a-practical-guide-to-gpg-part-1-generate-your-keypair

Symmetriska krypteringsexempel framtagna med chatGPT.
