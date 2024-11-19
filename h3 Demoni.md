# H3 Demoni

## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot
Tähän tulee tiivistelmä 

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

## tehtävä1

### Lähteet:
- Tehtävän lähteet tähän

## tehtävä2

### Lähteet:
- Tehtävän lähteet tähän

## tehtävä3

### Lähteet:
- Tehtävän lähteet tähän

## tehtävä3

### Lähteet:
- Tehtävän lähteet tähän
   
## tehtävä4

### Lähteet:
- Tehtävän lähteet tähän

## tehtävä5

### Lähteet:
- Tehtävän lähteet tähän

## Lähteet:
  -  Tehtävät: Karvinen 2024: Palvelinten hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/
