Kirjoittanut Timo Lampinen 2026  
Linux-palvelimet kurssi - ICI003AS2A-3016  
Tehtävä h5 sivulta: https://terokarvinen.com/linux-palvelimet/  

# Tehtava H5 Nimekäs

## a) Nimi. Laita julkinen nimi osoittamaan omaan koneeseesi.  
  
Hankin nimen bonakota.com NameCheapin kautta. Nimeksi valitsin tuon, koska teen yhtä projektia tuolla  
nimellä.  

![namecheap bonakota.com](h5images/bonakota.png)  
  
![namecheap bonakota.com oder](h5images/bonakotadomain.png)   

  ![namecheap bonakota.com pay](h5images/bonakotapay.png)  


Menin omaan accountiin ja sieltä domain list kohtaan sivupalkista.  
Täällä näemme bonakota.com ja valitsemme manage.  
  
  ![namecheap bonakota.com domain list manage](h5images/bonakota-manage.png)  


Menin suoraan Advanced DNS välilehdelle ja poistin vanhat recordit.  
Kuvassa näkyy tyhjä record lista.  

  ![namecheap bonakota.com removed old DNS records](h5images/bonakota_old_rec_rm.png)  

Tämän jälkeen lisäsin kaksi a-record, host ja value ja päivitysnopeus välimuistiin.

  ![namecheap bonakota.com new records](h5images/bonakota-add-new-records.png)  
  
Kopioin vanhan timo.example.com.conf pohjaksi bonakota.conf tiedostolle ja muokkasin siihen oikeat tiedot.  
Tämän jälkeen poistin vanhan .conf käytöstä, otin uuden käyttöön ja käynnistin apache2:n uudestaan.

![make bonakota.conf and ensite it. Then restart server](h5images/bonakota-uusi-conf.png)  

