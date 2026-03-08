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
*chmod +x server*  
*./server*  

![server oikeudet ja ajo, eli testaus toimiiko](h7images/server-ajo.png)

Siirretään script /usr/local/bin kansioon ja ajetaan se käskyillä  
*sudo cp server /usr/local/bin*  
*server*  

![kopioidaan script /usr/local/bin ja ajetaan se](h7images/server-for-all.png)

Toimii. 


## d) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.  


![käynnistän micro editorin](h7images/micro-server.png)


## Lähteet 

Karvinen 2026:  https://terokarvinen.com/linux-palvelimet/  
C-ohjelman lähde:  https://www.geeksforgeeks.org/c/c-hello-world-program/  
Go-ohjelman lähde: https://gobyexample.com/hello-world  
echo komennon lähde: https://linuxize.com/post/echo-command-in-linux-with-examples/  
uptime komennon käyttö lähde: https://www.site24x7.com/learn/linux/uptime.html  
df komennon käyttö lähde: https://linuxize.com/post/how-to-check-disk-space-in-linux-using-the-df-command/  

