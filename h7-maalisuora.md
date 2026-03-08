Kirjoittanut Timo Lampinen 2026  
Linux-palvelimet kurssi - ICI003AS2A-3016  
Tehtävä h7 sivulta: https://terokarvinen.com/linux-palvelimet/  

# Tehtava H7 Maalisuora

## a) Kirjoita Hei Maailma kolmella kielellä  

Kirjaudutaan omalle palvelimelle  
*ssh timo@185.20.138.164*  

![ssh yhteyden muodostaminen](h7images/ssh-timo.png)  

Tehdään ohjelmat kolmelle eri kielellä: Python, C ja Go.   

Ensin päivitetään ja asennetaan ohjelmat Python, C ja Go käskyillå:
*sudo apt update*  
*sudo apt-get install python3 gcc golang-go*  

![update ja install python3 gcc ja go ](h7images/asenna-ohj-kielet.png)  

Siirrytään aiemmin tehtyyn scripts hakemistoon ja aletaan tekemään micro-ohjelmalla heipython.py tiedostoa  
*cd scripts*
*micro heipython.py*

![siirtyään kansioon ja aletaan micro:lla kirjoitta koodia](h7images/micro-py-1.png)  

Kirjoitetaan print komento python-kielellä 

![print komento pythonilla](h7images/py-code-1.png)  

Ajetaan heipython.py  
*python3 heipython.py*  

![ajetaan ja todetaan python koodin toimivan](h7images/py-ajo-1.png)  

Toimii!  
  
Aloitetaan kirjoittamaan ohjelmaa c-kielellä  
*micro heic'

![käynnistetään koodinkirjoittaminen](h7images/micro-c.png)  

Kirjoitetaan ohjelma.  
lähteenä:  https://www.geeksforgeeks.org/c/c-hello-world-program/  

![koodin sisältö micro ohjelmassa](h7images/c-code-1.png)  

C-ohjelmat pitää ensin kääntää ohjelmiksi. Kääntäminen tapahtuu komennolla: gcc heic.c -o heic  
Syntaksin selitys:   
- gcc on kääntäjä
- heic.c lähdekoodin tiedosto joka käännetään
- -o kertoo että seuraavaksi tulee käännetyn tiedoston nimi
- heic on käännetyn ohjelman nimi
  
Suoritetaan komento ja ajetaan ohjelma heic tässä kansiossa komennoilla:  
*gcc heic.c -o heic*  
*./heic*  

![koodin sisältö micro ohjelmassa](h7images/c-ajo-1.png)  

Huomaamme, että print komentomme lopussa ei ole rivinvaihtoa, joten komentokehoite tullee kirjoituksen perään.  
Lisätään microlla rivinvaihto, joka toteutuu, kun laitetaan \n  printf komennon sisälle. 

![muokataan koodia](h7images/c-code-2.png)  

Käännetään ohjelma ja ajetaan se:  
*gcc heic-c -o heic*  
*./heic*

![C tiedoston kääntäminen ohjelmaksi ja ajaminen](h7images/c-ajo-2.png)  

Hienoa. Nyt ohjelma toimii kuten pitää.  

Tehdään Hei maailma ohjelma käyttäen Go-kieltä. Itselleni tämä kieli on täysin tuntematon, joten etsin sopivan lähteen.  
Lähde:   https://gobyexample.com/hello-world  
Aletaan kirjoittamaan koodia komennolla  
*micro hei-maailma.go*  

![käynnistetään koodinkirjoittaminen](h7images/micro-go-1.png) 

Kirjoitetaan ohjelma microlla  

![kirjoitettu Go koodi](h7images/go-code-1.png) 

Ajetaan ohjelma komennolla  
*go run hei-maailma.go*  

![Go tiedoston ajaminen](h7images/go-ajo-1.png) 

Toimii. Käännetään seuraavaksi go ohjelmaksi ja ajetaan se  
*go build hei-maailma.go*  
*go build hei-maailma.go*  

![Go tiedoston kääntäminen ohjelmaksi ja ajaminen](h7images/go-build-1.png) 

Toimii. Hienoa.  

## b) Lähdeviitteet. Tarkista ja tarvittaessa lisää lähdeviitteet kaikkiin raportteihisi

Puutteet korjattu 

## c) Laita Linuxiin uusi, itse tekemäsi komento niin, että kaikki käyttäjät voivat ajaa sitä.  

Päätin tehdä scriptin, joka näyttää serverin tietoja yhdellä komennolla. Koska komentoa server ei ole, päätin tehdä sen sille nimelle  
*micro server* 

![käynnistän micro editorin](h7images/micro-server.png)

