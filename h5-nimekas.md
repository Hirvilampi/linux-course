Kirjoittanut Timo Lampinen 2026  
Linux-palvelimet kurssi - ICI003AS2A-3016  
Tehtävä h5 sivulta: https://terokarvinen.com/linux-palvelimet/  

# Tehtava H5 Nimekäs

## a) Nimi. Laita julkinen nimi osoittamaan omaan koneeseesi.  


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
  
Sivu alkoi heti näkymään netissä osoitteessa bonakota.com  

  ![namecheap bonakota.com timo's page](h5images/bonakota-com-timos-page.png)  

Kokeilin myös kännykällä ja sivu näkyy siellä samalla tavalla. 
Lisäksi kokeilin www.bonakota.com ja se toimii myös.  

## b) Alidomain. Tee kaksi uutta alidomainia.

Tein uuden alidomainin domain list:n kautta bonakota.com Namecheapin kautta.  
Uuden alidomainin nimi on try.bonakota.com

![alidomain a-record try.bonakota.com](h5images/bonakotas.png) 

Tämä ei varmaankaan vielä toimi näin, mutta testataan:  

![try.bonakota.com netti näyttää tyhjää](h5images/bonakotas.png) 

Ei toiminut. Tämä pitää varmasti lisätä .conf tiedostoon.  
Ehkä kuitenkin on syytä etsiä jokin lähde, missä asia selitetään paremmin.  
Lähteeksi löytyi: https://www.eksis.one/artikkelit/apache2/apache2-ja-alidomain/

Tehdään ensin uusi hakemisto polkuun  
*/home/timo/publicsites/*  
ja lisätään sinne index.html  

kuva  

Käydään sen jälkeen luomassa uusi .conf tiedosto  

kuva siirtymäst ja uuden sivun sisällöstä - ei toimi vielä  

Poistin try.bonakota.com tiedostosta serveraliaksen ja muokkasin *ServerName try.bonakota.com*  
Tämä alkoi toimimaan.







## Lähteet  

EksisONE 2012: https://www.eksis.one/artikkelit/apache2/apache2-ja-alidomain/  

