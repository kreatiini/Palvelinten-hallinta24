# h1 Viisikko
## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot
Tehtävät olivat mielenkiintoisia. Täytyy perehtyä paremmin komentojen muodostamiseen. Omia komentoja lukuunottamatta tehtävä meni hyvin suoraviivaisesti. 
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

### Karvinen 2023: Run Salt Command Locally
Tässä artikkelissä esitellään Saltin tärkeimmät 5 state komentoa: `pkg`, `file`, `service`, `user` ja `cmd`.
Komennoilla on eri tarkoituksia joiden selitykset löytyvät kohdasta c). Saltin komennot toimivat sekä Windowsilla että Linuxilla. Paikallisesti testaaminen on nopea tapa varmistaa että Salt toimii.

### Karvinen 2018 Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux
Tässä kirjoituksessa käydään läpi nopeasti miten asentaa Salt ja luoda mestari-minioni yhteys. Yhdellä mestarilla voidaan hallita useita koneita etänä yhtäaikaisesti. Tärkeinä pointteina on konfiguraatiot jotta yhteys toimii.
- Mestarin palomuurista 4505/tcp sekä 4506/tcp auki
- minionin pitää tietää mestarin osoite ja jokaisella minionilla pitää olla yksilöllinen id/nimi.

### Karvinen 2006: Raportin kirjoittaminen
- Tee raportista toistettava niin että toisen käyttäjän on helppo tehdä täysin samat ja saada samat virheet aikaan
- Tee siitä täsmällinen, kerro kaikki komennot ja klikkailut.
- Kirjoita havainnot tapahtumista ylös
- Tee selkeä ja hyvin jäsennelty raportti
- Muista lähdeviittaukset
  
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

