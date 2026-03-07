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

## Lähteet 

Karvinen:  https://terokarvinen.com/linux-palvelimet/  
