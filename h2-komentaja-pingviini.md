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

![/home hakemisto käyttäjät](./hsimages/home-dir.png)

Näemme, että tänne on määritelty vain yksi käyttäjä hirvilampi  


###  /home/hirvilampi/

Käyttäjän hirvilampi kansio on paikassa /home/hirvilampi  
Tämä on tärkeä, koska tämä on ainoa paikka, jonne hirvilampi voi tallentaa tiedostoja  

![/home hakemisto käyttäjät](./hsimages/hirvilampi-dir.png)


### /etc/ 

Kaikki järjestelmän asetukset tiedostoina.


![esimerkki /etc/ kansion tiedoston sisällöstä](./hsimages/etx-example.png)



