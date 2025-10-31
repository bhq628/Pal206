x)  
Karvinen 2014: Hello Salt Infra-as-Code  
-  
- Tässä esitetään kansion luominen Saltissa, josta tehdään idempotenttinen.  
- Salt pitää huolen, että kansio on olemassa.  

Salt contributors: Salt overview:  
-
YAML on formaatti, miten data rakentuu ja näkyy Saltissa.  

YAML rakenteen kolme osaa ovat:  
- Scalars/Skalaarit = Näissä arvoina voi olla numero, merkkijono tai totuusarvo.  
- Lists/Listat = listoissa on tavuviiva, arvo ja kaksi välilyöntiä lopussa. Arvot esitetään omilla riveillään.  
- Dictionaries/Sanakirjat = Nämä ovat scalaareista tehtyjä kokoelmia.  

YAML lohkorakenteet  
-
- YAML lohkorakenteissa on sisennettävä ominaisuudet yhdellä tai kahdella välilyönnillä. Ilman tätä tulee virhe.  

Salt contributors: The top file
-
- Päätiedosto/"Top file" kertoo, mitkä asetukset koskevat mitäkin orjia.  
  Päätiedostoon kuuluu kolme asetusta:  
  - Ympäristö: Tilapuuhakemisto, josta haetaan tilatiedostot asetuksia varten.  
  - Kohde: Ryhmä koneita, joille asetataan tila.  
  - Tilatiedostot: Lista tilatiedostoista, joita käytetään kohteessa. Jokainen tilatiedosto kuvaa yhden tai useamman tilan, jotka otetaan käyttöön.  

Oracle VirtualBox tekniset tiedot  
4 Ydintä  
RAM: 4096 MB  


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



Lähteet: Karvinen, Tero 2024. Hello Salt Infra-as-Code. Luettavissa: https://terokarvinen.com/2024/hello-salt-infra-as-code/  
Salt Project. (n.d.). Salt user guide. Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml  
Salt Project. 2025. xxx. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/top.html  
