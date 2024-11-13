# h2 Infra-as-code

## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot
Alkuun Vagrantin käyttö tuntui tönköltä ja hankalalta ymmärtää. Se alkoi kuitenkin rullaamaan nopeasti. En kohdannut tehtävän aikana yhtään ongelmia ja tehtävät avasivat Saltin toimintaa paremmin kuin ensimmäisen luennon jälkeen. Se varmasti on tarkoituskin.  

### Tehtävänanto:
-  x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva. Ei siis vaadita pitkää eikä essee-muotoista tiivistelmää.)
        Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant (Huomaa: nykyinen Debian stable on 12-Bookworm, Vagrantissa "debian/bookworm64". Vanhentunutta 11-bullseye:ta ei enää käytetä)
  -  Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux (Huomaa: Nykyisin ennen Saltin asentamista on asennettava ensin varasto [package repository], ohje h1 vinkeissä)
  -   Karvinen 2014: Hello Salt Infra-as-Code (Huomaa: kannattaa laittaa jokainen moduli omaan kansioonsa toisin kuin artikkelissani. Hyvä: "/srv/salt/hello/init.sls" eli moduli "hello" siististi omana kansionaan. Huono: "/srv/salt/hups.sls" eli sls-tiedostot ja kaikki niihin liittyvät muotit hujan hajan saltin pääkansiossa)
  - Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves, vain kohdat
            - Infra as Code - Your wishes as a text file

    - top.sls - What Slave Runs What States

     - Salt contributors: Salt overview, kohdat
    
     - Rules of YAML
     -  YAML simple structure
     -  Lists and dictionaries - YAML block structures
    
    a) Hello Vagrant! Osoita jollain komennolla, että Vagrant on asennettu (esim tulostaa vagrantin versionumeron). Jos et ole vielä asentanut niitä, raportoi myös Vagrant ja VirtualBox asennukset. (Jos Vagrant ja VirtualBox on jo asennettu, niiden asennusta ei tarvitse tehdä eikä raportoida uudelleen.)
    
    b) Linux Vagrant. Tee Vagrantilla uusi Linux-virtuaalikone.
    
    c) Kaksin kaunihimpi. Tee kahden Linux-tietokoneen verkko Vagrantilla. Osoita, että koneet voivat pingata toisiaan.
    
    d) Herra-orja verkossa. Demonstroi Salt herra-orja arkkitehtuurin toimintaa kahden Linux-koneen verkossa, jonka teit Vagrantilla. Asenna toiselle koneelle salt-master, toiselle salt-minion. Laita orjan /etc/salt/minion -tiedostoon masterin osoite. Hyväksy avain ja osoita, että herra voi komentaa orjakonetta.
    
    e) Hei infrakoodi! Kokeile paikallisesti (esim 'sudo salt-call --local') infraa koodina. Kirjota sls-tiedosto, joka tekee esimerkkitiedoston /tmp/ -kansioon.
    
    f) Aja esimerkki sls-tiedostosi verkon yli orjalla.
    
    g) Tee sls-tiedosto, joka käyttää vähintään kahta eri tilafunktiota näistä: package, file, service, user. Tarkista eri ohjelmalla, että lopputulos on oikea. Osoita useammalla ajolla, että sls-tiedostosi on idempotentti.
    
    h) Top file. Automatisoi vähintään kahden tilan / modulin ajaminen. Esim. komento 'sudo salt "*" state.apply' tai 'sudo salt-call --local state.apply' ajaa modulit "hello" ja "apache".
    
    i) Vapaaehtoinen, haastavahko tässä vaiheessa: Asenna ja konfiguroi Apache. Sen tulee näyttää palvelimen etusivulla weppisivua. Weppisivun tulee olla muokattavissa käyttäjän oikeuksin, ilman sudoa.
  
### Tietokoneen tiedot: 
- Näytönohjain: Asus GeForce RTX 3070 Ti ROG Strix - OC Edition
- Virtalähde: Corsair 750W SF Series SF750, modulaarinen SFX-virtalähde
- Emolevy: Asus ROG STRIX B550-I GAMING, Mini-ITX -emolevy
- Prosessori: AMD 5800x3D
- RAM: Corsair 32GB (2 x 16GB) Vengeance LPX, DDR4 3600MHz, CL18,
- SSD: Samsung 1TB 980 SSD-levy, M.2 2280, PCIe 3.0 x4, NVMe 1.4, sekä Kingston 1TB A2000 NVMe PCIe SSD-levy, M.2 2280, 2200/2000
- Käyttöjärjestelmä: Edition	Windows 10 Pro Version	22H2
- Virtuaaliympäristö: VirtualBox Version 7.0.14 r161095 (Qt5.15.2)
- Operating System: Debian GNU/Linux 12 (bookworm)  
- Kernel: Linux 6.1.0-25-amd64

