Kirjoittanut Timo Lampinen 2026  
Linux-palvelimet kurssi - ICI003AS2A-3016  
Tehtävä h6 sivulta: https://terokarvinen.com/linux-palvelimet/  

# Tehtava H6 Salataampa

## x) Lue ja tiivistä  

Let's Encrypt 2024: How it works (https://letsencrypt.org/how-it-works/)  
- ensimmäisessä vaiheessa tarkastetaan domainin hallinta. Luotuja salausavainpareja käyttäen Let's Encrypt tarkastaa haasteella, että domain on hallussa
- seuraavaksi tarkastetaan, voidaanko haasteet suorittaa useasta verkkonäkökulmasta
- Tämän jälkeen olla valmiita antamaan sertifikaatti. Client rakentaa pyynnön (CSR) Let's Encryptille myöntää sertifikaatti. Let's Encrypt tarkastaa, että CSR:ssä ja domainissa käytetään valtuutettuja salausavaimia. Jos kaikki täsmää sertifikaatti myönnetään.
- Let's Encrypt jakaa tiedon sertifikaatista eteenpäin.
- Sertikaatin poistossa tarvaitaan salausavainpari ja Let's Encrypt vahvistaa, että pyyntö on authorisoitu.

The Apache Software Foundation 2025: Apache HTTP Server Version 2.4 [Official] Documentation: SSL/TLS Strong Encryption: How-To: (https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample)  
-  Esitellään perus SSL konfiguraatio Apache HTTP serverissä HTTPS-yhteyksiä varten
-  Kuvataan erilaisten salausalgoritmien käyttöä sekä näytetään kuinka vahvat ja suorityskykyiset salausasetukset määritellään
-  Selitetään OCSP Stapling-mekanismi, jolla tarkastetaan onko sertifikaatti peruttu
-  Kerrotaan kuinka sertifikaatteja käytetään clientien kanssa erilaisissa tilanteissa. Voi olla esimerkiksi mahdollista, että osaan serveristä pääsee pelkällä HTTP yhteydellä, mutta tiettyihin osiin vaaditaan HTTPS yhteys

## a) Let's - asenna palvelimellesi ilmainen TLS-sertifikaatti Let's Encryptilta. Osoita, että se toimii.  

Kirjaudun ensin sisään palvelimelle  ja varmistetaan, että daemon apache2 on käynnissä  
*ssh timo@185.20.138.164*  
*sudo systemctl restart apache2*  

![ssh ja update toimivat](h6images/ssh-update.png)  
  

Tarkastetaan web-sivun näkyvyys lataamalla bonakota.com.
Toimii tällä koneella, sekä toisella koneella. 

