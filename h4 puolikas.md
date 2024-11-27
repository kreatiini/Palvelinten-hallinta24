# h4 puolikas

## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot
Olen suorittanut lähinnä tiedonhakua, tiedostot ovat hyvin keskeneräisiä vielä tässä vaiheessa. Oma moduuli muotoutuu vielä. 

### Tehtävänanto:
Puolikas. Tee ensimmäinen vedos omasta modulista. Tätä jatketaan vielä, eli valmista ei tarvitse tulla. Keskeneräisen modulin pohjalta saat vinkkejä haastaviin kohtiin ja oikeaan kehityssuuntaan. Lopullisen modulin tulee olla modernia keskitettyä hallintaa, eli idempotentti ja infraa koodina.
  
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

## Kysymyksiä:
1. Kannattaako ohjelmat asentaa käyttäen Saltia ja Vagrantin avulla asentaa vain esim micro ja salt joita ei hallita Saltilla?
2. Onko turvallista yrittää asentaa Django Saltin avulla vai parempi esim asentaa virtualenv ja luoda hakemisto omille koodeille ja sinne requirements.txt valmiiksi
3. Apachen Salt scriptin saaminen idempotentiksi(ongelma uudelleenkäynnistymisessä, jokin if ehto lisättävä)
4. Miten paljon uskaltaa asennustoimia automatisoida?

## Tavoitteet
Eli oman moduulin suunnitelma ja toivotut ominaisuudet:
- Vagrantfile jossa master ja minion valmiina Saltin käyttöön 
- Saltissa omat moduulit
  - Apache
  - Django (ehkä vain virtualenv?)
  - ufw?
- Valmiit tiedostot Apachen perus määrityksille ja Saltille suoraan master koneelle vagrantilla

### Toteutussuunnitelma
1. Vagrantfile valmistelu
2. Salt Apache2 valmistelu
3. Salt ufw valmistelu
4. Salt Django? valmistelu
5. Manuaalinen asennus
6. Automaattinen asennus

## Vagrantfile ensimmäinen versio
~~~
# -*- mode: ruby -*-
# vi: set ft=ruby :


kenraali_script = <<SCRIPT
set -o verbose
apt-get update
apt-get -y install tree curl git micro ufw
mkdir -p /etc/apt/keyrings
curl -fsSL https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public | sudo tee /etc/apt/keyrings/salt-archive-keyring.pgp
curl -fsSL https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources | sudo tee /etc/apt/sources.list.d/salt.sources
apt-get update
apt-get -y install salt-master
sleep 15
sudo systemctl restart salt-master
sleep 15
sudo salt-key -L
sudo salt-key --accept=alokas -y
sudo salt-key -L
SCRIPT

alokas_script = <<SCRIPT
set -o verbose
apt-get update
apt-get -y install tree curl git micro
mkdir -p /etc/apt/keyrings
curl -fsSL https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public | sudo tee /etc/apt/keyrings/salt-archive-keyring.pgp
curl -fsSL https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources | sudo tee /etc/apt/sources.list.d/salt.sources
apt-get update
apt-get -y install salt-minion
echo "master: 192.168.88.101" | sudo tee -a /etc/salt/minion > /dev/null
sleep 5
sudo systemctl restart salt-minion
sleep 5
sudo systemctl status salt-minion
SCRIPT

Vagrant.configure("2") do |config|
	config.vm.synced_folder ".", "/vagrant", disabled: true
	config.vm.synced_folder "shared/", "/home/vagrant/shared", create: true
	config.vm.box = "debian/bookworm64"

	config.vm.define "alokas", primary: true do |alokas|
		alokas.vm.hostname = "alokas"
		alokas.vm.network "private_network", ip: "192.168.88.102"
		alokas.vm.provision "shell", inline: alokas_script
	end

	config.vm.define "kenraali" do |kenraali|
		kenraali.vm.hostname = "kenraali"
		kenraali.vm.network "private_network", ip: "192.168.88.101"
		kenraali.vm.provision "shell", inline: kenraali_script
	end
	
end
~~~
Ongelmat: Jouduin laittamaan `sleep` komentoja demonien käynnistymisen takia. Muuten demonit eivät ehdi käynnistyä ennen avaimen kysymistä. Tämän scriptin testit löytyvät edellisen viikon [tehtävistä](https://github.com/kreatiini/Palvelinten-hallinta24/blob/main/h3%20Demoni.md).

## Apache conf tiedosto
~~~
<VirtualHost *:80>
  Alias /static/ /home/intiaani/myproject/app1/static/
  <Directory /home/intiaani/myproject/app1/static/>
       Require all granted
  </Directory>
</VirtualHost>
~~~
Tämä tiedosto siirtyy Vagrantin käynnistyessä master laitteelle.

## Salt 
Huom! Salasana korvattava omalla vahvalla salasanalla, tässä esimerkin vuoksi vain jotain.

### Apache2
~~~

apache2:
  pkg.installed

/home/intiaani/myproject/app1/static/index.html:
  file.managed:
    - contents: "Tämä on testisivu"
    - makedirs: True

/etc/hosts:
  file.append:
    - text: |
        192.168.88.102 myproject.com

/etc/apache2/sites-available/myproject.conf:
  file.managed:
    - source: salt://myproject.conf

disbale_default:
  cmd.run:
    - name: a2dissite 000-default.conf

enable_myproject:
  cmd.run:
    - name: a2ensite myproject.conf

apache2_service:
  service.running:
    - name: apache2
    - enable: True
    - watch:
        - file: /etc/apache2/sites-available/myproject.conf
~~~

### ufw + yleiset asetukset
Haasteita: ufw säännöt asetetaan komentokentästä eikä esim. suoraan `.conf` tiedostoon. 
~~~
intiaani:
  user.present:
    - name: intiaani
    - password: "JokusurkeeSalis"

ufw:
 pkg.installed

ufw.service:
  service.running:
    - name: ufw

~~~

### Virtualenv + Django
Tämän toteutus vielä pohdinnassa vahvasti
~~~
virtualenv:
  pkg.installed

/home/intiaani/myproject/app1:
  virtualenv.managed:
    - system_site_packages: True
    - requirements: salt://REQUIREMENTS.txt
    - env_vars:
        PATH_VAR: '/usr/local/bin/'
~~~
## Lähteet:
  -  Tehtävät: Karvinen 2024: Palvelinten hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/
  -  Salt Documentation: https://docs.saltproject.io/en/latest/contents.html
  -  Vagrant Documentation: https://developer.hashicorp.com/vagrant/docs