## x) Lue ja tiivistä

### Karvinen 2021: [Two Machine Virtual Network With Debian 11 Bullseye and Vagrant](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)
- Muista tehdä hakemisto yksittäiselle projektille `mkdir <PROJEKTIN NIMI>/; cd <PROJEKTIN NIMI>/` ja luo sille `Vagrantfile`
- Varmista Config tiedoston sisältö, etenkin Linux versio
- Yhdistä oikeaan koneeseen `vagrant ssh <KONEEN NIMI>`
- Poistu komennolla `exit`
- `vagrant destroy` poistaaksesi kaikki projektin koneet
### Karvinen 2018: [Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux)
- Asenna salt-master master koneelle ja salt-minion slave koneelle
- Muokkaa slave koneen config tiedostosta masterin osoite kuntoon `sudoedit /etc/salt/minion` ja laita `master` riville master koneen osoite
- Komentojen muodostus esim. `sudo salt '*' cmd.run 'whoami'`
### Karvinen 2014: [Hello Salt Infra-as-Code](https://terokarvinen.com/2024/hello-salt-infra-as-code/)
- Asenna Salt koneille
- Tee `master` koneelle moduuli `sudo mkdir -p /srv/salt/<MODUULIN NIMI>/`
- Tee moduulin kansioon `init.sls` tiedosto
- Kirjoita haluamasi ohjeet `init.sls` tiedostoon Saltin kielellä
- Aja moduuli paikallisesti `sudo salt-call --local state.apply <MODUULIN NIMI>`
- Ajamisen jälkeen näytölle ilmestyy tiedot tehdyistä toimenpiteistä
- Varmista että komento toimii esimerkiksi `ls` komennolla mikäli loit tiedoston
- Idempotenssi komento tarkoittaa että komento ei tee muutoksia vaan haluttu tila on saavutettu
### Karvinen 2023: [Salt Vagrant - automatically provision one master and two slaves]
- Tee moduulikansio ja kansioon `init.sls` tiedosto
- Kirjoitaa `init.sls` tiedostoon YAML syntaksilla ohjeet
- Aja ohjeet minioneille komennolla `sudo salt '*' state.apply <MODUULIN NIMI>`
- `top.sls` tiedoston avulla voidaan määrittää mitä tiloja ajetaan millekkin slave koneille
- Tiedoston luomisen jälkeen pelkkä `sudo salt '*' state.apply` riittää ajamaan määritetyt tilat
### Salt contributors: [Salt overview](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml)
- **Scalars** ovat `key: value` sijoituksia. Value voi olla numero, merkkijono tai boolean.
- **Lists** `key` jonka jälkeen tulee jokainen arvo eri rivillä kahden välilyönnin ja tavuviivan kanssa.
- **Dictionaries** kokoelma `key: value` sijoituksia ja listoja.
- YAML organisoidaan block rakenteisiin
- Sisennys määrittää kontekstin. **KAKSI VÄLILYÖNTIÄ**
- Alla esimerkki:
  ```
  dinner: # Dictionary
  appetizer: shrimp cocktail # key: value1
  drink: sparkling water    # key: value2
  entree: # key
    - steak # value1
    - mashed potatoes #value2
    - dinner roll # value3
  dessert: # key
    - chocolate cake # value1

## a) Hello Vagrant!
Asensin Vagrantin Windows koneelleni jo oppitunnin jälkeen joten tässä versio:

![image](https://github.com/user-attachments/assets/0cfaaa54-e033-4371-bfbf-16b81ee344e9)


## b) Linux Vagrant
Aloitin luomisen tekemällä kansion `vagrant_kansio`. Tämän jälkeen katsoin ohjeista kuinka luodaan yksi Vagrant kone.
- Ensin komento `vagrant init debian/bookworm64`
- Seuraavana `Vagrant up`
  Tässä kohdassa Vagrant alkoi käymään läpi asetuksia ja luomaan virtuaalikonetta. Kun asennus oli ohi jatkoin eteenpäin.
- Komento `vagrant ssh` ja sain otettua ssh yhteyden laitteeseen joka näkyy komentokentästä:
  ![image](https://github.com/user-attachments/assets/6dadc3db-cf1d-42db-aec2-c294c11ef951)
- Aloin selaamaan ympäri laitetta ja testaamaan sitä eri tavoilla. Ensin siirryin juurihakemistoon:
  ![image](https://github.com/user-attachments/assets/326357da-f9d2-4bfd-90bb-c30b1ef9baba)
  Päivitin `sudo apt-get update` `sudo apt-get upgrade`
  Kokeilin pingata Googlen: `ping google.com`
  ![image](https://github.com/user-attachments/assets/481a7131-ab2d-4346-b1f8-99ada5cb04bd)
  Verkkoyhteys toimii hyvin. Loin uuden käyttäjän, vaihdoin sille, loin hakemiston ja tekstitiedoston:
  
  ![image](https://github.com/user-attachments/assets/84cddc9e-9d64-4750-a518-6eca2913493b)
- Kaikki toimii joten suljin yhteyden komennolla `exit` ja tuhosin virtuaalikoneen `vagrant destroy`
Vagrant kysyi olenko varma ja kuittasin että olen. Nyt laite on tuhottu.

### Lähteet:
Karvinen 2024: Palvelinten hallinta: h2 infra-as-a-code. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#h2-infra-as-code Luettu: 7.11.2024

## c) Kaksin kaunihimpi (**Rannekello 19.50 7.11.2024**)
Seuraavana otettiin taas askel eteenpäin ja luotiinkin kaksi konetta Vagrantin avulla. Loin ensin hakemiston `twohosts`. Ohjeissa sanottiin että luo Vagrantfile mutta ne ollut varma miten se onnistuu Windows laitteella. Verkosta löysin ohjeen `Vagrant.init` joka luo tämän tiedoston.(Sanna 2021) Sisällön kopioin Tero Karvisen ohjeesta.(Karvinen 2021) Muokkasin tekstitiedostoa Debianin uusimpaan versioon. 

![image](https://github.com/user-attachments/assets/2c08971d-4160-456d-a84e-4707ba9fc921)

Muokkauksen jälkeen ajoin komennon `vagrant up`.
Yhdistin ensimmäiseen koneeseen `vagrant ssh t001` ja pingasin toisen koneen, googlen ja katkaisin yhteyden:

![image](https://github.com/user-attachments/assets/9c64b5e9-844c-456b-a1e5-32c43c693c23)

Seuraavana toistin saman toisella koneella:

![image](https://github.com/user-attachments/assets/d457c914-169d-474e-b378-b5f06eb5f50c)

Tämän jälkeen tuhosin koneet komennolla `vagrant destroy` ja kuittasin varoituksen:

![image](https://github.com/user-attachments/assets/f2f030b3-6083-4ed8-90ab-dd64b9f1a65f)

Tehtävä tehty onnistuneesti(Karvinen 2021)
### Lähteet:
- Sanna 2021: Setting up Windows virtual test environments with Vagrant. Luettavissa: https://dev.to/sannae/setting-up-windows-virtual-test-environments-with-vagrant-4k1b#create Luettu: 7.11.2024
- Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/ Luettu: 7.11.2024

## d) Herra-orja verkossa(**Rannekello 20.06 7.11.2024**)
Päätin muokata `Vagrantfile` tiedostosta laitteiden nimiä ennen tehtävän aloitusta. Vaihdoin laitteiden nimeksi `kenraali` ja `alokas`. Selkeyttää tehtävän tekemistä ja vastausten tulkintaa. Käynnistin koneet komennolla `vagrant up` . Laitan tähän myös screenshotin tiedostosta koska muokkasin sitä:

![image](https://github.com/user-attachments/assets/5133ff07-3172-48ae-9575-310b5b937e82)


En tiedä pitäisikö Tero Karvisen copyright poistaa koska kyseessä ei ole enää puhtaasti Teron koodi vaan jotenkin lainata sitä. Jätän sen nyt kuitenkin paikalleen koska se on Teron tekemä. (Karvinen 2021)
### Alokkaan valmistelut
Yhdistin ensin `alokas` koneeseen komennolla `vagrant ssh alokas`. Aloitin ensin päivittämällä koneen `sudo apt-get update` ja `sudo apt-get upgrade`. Asensin Curlin `sudo apt-get install curl`. Tämän jälkeen aloin asentamaan Saltia ohjeen mukaan(Karvinen 2024). Antaessani komennon `sudo curl -fsSL -o /etc/apt/keyrings/salt-archive-keyring-2023.gpg https://repo.saltproject.io/salt/py3/debian/12/amd64/SALT-PROJECT-GPG-PUBKEY-2023.gpg` sain herjan `curl: (6) Could not resolve host: repo.saltproject.io`. Siirryin katsomaan Saltin dokumentaatiota jossa avaimen lataus oli muotoa `curl -fsSL https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public | sudo tee /etc/apt/keyrings/salt-archive-keyring.pgp` joten kokeilin sitä. Tein lopun asennuksen Saltin [ohjeilla](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html) (Salt). Nyt repon lisäys näytti onnistuneen.

