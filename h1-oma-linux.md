# TEHTÄVÄ H1 - LINUXIN ASENTAMINEN VIRTUAALIKONEESEEN

 Käytössä pc-pohjainen linux Debian 13. Kernel versio 6.12.63+deb13-amd64

 ## Virtualboxin asentaminen

 15:30
 Seurasin ohjeita ja selvisi, että Debian 13 mukana ei tule oletuksena. 
 Yritin seurata Oraclen sivun ohjeita, mutta tämähän meni monimutkaiseksi..
 Käytännössä nyt näyttää siltä, että ilmeisesti virtualboxista ei ole olemassa Debian 13 tukevaa versiota.
 Vaihtoehdoiksi siis jää:
 1. asentaa debian12 Bookworm
 2. asentaa m1 mac:lle virtualbox, mikä taitaa olla hankalaa sekin
 3. asentaa KVM + virt-manager

Kokeilen asentaa KVM + virt-managerin. Debian 12 asennus toiseksi olisi varmaan helpompaa, mutta ehkäpä
tämä opettaa enemmän. Katsotaan miten käy. Kysyn ChatGTP:ltä ohjeet asennukseen. 

## KVM ja Virtual Machine Manager asennus

16:13 Asennus onnistui helposti ja Virtual Machine Manager on nyt auki.

Minulla on mac:ssä BalenaEtcher ohjelma, millä tein edellisen Linuxin käynnistystikun. Sillion "tikkuna" toimi
500 gigan kovalevy. Nyt ostin usb3.0 tikun tätä varten. Latauksen pistin tulemaan tuossa jo hetki sitten. 
Kyseessä on debian-live-13.3.0-amd64.xfce.iso mistä kortille tehdään flash device

 16:18 tutustun samalla VirtualBox ohjeisiin, kun Flash Device syntyy. 
 
 ### Uuden virtual machinen luominen
 käytössä KVM ja Virtual Manager - ympäristö Linux Debian 13

 Uuden koneen luomisen nappi löytyi, nyt täytyy vain olla ISO image, jonka teko on vielä kesken.

 16:29 tämä onkin nyt hyvin erinäköinen ja ilmeisesti eri tavalla toimiva, mutta tutkitaan mit pitää valita.
 .iso levytiedosto onkin parempi valita, kuin tämä Flash device. Nopittiinpa tämäkin. 
 16:36 .iso kuva on ladattu ja päästään eteenpäin
 Nyt ollaankin antamassa koneelle jo muistimääriä ja lebynkokoa yms..

 16:40 mulla on toinen SSD levy koneessa ja yritän tehdä sille tuota virtuaalikoneelle varattua tilaa..
 Ehkä kyseessä on tuo create storage pool. Käytin sitä ja tein 40 gigan pool:n sitä varten. 

 16:43 nyt ollaankin tässä graafisessä käyttöliittymässä

 No helvetti - jotenkin se hyppäsi eteenpäin tuosta graafisesta käyttöliittymästä johonkin, joten tuhosin koko 
 homman aja aloitan alusta. Ei tää niin vaikeaa ole.

 16.48 uusi alustus

Jaahas tämä installointimenu onkin vähän erinäköinen - otan graafisen valinnan.

nimet, salasanat yms laitetaan
16.59 levyn parittiointi.. käytetään koko virtuaalilevy yhteen partitioon
Sit asennellaankin ja pitkään -- välillä on muutama valinta --
17.04 aah nyt pitääkin valita onko gnome xfce tms pr - olikohan dokumentaatiossa mitä olisi syytä käyttää 
alkutiedoissa olikin, että xfce - toisaalta sellainenhan me ladattiinkin - tai se eka lataus oli .iso versiossa taisi olla muutakin mukana
17:14 asennetaanko GRUB boot loader -> yes. Tämähän on virtuaalikone ja kaikki virtuaalinen levytilakin on määritelty tälle.
17:7 installation complete ja nyt reboot

17:19 bootti tehty ja kirjauduttu sisään -- nettiselaus ainakin toimii

17:20 tauko

17:40 sudo ap-get update -- no ei se mun peruskäyttäjän salasana toiminutkaan pitänee kokeilla root käyttäjän salasanaa
ööö nyt ei toimi root salasana, eikä hirvilammen salasana

menin root:n komennolla su -
asensin hirvilammen sudoersiin kommenolla: usermod -aG sudo hirvilampi
terminaalista ja ulos ja sisään
Sama homma jatkui, kunnes tajusin logata ulos. Restarttasin koko virtuaalikoneen varmuuden vuoksi
Perus päivitykset
17:54 firewall asennus ja restart

17:56 takaisin sisälle ja kokeillaan ohjelmia
Libreoffice Draw - ei kyllä vakuuta
Applikaatiot löytyy näklöjään täältä yläkulmasta
Teron kirjoja tuli katsottua
18:00 suurensin ikkunan koko ruudun kokoiseksi - mitenköhän tästä pääsee pois???
Shutdown .. 
18:10 no niin nyt onkin hyvä aika katsoa uudestaan mitä kaikkea piti tehdä ja huomata, 
että en ole ottanut yhtään kuvaa prosessista ja muutenkin olen kirjoittanut tätä viereisellä koneella, joten
kaikki virhe ilmoitukset ovat jääneet ottamatta talteen - tämähän menee hienosti.

Lähetin toisaalta aiemmin viestin Terolle, että voiko tehtävän tehdä KVM ja Virtual Machine Managerilla. 
En tänään torstaina kuluta enempää aikaa, jos joudunkin asentamaan vielä debian12 ja virtualboxin..

18:13 googlen mukaan virtualbox toimii debian 13:ssa.. nyt on hämmentävää. Täytyy kokeilla

## Virtualboxin asentaminen 
18:17 -> kokeilen uusia ohjeita: https://www.linuxtechi.com/how-to-install-virtualbox-on-debian/
tähän pari kuvaa 

18:25 uuden levykuvan lataus alkamaan

sit asennus ja annetut tiedot

18:40 nyt ihmettelen, että tuo ei suoraan anna tuota create virtual hard disk
- se löytyykin storagesta ja näitä tekstejä voi klikata
- luon tänne uuden 60 gigan levyn

18:45 yritin käynnistää, mutta saan virheen: KÄYNNISTÄESSÄ VIRHE: 
VT-x is being used by another hypervisor (VERR_VMX_IN_VMX_ROOT_MODE)

Kysyn ChatGTP:ltä syöttäen tuon virheen ja kysyen mikä virhe. Selviää, että koska asensin
KVM managerin, niin yritän ajaa VirtualBoxia KVM-virtuaalikoneen sisällä.. Mutta siis, 
en ole KVM sisällä ja ajamassa sieltä Virtualboxia. Tapansa mukaisesti chatgtp sekoilee taas.

Toki minua kiinnostaa, onko KVM onnistunut varaamaan nuo tiedot.. 
lsmod | grep kvm
.. jep niin on, kvm on varannut nuo.. pitänee poistaa ne ehkä kokonaan siltä

tekstejä tähän leikkuupöydältä 

19:00 Debian käynnistyi asennusta varten.. tältä illalta tää on kyllä tässä











 
 
 




 

