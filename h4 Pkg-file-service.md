x)
h4 Pkg-file-service

Artikelissa kerrotaan, miten Saltin avulla voidaan ohjata useita eri prosesseja samaan aikaan.  

- Package-file-service on yleisin malli tähän tarkoitukseen.  
- Tässä näytetään Salt-tila SSH-palvelimen portin vaihtamiseksi.  

a) SSHouto. Lisää uusi portti, jossa SSHd kuuntelee  
-

Muokkasin tiedostoa /srv/salt/sshd_config  
Porttejen arvot ovat 2222 ja 8888  
(Katsoin aluksi väärää tiedostoa /etc/ssh/sshd_config)  


Virhe tuli muutamiin kohtiin, ja vaihdoin nämä.
![](images/sshd-er1.png)
![](images/sshd-er2.png)


Lähteet:
Karvinen, Tero 2018. Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh  