![image](https://github.com/user-attachments/assets/86f85cb7-8485-4b29-803b-b203d65d5a28)

Asensin seuraavana Salt-minionin koneelle `sudo apt-get install salt-minion`. Asennettuani sen tajusin että minun täytyy valmistella kenraali kuten ohjeessa sanotaan. Katsoin minionin version varmistaakseni asennuksen ja poistuin komennolla `exit`.

![image](https://github.com/user-attachments/assets/401a8fbd-cf14-4d03-bfe2-c9ae5bb07263)

### Herra kenraalin valmistelut
Toistin aiemmin tehdyt toimenpiteet `kenraali` koneelle. Erotuksena asensin Salt-masterin:

![image](https://github.com/user-attachments/assets/46feb40a-a938-4f54-975b-316b004fd8f9)
![image](https://github.com/user-attachments/assets/2860af0a-ee63-499c-8fc8-a54f379bae90)

### Alokkaan valmistelut osa2
Siirryin takaisin alokas koneen kimppuun `vagrant ssh alokas`. 
Laitoin alokkaalle kenraalin hostiksi ja nimesin alokkaan `sudoedit /etc/salt/minion` :

![image](https://github.com/user-attachments/assets/b3d15e6f-abda-41bf-941f-a48e7d8c6583)
![image](https://github.com/user-attachments/assets/0ab015d8-7456-47db-9923-065e1f8e1223)

Tämän jälkeen käynnistin minionin uudestaan `sudo systemctl restart salt-minion` ja poistuin `exit`

### Avaimen hyväksyminen ja testailu
Ajoin seuraavan komennon kenraalilla `sudo salt-key -A`. 
Sain herjan `The key glob '*' does not match any unaccepted keys.` Kävin tarkistamassa aiemmin muokatun tiedoston jossa tiedot olivat oikein. Käynnistin minionit taas uusiksi ja kokeilin, edelleen sama vaiva. `ping` komento alokkaaseen ja alokkaasta kenraaliin toimii. 
Kävin kommentoimassa `id` kentän alokas koneella ja käynnistin minionin uusiksi. Nyt sain avaimen toimimaan:

![image](https://github.com/user-attachments/assets/78cc5275-9309-4057-b712-afbb6ff4fd03)

Tämän jälkeen kokeilin yksinkertaista komentoa `sudo salt '*' cmd.run 'whoami'` ja sain vastauksen: 
![image](https://github.com/user-attachments/assets/6ce61fab-62c4-4963-8563-a76232314fe7)
Komennot siis toimivat. 
Tehtävä tuli valmiiksi kotitöiden ohella **Rannekello 2120 7112024**
### Lähteet:
- Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/ Luettu: 7.11.2024
   
## e) Hei infrakoodi! (**Rannekello 1555 12112024**)
Aloitin käynnistämällä molemmat koneet komennolla `vagrant up`. Yhdistin master koneeseen komennolla `vagrant ssh kenraali`. Tämän jälkeen loin tarvittavat kansiot `sudo mkdir -p /srv/salt/hello/` ja siirryin kansioon `cd /srv/salt/hello/`.
Loin tiedoston `sudoedit hello.sls` ja laitoin sisällön: 

![image](https://github.com/user-attachments/assets/4ef40f63-7e24-4d00-9139-e0eb143ca65e)

Ajoin paikallisesti komennolla `sudo salt-call --local state.apply hello`. Vastaus oli:

![image](https://github.com/user-attachments/assets/31e0b821-adce-44d2-9fde-6bea8e3f47e4)

Tämän jälkeen kävin katsomassa kansiosta:

![image](https://github.com/user-attachments/assets/a9e746f8-961d-4d53-9a74-87ffc5a39575)

Eli tiedosto luotiin onnistunueesti. (**Rannekello 1604 12112024**)
### Lähteet:
- Karvinen 2024: Hello Salt Infra-as-Code. Luettavissa: https://terokarvinen.com/2024/hello-salt-infra-as-code/ Luettu 12.11.2024

## f) Aja esimerkki sls-tiedostosi verkon yli orjalla
Annoin komennon `sudo salt '*' state.apply hello` ulkomuistista. Tulos oli seuraava:

![image](https://github.com/user-attachments/assets/42b0d24a-a6ec-4ded-b996-7624ae996381)

Seuraavana vaihdoin nopeasti `alokas` koneelle katsomaan tilannetta:

![image](https://github.com/user-attachments/assets/d94a56b0-b779-4259-ad68-7181c23e9235)

ja boom tiedosto luotu. 

## e) tuplafunktiot (**Rannekello 1611 12112024**)
Seuraavana piti tehdä `.sls` tiedosto joka käyttää vähintään kahta tilafunktiota. Päätin käyttää `service` ja `package` tilafunktioita. 
Aloitin luomalla uuden hakemiston tiedostolle `sudo mkdir tupla` ja tein sinne tiedoston `sudoedit init.sls`. Katselin Saltin dokumentaatiosta mallia tekstin kirjoitusmuotoon ja päädyin seuraavaan:

![image](https://github.com/user-attachments/assets/cbac47be-8245-4136-8185-d6934ba5de9d)

Jonka ymmärtääkseni pitäisi toimia. Ajoin `sudo salt '*' state.apply tupla`. Sain seuraavan vastauksen:

![image](https://github.com/user-attachments/assets/e73a73cc-c42f-4753-8e77-c400175db263)

Tämä siis  asensi Apachen ja asennuksen jälkeen Apache oli jo käynnistynyt itsestään ennen `service.running` ajamista. Ajoin komennon 3 kertaa: 

![image](https://github.com/user-attachments/assets/1693d36d-88d4-4ff8-bd8b-4b871bd05ea7)

Ei muutoksia. Eli tiedosto on idempotentti. Seuraavana siirryin alokkaalle tarkistamaan onko apache päällä ja asennettu:

![image](https://github.com/user-attachments/assets/d693a674-84d1-4801-a07d-0d62984d0be4)
![image](https://github.com/user-attachments/assets/f3325abf-67b8-408e-a523-dbe4e89d7099)

Tästä näkee vielä että Apache käynnistynyt samaan aikaan kuin ensimmäinen annettu `tupla` komento:
![image](https://github.com/user-attachments/assets/01fc29e0-631d-4af0-8e57-7888c3a4c006)
Kello on väärin kenraali ja alokas koneissa.
### Lähteet:
- Salt documentation: States tutorial part 1 - Basic Usage. Luettavissa: https://docs.saltproject.io/en/latest/topics/tutorials/states_pt1.html Luettu: 12.11.2024
- Gite 2024: Linux how long a process has been running?. Luettavissa: https://www.cyberciti.biz/faq/how-to-check-how-long-a-process-has-been-running/ Luettu 12.11.2024

## e) Top file (**Rannekello 1654 12112024**)
Aloitin luomalla tiedoston `top.sls` hakemistoon `/srv/salt/` eli samaan paikkaan missä muut moduulit ovat. Tämän jälkeen kirjoitin sisällön:

![image](https://github.com/user-attachments/assets/f68ded88-b6d6-4113-a178-7ea94d6361b0)

ja ajoin komennolla `sudo salt "*" state.apply`. Tuloksena oli:

![image](https://github.com/user-attachments/assets/0a0653d1-29bd-4c7f-86a5-0a961a93b322)

Eli komento toimii ja on idempotentti.

### Lähteet:
-  Salt documentation: States tutorial part 1 - Basic Usage. Luettavissa: https://docs.saltproject.io/en/latest/topics/tutorials/states_pt1.html Luettu: 12.11.2024
## Lähteet:
   -  Salt documentation: States tutorial part 1 - Basic Usage. Luettavissa: https://docs.saltproject.io/en/latest/topics/tutorials/states_pt1.html Luettu: 12.11.2024
   -  Gite 2024: Linux how long a process has been running?. Luettavissa: https://www.cyberciti.biz/faq/how-to-check-how-long-a-process-has-been-running/ Luettu 12.11.2024
   -  Karvinen 2024: Hello Salt Infra-as-Code. Luettavissa: https://terokarvinen.com/2024/hello-salt-infra-as-code/ Luettu 12.11.2024
   -  Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/ Luettu: 7.11.2024
   -   Sanna 2021: Setting up Windows virtual test environments with Vagrant. Luettavissa: https://dev.to/sannae/setting-up-windows-virtual-test-environments-with-vagrant-4k1b#create Luettu: 7.11.2024
   -   Karvinen 2024: Palvelinten hallinta: h2 infra-as-a-code. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#h2-infra-as-code Luettu: 7.11.2024
   -   Tehtävät perustuvat kurssiin Palvelinten hallinta(Karvinen 2024) Tehtävät: https://terokarvinen.com/palvelinten-hallinta
