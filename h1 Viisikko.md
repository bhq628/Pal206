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

a) Asenna Debian 13-Trixie virtuaalikoneeseen. Debian 13 Trixie asennuksessa ei ongelmia.  
b) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi).  
-
Tässä kaikki komennot, mitä käytin tehtävän aikana:  
18:12 sudo apt-get update  
18:15 VIRHE: "admin1 is not in the sudoers file"  
18:24 su -  
18:26 usermod -aG sudo admin1  
18:26 groups admin1  
18:28 exit  
18:29 sudo apt-get update  
18:29 VIRHE: "admin1 is not in the sudoers file"  
Tässä kohdassa päätin vaihtaa vain juureen, enkä ymmärtänyt miksi käyttäjäni "admin1" ei voinut ajaa sudo-komentoja.  

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

c) Viisi tärkeintä. Näytä Linuxissa esimerkit viidestä tärkeimmästä Saltin tilafunktiosta: pkg, file, service, user, cmd. Analysoi ja selitä tulokset.  
-
d) Idempotentti. Anna esimerkki idempotenssista. Aja 'salt-call --local' komentoja, analysoi tulokset, selitä miten idempotenssi ilmenee.  
-

pkg:  
23:58 su -  
23:58 apt-get update  
00:01 apt-get -y install salt-minion  
00:01 salt-call --version  
00:03 salt-call --local -l info state.single pkg.installed tree
00:05  salt-call --local -l info state.single pkg.removed tree
Tässä kohdassa asennettiin  ohjelmisto tree, jonka heti jälkeen se poistettiin.  
Prosessi suoritettiin onnistuneesti, sillä lopputulos komennolla oli: True
Idempotenssi ilmenee: Paketti asennetaan, jos sitä ei ole mutta muutoksia ei tule, jos se on jo ladattu.

file:  
00:18 salt-call --local -l info state.single file.managed /tmp/Orange  
Tässä Salt loi tiedostopolun "/tmp/Orange".  

00:24 salt-call --local -l info state.single file.managed /tmp/Green contents="Tämä on vain testi"  
Tässä Salt loi tiedostopolun "/tmp/Green", jonka sisälle laitettiin teksti: "Tämä on vain testi". 

00:32 salt-call --local -l info state.single file.absent /tmp/hellotero  
Tässä Salt päinvastaisen toiminnon verrattuna osioon "file.managed". Salt siis pitää huolen, että "hellotero" poistuu ja ei ole olemassa.  
Koska polkua /tmp/hellotero ei alunperinkään ollut olemassa, Salt kertoo komennon suoriutuneen.  
Näissä idempotenssi ilmenee Saltin luomalla polut, jos niitä ei ole olemassa tai jättää tämän tekemättä, jos ne ovat jo olemassa.

service:  
00:40 salt-call --local -l info state.single service.running apache2 enable=True  
VIRHE: "The named service apache2 is not available"  
00:42 apt-get install apache2  
00:45 systemctl status apache2  
00:46 salt-call --local -l info state.single service.running apache2 enable=True  
00:48 salt-call --local -l info state.single service.dead apache2 enable=False
Tässä tarkoitus on käynnistää apache2 ja pitää se päällä, jos kone käynnistetään uudelleen.  
Lopuksi tämä vain kumottiin.  
Idempotenssi ilmenee tässä siten, että Salt käynnistää apachen tai jättää tekemättä mitään, jos tämä on jo päällä.

user:  
00:59 salt-call --local -l info state.single user.present tero  
01:00 salt-call --local -l info state.single user.absent tero  
Tässä luodaan ja poistetaan käyttäjä "tero"  
Idempotenssi näkyy siten, että uutta käyttäjää "tero" ei luoda, jos yksi tero on jo olemassa.

cmd  
01:21 salt-call --local sys.state_doc  
01:26 salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"  
Tässä Salt ajaa komennon shellissä, jonka avulla luotiin "/tmp/foo". Salt ei itse luo tiedostoa, vaan tekee tämän shellin kautta.
Tässä idempotenssi ilmenee, sillä ajettaessa tämän uudestaan muutoksia ei tapahdu, jos haluttu lopputulos on jo saatu.  

Lähteet:  
Karvinen, Tero 2025: Install Salt on Debian 13 Trixie. Luettavissa: https://terokarvinen.com/install-salt-on-debian-13-trixie/  
Karvinen, Tero 2021: Run Salt Command Locally. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/  
Unix & Linux Stack Exchange 2014: New user with root access in Linux Debian. Luettavissa: https://unix.stackexchange.com/questions/98797/new-user-with-root-access-in-linux-debian  
