# Room: Speed Chatting

## Cilj
- Pronaci flag

## Enumeracija
- nmap pronalazi upnp (protokol koji omogućava uređajima u mreži da se automatski pronađu i sami podešavaju) i ssh
- ffuf ne pronalazi direktorijume
- Postoji chat i upload profilne
- Chat blokira svaki vid XSS, ima dobru zastitu
- Renderuje poruke na svakih par sekundi, api/messages
- Upload prihvata ekstenzije, ali menja nazive dokumenata i prikazuje sadrzaj kao 'raw' text
- Cuva ih u /uploads kao Content-Type: text/html za .html ,text/x-python za .py i sl

## Eksploatacija
- napravljena reverse shell skripta //reverse_shell.py, reverse shell je način da dobiješ kontrolu nad udaljenom mašinom tako što se ta mašina sama poveže nazad ka tebi.
- u istoj napisani moja ip adresa i port za konekciju
- preko netcapa slusam i cekam konekciju posle uploada skripte //nc -lvnp 4444 (-l listen, -v verbose,-n ip umesto dns, -p port)
- Uspesno povezivanje! Radim ls i cat flag.txt i nalazim flag

## Nauceno
- Upotreba reverse shell-a
