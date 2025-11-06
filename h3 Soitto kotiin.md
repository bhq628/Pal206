x)


a)  Vagrant asennus  
-
6.11.2025 20:43 sudo apt update  

Käytin Vagrantin asentamiseen koodinpätkää hashicorpin viralliselta sivulta.  

6.11.2025 20:47 wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant

6.11.2025 20:50 sudo apt install lsb-release  
6.11.2025 21:06 lsb_release -a  
6.11.2025 21:06 vagrant --version  

![Vagrant-versio](images/Vagrant-versio.png)

b) Linux Vagrant. Tee Vagrantilla uusi Linux-virtuaalikone.  
-



Lähteet: Vagrant. https://developer.hashicorp.com/vagrant/install#linux  
