tehnyt Timo Lampinen, 2026, Linux palvelimet kurssi 

*Huomio tätä kannattaa silloin tällöin commitoida - varsinkin, jos tekee selaimessa, ettei kaikki häviä kun sulkee välilehden*

# Tehtävä: h2 Komentaja Pingviini

https://terokarvinen.com/linux-palvelimet/#h2-komentaja-pingviini


## Tiivistä - https://terokarvinen.com/2020/command-line-basics-revisited/

- uusia asia oli, että montaa kansiota voi luoda yhdellä komennolla
- mv komento oli myös uusi
- grep tulee varmasti kovaan käyttöö
- less on myös tärkeä


## Asenna Micro

Micron asennus kuvassa:

![asenna micro sudo apt-get install micro](./h2images/micro-asennus.png)


## Asenna kolme itsellesi uutta komentoriviohjelmaa

Etsin erilaisia ohjelmia ja löysin nämä:  
rolldice - nopanheitto ohjelma  
fd - kätevämpi kuulema kuin find  
fzf - sumealla logiikalla toimiva etsintä ohjelma, jolloin kaiken ei tarvitse olla täysin oikein kirjoitettu  

asennus:
sudo apt-get -y install rolldice fd fzf

![kuva kolmen ohjelman asennuksesta](./h2images/apt-get-install-3-programs.png)

fd ei asentunut, koska sitä ei löydy.

Tarkastetaan apt-cachesta grep käskyä hyödyntäen onko fd ohjelmaa olemassa

![apt-cachen search fd | grep "find"](./h2images/apt-cache-search-fd-etc.png)

Sen nimi on ilmeisesti (tai ainakin asennuspaketin nimi on fd-find)

asennetaan
![fd-find asennus](./h2images/install-fd-find.png)


## FHS - esittele tärkeät kansiot 

### /home/   

/home/ kansiossa näkyvät kaikkien käyttäjien kansiot  

![kansion home hakemisto käyttäjät](./h2images/home-dir.png)

Näemme, että tänne on määritelty vain yksi käyttäjä hirvilampi  


###  /home/hirvilampi/

Käyttäjän hirvilampi kansio on paikassa /home/hirvilampi  
Tämä on tärkeä, koska tämä on ainoa paikka, jonne hirvilampi voi tallentaa tiedostoja  

![hakemisto home käyttäjät](./h2images/hirvilampi-dir.png)


### /etc/ 

Kaikki järjestelmän asetukset tiedostoina.
Tässä katsomme cat käskyllä tiedoston timezone sisällön. 

![esimerkki etc kansion tiedoston sisällöstä](./h2images/etc-example.png)

Sisältö viittaa vahvasti siihen, että tämän tiedoston sisältö: *Europe/Helsinki* kertoo järjestelmälle, mikä on koneen timezone.  


## The Friendly M - esimerkkejä grep komennon käytöstä  

etsitään tietoa kissa kissa.md tiedostosta komennolla:  
grep "kissa" kissa.md  

![find |grep kissa --color](./h2images/grep-kissa-kissa-md.png)  

tässä jo aiemmin käytetty, kun fd ohjelmaa yritettiin etsia apt-cachesta. Oli hyvin todennäköistä, että kuvauksesta löytyisi myös find.  

![apt-cachen search fd | grep "find"](./h2images/apt-cache-search-fd-etc.png)

etsitään viikonpäivien alta kaikki tiedostot missä mainittu kissa ja toisella kertaa merkataan se eri väriseksi  

![find |grep kissa --color](./h2images/grep-kissa-ja-kissa-color.png)  


## Esimerkki putkista, pipe








