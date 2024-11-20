# H3 Demoni

## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot
Aloitin tehtävät Vagrant twohosts koneella. Turhauduin, koska Saltin joutui asentamaan aina uudestaan molemmille koneille. Olin järkevä ja käytin "hetken" aikaa Vagrantfilen tekemiseen. Siinä tehdään kaksi konetta, toiseen asentuu salt-minion ja toiseen salt-master. Tämän jälkeen master hyväksyy minionin avaimen automaattisesti. Näin pääsen suoraan töihin. (Tiedoston tekemiseen meni n. 1,5h aikaa joten onko fiksua ajankäyttöä oikeasti...). 

### Tehtävänanto:
- x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
  
     Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port
  
  - Artikkelissa on jonkun toisen Linux-version tiedosto. Jos tekisit samanlaisen, niin käyttäisit tietysti oman järjestelmäsi asetustiedostoa pohjana.
       
       - Silmäile Saltin ohjeet tilafunktioille pkg, file ja service. Nämä artikkelit ovat pitkiä, riittää kun luet vain johdannon ja silmäilet maintut komennot. Ei kannata yrittää opetella satoja itselle tarpeettomia parametreja ulkoa. (Less-vinkit alla)
         
        - $ sudo salt-call --local sys.state_doc pkg # johdanto + silmäile pkg.installed, pkg.purged, pkgs
           
         -   $ sudo salt-call --local sys.state_doc file # johdanto + silmäile file.managed, file.absent, file.symlink
         
        -  $ sudo salt-call --local sys.state_doc service # johdanto + silmäile service.running, service.dead, enable
 
- a) Apache easy mode. Asenna Apache, korvaa sen testisivu ja varmista, että demoni käynnistyy.

  - Ensin käsin, vasta sitten automaattisesti.
  - Kirjoita tila sls-tiedostoon.
  - pkg-file-service
  - Tässä ei tarvita service:ssä watch, koska index.html ei ole asetustiedosto
- b) SSHouto. Lisää uusi portti, jossa SSHd kuuntelee.
   - Jos käytät Vagrantia, muista jättää portti 22/tcp auki - se on oma yhteytesi koneeseen. SSHd:n asetustiedostoon voi tehdä yksinkertaisesti kaksi "Port" riviä, molemmat portit avataan.
   - Löydät oikean asetuksen katsomalla SSH:n asetustiedostoa
   - Nyt tarvitaan service-watch, jotta demoni käynnistetään uudelleen, jos asetustiedosto muuttuu masterilla
- c) Oma moduli. Valitse aihe omalle modulille. Varaa se myös kommentilla tämän kurssisivun perään. Kuvaile aihetta niin, että se yksilöi, mitä aiot tehdä. Aihesiin voi toki tulla muutoksia, kun rakennellessa oppii lisää ja paljastuu uusia yllätyksiä. (Tämä kohta ei edellytä testejä tietokoneella. Suosittelen omaa nimeä, mutta jos uskalla tai muuten halua, voit käyttää varauskommentissa etunimeä tai samaa nimimerkkiä, jota käytät läksyissä. ps. Käytä luovuutta, yleisönä ovat omat luokkakaverit. Voit vaikka viritellä jotain, mitä teet muutenkin. On nähty pelipalvelimia, Windows-työpöytiä, taiteilijan työasemaa, harjoitusmaaleja ja vaikka mitä.)
- d) VirtualHost. Asenna Apache tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.
  
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

### Lähteet:
- Tehtävän lähteet tähän

## a) Apache easy mode
### Ensin käsin
Kun olin saanut oman salt-minion ja salt-master leikkikentän valmiiksi eli automatisoitua koneiden luomisen pääsin vihdoin hommiin. Aloitin `sudo apt-get update` ja `sudo apt-get upgrade`.
`sudo apt-get install apache2`. Kurkkasin omasta Linux-palvelimet rapsastani miten oletussivu korvattiin ja tadaa:

