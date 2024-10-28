# h1 Viisikko
## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot
Tähän tulee tiivistelmä 
### Tehtävänanto:
   x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva. Ei siis vaadita pitkää eikä essee-muotoista tiivistelmää.)
  
   Karvinen 2023: Run Salt Command Locally
        
   Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux
        
   Karvinen 2006: Raportin kirjoittaminen
        
   Saltin asennus edellyttää nykyään (Debian 12 Bookworm) uuden pakettivaraston asentamista, mitä ei käsitellä näissä artikkelissa. Ohjeet pakettivaraston asentamiseen vinkeissä alla.
        
  a) Asenna Debian 12-Bookworm virtuaalikoneeseen. (Poikkeuksellisesti tätä alakohtaa ei tarvitse raportoida, jos siinä ei ole mitään ongelmia. Mutta jos on ongelmia, sitten täsmällinen raportti, jotta voidaan ratkoa niitä yhdessä.)
  
  b) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi).
  
  c) Viisi tärkeintä. Näytä Linuxissa esimerkit viidestä tärkeimmästä Saltin tilafunktiosta: pkg, file, service, user, cmd. Analysoi ja selitä tulokset.
  
  d) Idempotentti. Anna esimerkki idempotenssista. Aja 'salt-call --local' komentoja, analysoi tulokset, selitä miten idempotenssi ilmenee.
  
  e) Herra-orja. Kokeile herra-orja arkkitehtuuria niin, että herra ja orja ovat samalla koneella.
  
### Tietokoneen tiedot: 
- Näytönohjain: Asus GeForce RTX 3070 Ti ROG Strix - OC Edition
- Virtalähde: Corsair 750W SF Series SF750, modulaarinen SFX-virtalähde
- Emolevy: Asus ROG STRIX B550-I GAMING, Mini-ITX -emolevy
- Prosessori: AMD 5800x3D
- RAM: Corsair 32GB (2 x 16GB) Vengeance LPX, DDR4 3600MHz, CL18,
- SSD: Samsung 1TB 980 SSD-levy, M.2 2280, PCIe 3.0 x4, NVMe 1.4, sekä Kingston 1TB A2000 NVMe PCIe SSD-levy, M.2 2280, 2200/2000
- Käyttöjärjestelmä: Edition	Windows 10 Pro Version	22H2

## x) Lue ja tiivistä
## a) Asenna Debian
Debianin asennuksessa ei tullut ilmi ongelmia
## b) Asenna Salt Linuxille **Rannekello 1534 28.10.24**
Olin jo lukenut läpi kohdan x) sivut ja aloitin selvittämään kuinka Salt asennetaan. Loin ensin hakemiston Saltin avaimen ja lisäsin Saltin repositorion listalle. Tämän jälkeen päivitin paketit:

![image](https://github.com/user-attachments/assets/28975f50-25eb-4b8e-a6aa-ad0772ce3559)

Tämän jälkeen oli aika asentaa Salt-minion laitteelleni `sudo apt-get -y install salt-minion`: 

¨![image](https://github.com/user-attachments/assets/1f1ecf4c-875f-4df3-8cfe-541050502472)

 ja varmistin asennuksen sekä version:

 ![image](https://github.com/user-attachments/assets/b576b2a1-a937-4755-9ab1-00fe78442be3)

Käynnistin Salt minionin ja katsoin prosessilistauksesta että se käynnistyy taustalle:

![image](https://github.com/user-attachments/assets/8cd6fe47-6e28-4cdb-b0fd-fa3df23dec7a)

### Lähteet:
Karvinen 2018: Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

Salt documentation: https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/debian.html

## c) Viisi tärkeintä
1. `pkg` komennolla hallitaan pakettien asennusta. Tein kuten esimerkissä on tehty (Karvinen 2021) ja asensin sovelluksen `tree` :
   Kuvankaappauksesta näkee eri asioita:
   **ID** paketin nimi
   **Function** mikä komento
   **Comment** mitä tehtiin
   **Started** milloin aloitettiin
   **Duration** kauanko kesti
   **total states run** montako toimenpidettä tehtiin
   **new** ja **old** uusi ja edellinen versio sovelluksesta
   ![image](https://github.com/user-attachments/assets/c330c4c1-bba9-4848-9f4b-1d4dd6e3fda6)

2. `file` komennolla hallinnoidaan tiedostoja. 