Sivu alkoi heti näkymään netissä osoitteessa bonakota.com  

  ![namecheap bonakota.com timo's page](h5images/bonakota-com-timos-page.png)  

Kokeilin myös kännykällä ja sivu näkyy siellä samalla tavalla. 
Lisäksi kokeilin www.bonakota.com ja se toimii myös.  

## b) Alidomain. Tee kaksi uutta alidomainia.  

Tein uuden alidomainin domain list:n kautta bonakota.com Namecheapin kautta. 
Tämä tehtävän mukaisesti A Record:a käyttäen.  Uuden alidomainin nimi on try.bonakota.com

![Added A Record try.bonakota.com on 185.20.138.164 on DNS HOST records](h5images/bonakota-try.png) 

Tämä ei varmaankaan vielä toimi näin, mutta testataan:  

![try.bonakota.com netti näyttää tyhjää](h5images/bonakota-try-test.png) 

Ei toiminut. Pitänee lisätä try.bonakota.com .conf tiedostoon.  

![lisätään bonakota.conf tiedostoon serveralias try.bonakota.conf](h5images/bonakota-conf-try.png) 

Tämäkään ei auta ja virheilmoitus on sama kuin aiemmin.  
Ehkä kuitenkin on syytä etsiä jokin lähde, missä asia selitetään paremmin.  
Lähteeksi löytyi: https://www.eksis.one/artikkelit/apache2/apache2-ja-alidomain/

Sivujen erottamiseksi toisistaan, haluan tehdä sivulle oman index.html tiedoston.  
Tehdään ensin uusi hakemisto polkuun  
*/home/timo/publicsites/*  ja lisätään sinne *index.html*    


![tehdään try/ hakemisto](h5images/bonakota-try-dir.png) 
![luodaan index.html](h5images/bonakota-try-index.png) 
![bonakota.conf serveralias try.bonakota.com](h5images/bonakota-conf-try-alias.png) 

En vieläkään saa sivua try.bonakota.com latautumaan. Selaimen konsolista ei myöskään ollut suuresti apua.  

![web konsoli try.bonakota.com](h5images/bonakota-try-console.png) 


Tutkin lisää ja tarkemmin lähdesivua.  
try.bonakota.com pitääkin määritellä ServerName, eikä alias. Se siis tarvitsee oman .conf tiedoston.  
Vaihtoehtoisesti sen voisi lisätä bonakota.conf tiedoston perään omana uutena VirtualHost:na, mutta  
oma try.bonakota.conf tiedosto mahdollistaa virtualhostien ensite ja dissite tekemisen erikeen. 

Käydään sen jälkeen luomassa uusi try.bonakota.conf tiedosto.  

![try.bonakota.com ei lataudu vieläkään](h5images/bonakota-try-test.png) 

Hemmetti - eihän tämä toimi vieläkään.  
Poistin try.bonakota.com tiedostosta serveraliaksen ja muokkasin *ServerName try.bonakota.com*  
Tämä alkoi toimimaan.  

![working try.bonakota.conf servername try.bonakota.com](h5images/bonakota-try-conf.png) 
![a2ensite try.bonakota.conf](h5images/bonakota-ensite-try.png) 
![try.bonakota.com latautuu](h5images/bonakota-try-works.png) 

Miksi näin? Tulin siihen tulokseen, että try.bonakota.com täytyy olla omana ServerName määritelty,  
koska se osoittaa omaan hakemistoon. Mikäli try.bonakota.com osoittaisi samaan hakemistoon kuin  
bonakota.com, silloin se voisi olla määritelty ServerAliaksena. Tämä käy järkeen, sillä ServerName ja
ServerAlias on osoitettava samaan polkuun.  
Päättelyn lisäksi on löysin saman tiedon myös Apachen dokumentaatiosta:  
https://httpd.apache.org/docs/current/vhosts/name-based.html?utm_source=chatgpt.com

Mielenkiinoinen yksityiskohta.  Apache lukee .conf tiedostot aakkosjärjestyksessä, joten jos aiemmin  
aakkosjärjestyksessä olevasta lokista löytyy etsintään kelpaava vastaus, se käytetään ja näytetään.  
Tämän vuoksi default loki on nimeltään 000-default.conf.  On siis tärkeää muistaa tämä jatkossa, jos  
VirtualHost:ja on käytössä enemmänkin.

CNAMEn lisääminen. 

CNAME eroaa A Recordista siten, että siinä DNS tunnusta käytetään aliaksena toisella domain nimelle.
Tämä eroaa A Recordista käytännössä niin, että samalla kun A Record laitetaan osoittamaan suoraan  
IP osoitteeseen (kuten 185.20.138.164), laitetaan CNAME osoittamaan domain nimeen (bonakota.com).  

CNAME suurin hyöty on yksinkertaistaa kokonaisuuden hallintaa 

Lähde: https://dnsmadeeasy.com/resources/cname-records-explained  

Lisäsin CNAME tiedon DNS tietoihin nimipalvelussa ja .conf tiedostoon.

KUVA-lisätty nimi palveluun namecheap cname
![](h5images/bonakotas.png) 

KUVA - bonakota.conf
![](h5images/bonakotas.png) 

Sivu ei kuitenkaan heti latautunut.  

KUVA - error 
![](h5images/bonakotas.png) 

Tämä oli outoa, koska ping ja curl sivusta toimivat.  

KUVA ping curl  
![](h5images/bonakotas.png) 

Toisella laitteella tämä kuitenkin toimi ja lopulta sivu latautui myös tässä koneella.  

KUVA - TOINEN LAITE
![](h5images/bonakotas.png) 

KUVA - support.bonakota.com
![](h5images/bonakotas.png) 








## Lähteet  

EksisONE 2012: https://www.eksis.one/artikkelit/apache2/apache2-ja-alidomain/  
Apache: https://httpd.apache.org/docs/current/vhosts/name-based.html?utm_source=chatgpt.com