![image](https://github.com/user-attachments/assets/cdcc2b04-99b5-41f6-86a0-7cbee5e6c245)

### Automaagista
Seuraavana poistin koneet `vagrant destroy` ja loin ne uudestaan suoraan Salt valmiudessa ;). 
- Tein moduuliani varten loogisesti kansion `sudo mkdir -p /srv/salt/apache/`
- Siirryin sinne `cd /srv/salt/apache`
- Tein init.sls tiedoston: sudoedit init.sls
- Katsoin mallia aiemmasta tehtävästä tiedoston muokkaamiseen:
- ![image](https://github.com/user-attachments/assets/f0a1f51e-d82e-457d-ae4e-395a670924a3)

- laitoin tilat tulille  `sudo salt '*' state.apply apache`
- ![image](https://github.com/user-attachments/assets/397bff25-604c-4bc5-97c0-90983f4c3f5f)
- Tulosteena tuli muutokset eli oletustiedoston sisältö ennen muutosta ja lopussa näkyy:
- ![image](https://github.com/user-attachments/assets/82b9c911-0fde-49ca-92cd-ba89c15789d1)
- Samassa kuvassa näkyy miten otin yhteyden kenraalilla alokas koneeseen ja katsoin että oletussivu oli vaihtunut


### Lähteet:
- Tehtävän lähteet tähän

## b) SSHouto
Lueskelin alkuun ohjeet ja loin tehtävää varten kansion `sshd` salt hakemistoon. Tämän jälkeen loin sinne tiedoston `init.sls`. Kopioin annetun tekstin tiedostooni. Tämän jälkeen tein uuden tiedoston `salt/` hakemistoon nimellä `sshd_config` . Sinne lisäsin portit 22 ja 1234:

![image](https://github.com/user-attachments/assets/c054af6c-3bb9-4e99-b948-13db88d9ad44)


Ajettuani komennon `sudo salt '*' state.apply sshd` sain ensin herjan

~~~~
 alokas:
Data failed to compile:
----------
   Rendering SLS 'base:sshd' failed: mapping values are not allowed here; line 3

openssh-server:
 pkg.installed
 /etc/ssh/sshd_config:    <======================
  file.managed:
     - source: salt://sshd_config
     sshd:
      service.running:
         - watch:
[...]
---
ERROR: Minions returned with non-zero exit code 
~~~~

Joten muokkasin hieman tiedoston asettelua ja sain sen toimimaan:

![image](https://github.com/user-attachments/assets/72afa955-95df-4c49-bb7f-3692787e4bce)


![image](https://github.com/user-attachments/assets/441e7a28-af29-403d-a7f3-5853bff78aa5)

![image](https://github.com/user-attachments/assets/38fa3880-4065-4b32-88b9-936ee25c9033)

Sain otettua yhteyttä `alokas` koneeseen. En kuitenkaan tiennyt sen salasanaa sillä se oli luotu Vagrantilla. Kokeilin tietysti  `vagrant`, `1234` ja paria muuta. 

![image](https://github.com/user-attachments/assets/9cc59cc8-6f9a-46ba-a264-ddb4f5697e9d)

Sama onnistui myös portista 22 ja 1234:

![image](https://github.com/user-attachments/assets/086aee0e-ae92-4dbe-8d04-bc9fe5e0f377)
![image](https://github.com/user-attachments/assets/6b20766e-aea7-4c4d-83cf-259b6b06b6d2)

### Lähteet:
- Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. Luettu 20.11.2024

## c) Oma moduli

### Lähteet:
- Tehtävän lähteet tähän
   
## d) VirtualHost
Aloitin tehtävän siirtymällä alokas koneelle. Alokkaalla loin tavallisen käyttäjän `intiaani`. 

### Lähteet:
- Tehtävän lähteet tähän

## tehtävä5

### Lähteet:
- Tehtävän lähteet tähän

## Lähteet:
  -  Tehtävät: Karvinen 2024: Palvelinten hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/
