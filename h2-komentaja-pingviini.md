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