## c) Viisi tärkeintä **Rannekello 20.08 28.10.24**
Kaikki komennot otettu Tero Karvisen Run Salt Commands Locally- sivulta. Linkki löytyy [tästä](https://terokarvinen.com/2021/salt-run-command-locally/) sekä kappaleen lopusta.
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
   Kuvankaappauksesta näkee samat asiat mutta funktio ja lopputulos ovat erit kuin edellisessä. Lisäämällä polun ja `contents="sisältö"` muodossa komennon voidaan syöttää myös tietoa kyseiseen tekstitiedostoon. `file.absent` komennolla taas voidaan 
![image](https://github.com/user-attachments/assets/f794b11c-d1e9-4365-9680-e323f6f2a423)

Nyt `hellokreatiini` löytyy tiedostoista

![image](https://github.com/user-attachments/assets/75cb03d7-10d0-40e2-815e-4e6fea987ad7)

3. `service` komennolla voidaan käynnistää ohjelmia uudestaan mikäli asetuksia muutellaan. 
   `service.dead` komennolla tapetaan ohjelma ja `service.running` käynnistetään. Kuvankaappauksista näkyy että apache2 oli jo käynnissä omalla laitteellani. Toisella komennolla apache suljettiin joka näkyy myös kuvankaappauksessa.

   ![image](https://github.com/user-attachments/assets/9fbe14d3-54f4-430e-8fb0-699c2709f2e1)

   ![image](https://github.com/user-attachments/assets/81a0efbf-6d63-42fa-ba6a-b10762313646)

4.`user` komennolla voidaan luoda käyttäjiä mikäli sellaista käyttäjää ei ole vielä luotu. `user.present` komennolla luodaan uusi käyttäjä mikäli samannimistä käyttäjää ei vielä ole. `user.absent` komennolla poistetaan käyttäjä mikäli sellainen on olemassa. Tuloksissa ei taas paljoa analysoitavaa ole. Komento luo käyttäjän tai poistaa sen ja jos tulos on True komento onnistuu. Se kertoo myös mitä muutoksia on tehty ja luodun käyttäjän tiedot. 

![image](https://github.com/user-attachments/assets/5f9e4dfb-2e8d-40d1-b345-bed2393a2fbc)

![image](https://github.com/user-attachments/assets/77786e29-6af1-453b-9fa8-9ee84d275b7f)

5. `cmd` komennolla voidaan suorittaa komentoja esim. tiettyjen ehtojen toteutuessa. Alla oleva komento kertoo mitä komento tekee, mikä funktio on käytössä, onnistuiko luominen ja kommentit mikäli sellaiset on.
   
   ![image](https://github.com/user-attachments/assets/4495b1ac-cbb5-4073-93cf-6462f6966c55)
   
   Nyt tiedostoissa näkyy `foo`

   ![image](https://github.com/user-attachments/assets/388a9a71-b310-40eb-94cf-c5edfbc16d1f)

### Lähteet:
   Karvinen 2021: Run Salt Command Locally. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/ Luettu: 28.10.24
   Salt documentation: https://docs.saltproject.io/en/latest/ref/states/all/index.html Luettu 28.10.24
   
## d) Idempotentti. **Rannekello 20.34 28.10.24**
Idempotentti tarkoittaa kutsua tai operaatiota jolla on sama tulos riippumatta siitä kuinka monta kertaa se ajetaan. (Squareup)
Koska olin jo tappanut apache demonin aiemmin, päätin kokeilla sen tappamista uudestaan. Toistin saman komennon kolme kertaa ja `changes` kohta pysyi tyhjänä. Eli komento ei tehnyt mitään muutosta vaan tulos oli joka kerta sama. Se on siis idempotentti. Voisin esimerkiksi toistaa saman asentamallani paketilla tai poistamalla käyttäjälläni. Muutosta ei tapahtuisi. Tässä kolme kertaa:

![image](https://github.com/user-attachments/assets/27c22356-8ff2-4a6d-bc03-2f83fecf64a2)

![image](https://github.com/user-attachments/assets/2e7d81e8-5a23-488f-96b2-5a8a7674a0d3)

![image](https://github.com/user-attachments/assets/9cc0d982-6431-4b79-a1a6-30eac276a08b)


### Lähteet
   Squareup: Idempotency. Luettavissa: https://developer.squareup.com/docs/build-basics/common-api-patterns/idempotency Luettu 28.10.24
   Karvinen 2021: Run Salt Command Locally. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/ Luettu: 28.10.24
## e) Herra-orja **Rannekello 21.14 28.10.24** 
Tämän tehtävän oikea toteutustapa hieman mietitytti. Pystynkö siis ajamaan samalla laitteella komennot herrana niin että ne tapahtuvat myös minionille. Kokeillaan ainakin. Luulen että pitäisi asentaa Salt esim Windowsille tai toiselle virtuaalikoneelle. Onnistuin muuttamaan mestarin osoitteen localhostiin ja hyväksyin avaimen. Nyt kuitenkin herää kysymys ajanko todella siis herra-orja metodilla vai vain paikallisena. Tässä ainakin ensimmäisen testin tulos:

![image](https://github.com/user-attachments/assets/4744bc1d-8e94-4287-abba-a3ade7ad14d1)

Muut komennot kuitenkin herjasivat `ERROR: Minions returned with non-zero exit code`.



Ilmeisesti komentojen muodostuksessa oli häikkää sillä komento `sudo salt '*' pkg.install httpie` (Karvinen 2018) toimi hyvin: 

![image](https://github.com/user-attachments/assets/dfc405a8-d465-44f6-8eb4-a6d8d8f24b38)

Halusin kuitenkin kovasti saada jonkin itse muodostetun komennon toimimaan joten aloin perehtymään asiaan. `service.enabled` komennolla sain tietää ilmeisesti käynnistyykö apache2 automaattisesti. Jostain syystä en kuitenkaan onnistunut käynnistämään sitä. Sain saman herjan kuin aiemmin. Ehkä asetuksissani on jotain pielessä. Asetin kuitenkin localhostin masteriksi ja user kohdan kreatiini nimellä. Teron tekemät komennot kuitenkin toimivat hyvin.

![image](https://github.com/user-attachments/assets/ad58d059-2e00-4521-a31e-444204800ef3)

Omia virheilmoituksia:

![image](https://github.com/user-attachments/assets/3cb59e44-0a39-40cb-9218-6d333b66b44a)


### Lähteet:
   Karvinen 2018: Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/ Luettu: 28.10.24
   Salt documentation: https://docs.saltproject.io/en/latest/ref/states/all/index.html Luettu 28.10.24
## Lähteet:
   Tehtävät perustuvat Tero Karvisen 2024 Palvelinten hallinta kurssiin: https://terokarvinen.com/palvelinten-hallinta/
