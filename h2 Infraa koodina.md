x)  
Karvinen 2014: Hello Salt Infra-as-Code  
-  
- Tässä luodaan kansio, josta tehdään idempotenttinen  
- Salt pitää huolen, että kansio on olemassa

Salt contributors: Salt overview:
- YAML

Specs:  

a)
b)
c)
d)

Aloitus
09:31  sudo apt-get update  
09:32 sudo apt-get -y install salt-minion  
(Salt oli jo asennettu)  

09:33 sudo apt-get -y install micro  
09:33 export EDITOR=micro  
09:36 sudo mkdir -p /srv/salt/hello/  
09:36 cd /srv/salt/hello/  
09:40 sudoedit init.sls  
(Micro editor avautuu ja sinne lisättiin:  
/tmp/hellotero:
  file.managed)
09:42 Ctrl-s  
09:42 Ctrl-q  
09:45 sudo salt-call --local state.apply hello  
09:48 sudoedit init.sls  
09:48 (kuva tähän tekstieditorin muokkauksesta, se toimii)  
