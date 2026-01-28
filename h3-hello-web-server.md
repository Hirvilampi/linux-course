Kirjoittanut Timo Lampinen 2026
Linux-palvelimet kurssi  - ICI003AS2A-3016

Tehtävä
# h3 Hello Web Server
  
## x) Lue ja Tiivistä
  
### https://httpd.apache.org/docs/2.4/vhosts/name-based.html  

- dokumentti kertoo milloin ja kuinka käytetään: name based virtual hosts 
- mahdollistaa usean nimipalvelun toimimisen samassa ip-osoitteesta
- ensisijaisesti nimeen perustuvaa virtuaaliserveriä etsitään ip-numeron ja portin perusteella
- useamman virtuaalihostin löytyessä tehdään valinta ServerName ja ServerAlias perusteella
- jokaisessa Virtual Host lohkossa tulisi olla vähintään ServerName ja DocumentRoot
- ServerAlias on välttämätön jos haluaa saada saman sivuston näkymään useammalla nimellä  

### https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/ 

- Sivusto antaa ohjeet, kuinka montaa eri nimistä virtuaali hostia voi ajaa samasta IP-osoitteesta
- ohjeissa käytetään komentorivikehotetta 
- opetetaan asentamaan apache2 ja tekemään kaikki perusasiat siihen pisteeseen, että tehty nettisivu näyttää halutun tekstin
- ohjeissa käydään vielä läpi, kuinka paikallisesti voidaan simuloida nimipalvelun sivua  

xx a) testaa, että web palvelimesi vastaa localhost osoitteesta

![localhost in web browser](h3images/localhosworks.png)  

## b) lokin rivit, kun avaat yhden sivun ja selitykset  

sudo tail -3 /var/log/apache2/other_vhosts_access.log  

![sudo](h3images/lokit.png)  

Ladattessa näkyy kolme lokitapahtumaa,joista ajan perusteella kaksi viimeistä liittyvät viimeisimpään lataukseen.

ensimmäinen lokitapahtuma ajankohdalla 17:46:11
hirvilampi.example.com:80  - virtuaalipalvelin ja portti
127.0.0.1 - pyyntö menee tähän ip-osoitteeseen, eli paikallisesti   
 -   remote logname, viiva koska ei annettu
 -   remote user, if the request was authenticated, tämä myös pelkkä viiva   
[28/Jan/2026:17:46:11 +0200] - Ajankohta jolloin haettua, ja lopussa paljonko aika on eri GMT verrattuna  
"GET / HTTP/1.1" - pyyntö, haetaan etusivua  
200 305 - vastaus on onnistunut ja siinä on ollut 305 merkkiä
-    verkkosivu, jotka käyttäjä tuli tälle sivulle 
Viimneinen osio kertoo tietoja haetusta järjesestelmästä

toinen lokitapahtuma ajankohdalla 17:46:11


