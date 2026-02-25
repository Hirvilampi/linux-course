Kirjoittanut Timo Lampinen 2026  
Linux-palvelimet kurssi - ICI003AS2A-3016  
Tehtävä h6 sivulta: https://terokarvinen.com/linux-palvelimet/  

# Tehtava H6 Salataampa

## x) Lue ja tiivistä  

Let's Encrypt 2024: How it works (https://letsencrypt.org/how-it-works/)  
-  

The Apache Software Foundation 2025: Apache HTTP Server Version 2.4 [Official] Documentation: SSL/TLS Strong Encryption: How-To: (https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample)  
-  

## a) Let's - asenna palvelimellesi ilmainen TLS-sertifikaatti Let's Encryptilta. Osoita, että se toimii.  

Kirjaudun ensin sisään palvelimelle  
*ssh timo@185.20.138.164*  

Tsekataan, että apache2 on päällä  
*sudo systemctl restart apache2*  

![ssh ja update toimivat](h6images/ssh-update.png)  

Toimiii, koska ei anna mitään viestiä    

Tarkastetaan web-sivun näkyvyys lataamalla bonakota.com.
Toimii tällä koneella, sekä toisella koneella. 

![http://bonakota.com latautuu](h6images/bonakota.works.png)  

Ensin update palvelimen ohjelmistolle  
*sudo apt-get update*  

Asennan palvelimelle certbot:n, python3-certbot, python3-certbot-apache
*sudo apt install certbot*  
*sudo apt install python3-certbot*  
*sudo apt install python3-certbot-apache*  

![install certbot](h6images/inst-certbot.png)  
![install python3-certbot ja python3-certbot-apache](h6images/python-certbot-apache.png)  

Käynnistetään certbot ja asennetaan sertifikaatit kaikille sivustoille tämän alla  
*sudo certbot*  

![sudo certbot alkaa](h6images/sudo-certbot.png)  
![succees](h6images/cert-success.png)  

Tarkastetaan mille porteille on reikä palomuurissa  
*sudo ufw status verbose*  

![nähdään, että vain 20 ja 80 portit on käytössä](h6images/uwf-status-verbose.png)  

Tehdään reikä palomuuriin https portille 443. Tarkastetaan reiät palomuurissa.  
*sudo ufw 443/tcp*  
*sudo ufw status verbose*  

![tehdään reikä ja tarkastetaan, että reikä ilmestyi](h6images/uwf-allow-443-verbose.png)  

Kokeillaan toimiiko bonakota.com https protokollalla sivulla https://bonakota.com  

![https://bonakota.com avautuu ja sertifikaatti näkyy](h6images/https-lets-encrypt.png)  

Lukko osoittaa, että kyseessä on https protokolla, mutta avatessamme koko url:n todennamme https:n näkyvän myös kokonaan.  
Lukosta painaen näemme, etät kyseessä on Let's Encryptin sertifikaatti.

Testasin varmuuden vuoksi vielä toisella koneella ja puhelimella bonakota.com, www.bonakota.com, try.bonakota.com sekä support.bonakota.com kaikki toimivat.  


## b) A-rating. Testaa sivusi TLS laadunvarmistustyökalulla  