![http://bonakota.com latautuu](h6images/bonakota-works.png)  

Ensin update palvelimen ohjelmistolle  
*sudo apt-get update*  

Asennan palvelimelle certbot:n, python3-certbot, python3-certbot-apache
*sudo apt install certbot*  
*sudo apt install python3-certbot*  
*sudo apt install python3-certbot-apache*  

![install certbot](h6images/inst-certbot.png)  
![install python3-certbot ja python3-certbot-apache](h6images/python-certbot-apache.png)  

Käynnistetään certbot ja annetaan sen haluamat tiedot   
*sudo certbot*  

![sudo certbot alkaa](h6images/sudo-certbot.png)  
![succees](h6images/cert-success.png)  

Setifikaatit saatiin asennettua kaikille neljälle sivulle. 

Tarkastetaan mille porteille on reikä palomuurissa  
*sudo ufw status verbose*  

![nähdään vain portit 22 ja 80](h6images/uwf-status-verbose.png)  

Tehdään reikä palomuuriin https portille 443. Tarkastetaan reiät palomuurissa.  
*sudo ufw allow 443/tcp*  
*sudo ufw status verbose*  

![tehdään reikä ja tarkastetaan, että reikä ilmestyi](h6images/uwf-allow-443-status.png)  

Kokeillaan toimiiko bonakota.com https protokollalla sivulla https://bonakota.com  

![https://bonakota.com avautuu ja sertifikaatti näkyy](h6images/https-lets-encrypt.png)  

Lukko osoittaa, että kyseessä on https protokolla, mutta avatessamme koko url:n todennamme https:n näkyvän myös kokonaan.  
Lukosta painaen näemme, etät kyseessä on Let's Encryptin sertifikaatti.

Testasin varmuuden vuoksi vielä toisella koneella ja puhelimella bonakota.com, www.bonakota.com, try.bonakota.com sekä support.bonakota.com kaikki toimivat.  


## b) A-rating. Testaa sivusi TLS laadunvarmistustyökalulla  

Testataan bonakota.com osoitteessa www.ssllabs.com  

![received a A rating from SSL Labs ](h6images/ssl-labs-bonakota.png)  

Näyttää toimivan. Toki DNS CAA tuottaa vastauksen no. Katsoessa infoa selviää, ettei CAA ole vielä monellakaan nettisaitilla käytössä. 
Raportissa on useampi sivu, jotka kertovat lisää tietoa. Tässä pieni näyte:

![TLS sertifikaatiti ja mm missä handshake on toiminut ja missä ei](h6images/tls-handshake.png)  
![safari ja ios joissa handshake ei toimi](h6images/handshake-no-2.png)  

Huomaamme että sivulla ovat voimassa protokollat TLS 1.2 ja TLS 1.3.   
On mielenkiintoista huomata myös, että monella handshake-simulaatio toimii, mutta Chrome 49 + window XP Service Pack 3 kokonaisuudessa ei toimi. Myös Safarin muutamat versiot vanhoilla iOS käyttöjärjestelmillä, eivät onnistu handshake testissä. 

Tuo DNS CAA jäi mietityttämään. Niinpä aloin lukemaan löytyisikö Giang:n ratkaisusta jotain apua.  https://github.com/gianglex/Courses/blob/main/Linux-Palvelimet/h6-salataampa.md

Kokeilen lisätä DNS CAA palvelimen tietoja nimipalvelimelle, saisiko sillä muutettua DNS CAA arvoa.

![DNS CAA settings issuewild](h6images/caa-issuewild.png)  

Katsotaan mikä on tulos SLS Labs:n testissä

![DNS CAA no on SLS Labs](h6images/sls-dns-caa-no.png)  

Sls Labs antaa edelleen tiedon, ettei CAA tietoa näy. 
Kokeilen mitä dig antaa komennolla  
*dig CAA bonakota.com"  

![dig caa bonakota toimii](h6images/dig-caa-bonakota.png)  

Dig kertoo, että CAA on näkyvillä, mutta SLS Labs:n testi antaa silti no. Lopetan tältä päivältä.  

Seuraavan päivän SLS Labs ajo antaa DNS CAA ok tuloksen.  

![sls caa bonakota toimii](h6images/sls-labs-caa-ok.png)  

On näköjään tärkeä huomata, että joskus tietojen päivittymienn voi kestää pitkään.  
Mietin myös, että olisi ollut hyödyllistä ajaa testi toisella koneella tai edes selaimella.  
Voisiko kyseessä olla välimuistissa olevat tiedot, vaikka teinkin latauksen aina painamalla Clear Cache nappia SLS Labsssa.  



# Lähteet 
Let's Encrypt, 2024. How It Works: https://letsencrypt.org/how-it-works/  
TThe Apache Software Foundation, 2025. Apache HTTP Server Version 2.4 – SSL/TLS Strong Encryption: How-To: https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html  
Qualys SSL Labs. SSL Server Test:  https://www.ssllabs.com/ssltest/  
Tero Karvinen. Linux-palvelimet – Tehtävä H:. https://terokarvinen.com/linux-palvelimet/  
Giang 2025: https://github.com/gianglex/Courses/blob/main/Linux-Palvelimet/h6-salataampa.md
