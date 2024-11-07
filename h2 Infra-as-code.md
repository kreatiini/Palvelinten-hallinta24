# h2 Infra-as-code

## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot
Tähän tulee tiivistelmä 

### Tehtävänanto:
   Tähän tulee tehtävänanto
  
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

## a) Hello Vagrant!
Asensin Vagrantin Windows koneelleni jo oppitunnin jälkeen joten tässä versio:

![image](https://github.com/user-attachments/assets/0cfaaa54-e033-4371-bfbf-16b81ee344e9)


### Lähteet:
Tehtävän lähteet tähän

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
Tehtävä tuli valmiiksi kotitöiden ohella **Rannekello 21.20 7.11.2024**
### Lähteet:
Tehtävän lähteet tähän
   
## tehtävä4

### Lähteet:
Tehtävän lähteet tähän

## tehtävä5

### Lähteet:
Tehtävän lähteet tähän

## Lähteet:
   Kaikki lähteet yhteen tähän
