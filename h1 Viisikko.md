x)  
Karvinen 2025: Install Salt on Debian 13 Trixie  
-
- Tässä kerrotaan, miten Salt asennetaan Debian koneellesi.
- Tarvitaan paljon luottoa, jos annat ulkoisen tahon asentaa binääritedoston laitteellesi.
- Saltin toimivuutta testataan.
+ Artikkelin alussa on linkki nimeltä "Too short summary", joka vie sivun pohjalle ja näyttää hyvin tiivistetysti, mitä tehdä.

Karvinen 2023: Run Salt Command Locally  
-
- Aiheena on Salt komentojen suorittaminen paikallisesti.
- Asennetaan Salt-orjademoni, ja tälle säädetään asetuksia.
+ Syy miksi komentoja tehdään paikallisesti on se, että tulokset nähdään välittömästi, joka sopii harjoitukseksi.

Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux  
-
- Nopea ohje Saltin käyttöön
- Lyhyesti: Asenna mestari ja orja. Hyväksy orja-avain mestarilla. Tämän jälkeen testaa toimivuus.
+ Tämän mukaan vain pääpalvelin tarvitsee tunnetun osoitteen, mutta orjapalvelimet eivät.

Karvinen 2006: Raportin kirjoittaminen  
-
- Ohjeistus raporttien kirjoittamisesta kurssilla.
- Tärkeää on sinun lopputuloksesi toistuminen, jos joku muu tekisi tismalleen samoin.
- Tekemäsi komennot, klikkaukset ja kellonajat on näytettävä.
- Oudot tai epäonnistuneet tulokset on kirjattava.
- Lähteet on oltava, jos niitä on käytetty.
+ Artikkelin tarkoitus on kertoa tärkeimmät seikat kirjoittamisesta. Ei pidä kirjoittaa raamatun verran tekstiä, mutta tekstisi on oltava yksityiskohtainen.

a) Debian 13 Trixie asennuksessa ei ongelmia.  
b)  
18:12 sudo apt-get update  
18:15 VIRHE: "admin1 is not in the sudoers file"  
18:24 su -  
18:26 usermod -aG sudo admin1  
18:26 groups admin1  
18:28 exit  
18:29 sudo apt-get update  
18:29 VIRHE: "admin1 is not in the sudoers file"  
18:32 su -  
18:32 whoami  
18:34 groups admin1  
18:34 apt update  
18:35 apt install sudo
18:40 apt-get install wget  
18:43 mkdir saltrepo/ 
18:43 cd saltrepo/  
18:49 wget https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public  
18:51 wget https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources  
18:53 less salt.sources  
19:09 cp public /etc/apt/keyrings/salt-archive-keyring.pgp  
19:09 cp salt.sources /etc/apt/sources.list.d/  
19:10 apt-get update
19:11 apt-get install salt-minion salt-master
19:14 salt --version  
19:28 salt-call --local state.single file.managed /tmp/hellotero file  
19:29 ls /tmp/hellotero  
19:30 exit  
19:30 exit  

c) abc  
d) abc  