Alkuun asetetaan, millä komento ajetaan eli bash. Sen jälkeen muut kommennot:  
*#!/bin/bash* määrittää millä komennolla script suoritetaan. Scripteissä se on bash    
*echo "Server: $(hostname)* tulostaa Server: ja hostname. Lähde: https://linuxize.com/post/echo-command-in-linux-with-examples/    
"echo "User: $(whoami)* tulostaa User: ja käyttänimen  
*echo "Uptime:"* tulostaa Uptime:  
*uptime* tulostaa kuinka kauan severi on pyörinyt. Lähde: https://www.site24x7.com/learn/linux/uptime.html   
*echo "Disk usage:"*  tulostaa Disk usage:  
*df -h /* tulostaa järjestelmän levytilan käytön tietoja. -h näyttää koko tiedot luettavassa muodossa (KB, MB, GB). / antaa poluksi root kansion, eli koko järjestelmän tilankäyttö nähdään käyttäen tätä. Lähde: https://linuxize.com/post/how-to-check-disk-space-in-linux-using-the-df-command/  

![serverin scriptn](h7images/server-script.png)

Script täytyy muuttaa ensin ajettavaan muotoon oikeuksia muokkaamalla ja sen jälkeen se voidaan ajaa.  
*chmod ugo+x server*  
*./server*  

![server oikeudet ja ajo, eli testaus toimiiko](h7images/server-ajo.png)

Siirretään script /usr/local/bin kansioon ja ajetaan se käskyillä  
*sudo cp server /usr/local/bin*  
*server*  

![kopioidaan script /usr/local/bin ja ajetaan se](h7images/server-for-all.png)

Toimii. 


## d) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.  

Valitsin tehtäväksi DJ Hatut tehtävän 2024 syksyn kurssilta (https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-syksy-linux-palvelimet/  kohta g). 

Tehtävänanto on:  

Prosessinhallintaa ja lokeja.
a) Kuormitusta yli ajan. Tietysti palvelin hidastelee juuri silloin, kun olet nukkumassa. Seuraisipa joku kuormitusta tuolloin. Asenna heti aluksi jokin ohjelma seuraamaan kuormitusta, jotta voit tarkastella sitä koko tehtävän ajalta. Sopivia ohjelmia ovat esimerkiksi 'munin' ja sysstat ('sar').
b) Kuormita järjestelmän eri osa-alueita. Esim. 'stress'. Etsi prosessi toisesta ikkunasta 'top' tai 'htop', järjestystä voi vaihtaa "P" ja "M".
Kokeile käytännössä, selitä ja analysoi. Muista selittää, mitä komennolla halutaan selvittää ja tulkitse kokeilusi tulokset. Aiheuta tarvittaessa kuormaa tai muuta työkalulla näkyvää tulkittavaa.
c) iotop; iotop -oa
d) dstat
e) ss --listening --tcp --numeric; ss --listening --tcp; ss --tcp; ss --listening --udp; ss --listening --udp;
f) grep -i error /var/log/syslog; grep -ir error /var/log/
g) Load average näkyy esim 'uptime', 'top', 'htop'. Prosessoriydinten määrä näkyy 'nproc'. Miten load average tulkitaan? Miksi prosessoriydinten määrä on tässä kiinnostava? Vapaaehtoisena bonuksena voit miettiä, mitä hyötyä on kuormituslukemasta, joka voi mennä yli yhden eli yli 100%.
h) Analysoi lopuksi koko ajalta keräämäsi kuormitustiedot. Löydätkö esimerkiksi aiheuttamasi kuormituspiikin?


### a) asennetaan ohjelma 

asennetaan sysstat. Lähde: https://www.geeksforgeeks.org/linux-unix/sar-command-linux-monitor-system-performance/    
*sudo apt install sysstat*  

![installoidaan sysstat](h7images/inst-systat.png)


### b) kuormitaa järjestelmää  

asennetaan stress  
*sudo apt install stress*  

![installoidaan stress](h7images/inst-stress.png)

käynnistetään monitorointi toisessa terminaalissa komennolla   
*sar -u 1*  

![sar tulostus alkaa](h7images/sar-0.png)

stress ohjeita https://www.geeksforgeeks.org/linux-unix/linux-stress-command-with-examples/  
Käynnistetään kuormitus 10 sekunniksi komennolla  
*stress -c 8 --timeout 10*  
c tarkoittaa 8 cpu:ta ja timeoutilla määritellään kesto

![käynnistetään stress](h7images/stress-c8-t10.png)

Katsotaan mitä *sar -u 1* komento näyttää tuolta ajalta  

![sar tulostus](h7images/sar-1.png)

Näemme selkeästi, että cpu kuormittuu täysille tuoksi ajaksi, eikä järjestelmä ole idle hetkeäkään

Katsotaan mitä muistin käyttöa voidaan testata.  
Laitetaan muistin monitorointi päälle komennolla  
*sar -r 1 25*  

testataan muistia komennolla  
*stress --vm 10 --vm-bytes 256*   

![sar tulostus vm](h7images/stress-vm-1.png)


![sar tulostus](h7images/sar-r-2.png)

Tulosteesta ei voi päätellä okein mitään. Ainoa arvo mikä muuttuu on kbdirty, mutta arvo on koko ajan niin pieni, ettei siitä oikein voi päätellä mitään - paitsi, että kun se on 0, ei ole yhtään dataa odottamassa kirjoittamista levylle.  iot


### c) iotop

iotop tarkastelee järjestelmän levylle kirjoittamista ja lukemista. Lähde: https://www.geeksforgeeks.org/linux-unix/iotop-command-in-linux-with-examples/

asennetaan iotop komennolla  
*sudo apt install iotop*  

käynnistin ohjelman annetulla komennolla  
*sudo iotop -oa*  
- o parametri näyttää prosessit, jotka oikeasti suorittavat I/O toimintoja  
- a parametri näyttää kertyneen IO-käytön ajan kuluessa  

![iotop -oa monitorointi](h7images/sudo-iotop.png)  

Näemme päivittyvät. Koska loki näytti tyhjältä, latasin sivuni bonakota.com, jolloin viimeinen rivi, missä apache2 on mainittu tuli näkyviin.  Tarkastellaan rivin tietoja:  
260368 be/4 www-data 0.00 B 4.00 K apache2 -k start  
- 260368 on prosessin id
- be/4 on I/O-prioriteetti (best effort, taso 4)
- www-data on käyttäjä, jonka oikeuksilla prosessi toimii
- 0.00 B kertoo paljonko lukee levyltä nyt  
- 4.00 K kertoo paljonko kirjoittaa levylle nyt  
- apache2 -k start on käynnistetty ohjelma parametreineen

Huomasin myös, että ladattaessa sivu Total DISK WRITE ja Current DISK WRITE antavat pieniä lukuja.  

Epäilen, että nämä ovat lokitiedostoja, mitä kirjoitetaan apachen lokeihin. Testaan näin:   
*cd /var/log/apache3/*  
*tail other_vhosts_access.log*  
Lataan tässä välissä selaimessa bonakota.com sivun (joka on tällä palvelimella).  
Samaan aikaan iotop näkymässä on muutosta disk write. 
*tail other_vhosts_access.log*  

Iotop -oa näkymän muutos:  
![iotop tulostus](h7images/iotop-write.png)  

molemmat lokit, joista jälkimmäiseen on tullut lisäys:  
![tail log](h7images/tail-log.png)  

Tämä ei aukottomasti todista, että kyse on juuri tuosta tapahtuamasta, koska kirjoitustapahtumia voi myös olla muita. Todennäköisesti tämä on yksi kyseisistä tapahtumista. Tämä on omaa päättelyäni ja todistaakseni tämän aukottomasti pitäisi sama tapahtuma toistaa useita kertoja, että tultaisiin varmemmin siihen tulokseen, että tämä on yksi suoritettuista kirjoitusprosesseista. 

### d) dstat  

dstat on työkalu, jolla näemme Linuxin järjestelmän resurssienkäyttöä reaaliajassa.
Lähde https://www.geeksforgeeks.org/linux-unix/dstat-command-in-linux-with-examples/  

asennus  
*sudo apt install dstat*  



## Lähteet 

Karvinen 2026:  https://terokarvinen.com/linux-palvelimet/  
GeegsForGeegs.org - C-ohjelman lähde:  https://www.geeksforgeeks.org/c/c-hello-world-program/  
Go-ohjelman lähde: https://gobyexample.com/hello-world  
echo komennon lähde: https://linuxize.com/post/echo-command-in-linux-with-examples/  
uptime komennon käyttö lähde: https://www.site24x7.com/learn/linux/uptime.html  
df komennon käyttö lähde: https://linuxize.com/post/how-to-check-disk-space-in-linux-using-the-df-command/  
Vanha laboratirioharjoitus. Kohta g: https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-syksy-linux-palvelimet/ 
GeegsForGeegs.org - Sar command to monitor system performance: https://www.geeksforgeeks.org/linux-unix/sar-command-linux-monitor-system-performance/  
GeegsForGeegs.org - Stress käytön esimerkkeja: https://www.geeksforgeeks.org/linux-unix/linux-stress-command-with-examples/   
GeegsForGeegs.org - iotop käyttö ja esimerkkejä: https://www.geeksforgeeks.org/linux-unix/iotop-command-in-linux-with-examples/
GeegsForGeegs.org - dstat käyttö ja esimerkkejä: https://www.geeksforgeeks.org/linux-unix/dstat-command-in-linux-with-examples/





