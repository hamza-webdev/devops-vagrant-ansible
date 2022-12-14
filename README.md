# Vagrant

````
vagrant list-commands

vagrant global-status

vagrant up

vagrant ssh

vagrant destroy
ou
vagrant halt

````

##  Init vagrant

````
vagrant init ubuntu/trusty64

vagrant up

vagrant ssh
````
## Box components

vagrant box list -i

### Install Vagrant Box
- vagrant box add --name ubuntu ubuntu/trusty64 [ --box-version=20190425.0.0]
- Vagrant cloud: https://app.vagrantup.com/boxes/search
- en se connectant dans ce VM: vagrant ssh:
  - sudo apt update
  - sudo apt-get install nginx
  - sudo service nginx start
    - curl 127.0.0.1
  - sudo apt install mysql-server
  - sudo mysql_secure_installation
  - sudo apt install php-fpm php-mysql

### Creation de notre VBox (compte lab2)

- vagrant package --output ubuntu-nginx-mysql-composer.box

### Verifier le code de fichier vagrantfile
````
vagrant validate
````
## Example vagrantfile
````
Vagrant.configure("2") do |config|
  config.vm.box = "geerlingguy/centos7"
  config.vm.provider "virtualbox" do |v|
    v.memory = RAM
    v.cpus = CPU
  end
  config.vm.network "private_network", ip: IP

end
````
### On se connectant sur le vm via ssh vagrant@ip
````
sudo systemctl start nginx
ou
sudo service nginx start
````
## Gestion et install des Plugins
````
vagrant plugin COMMAND -h
````
## Vagrant::Hostsupdater
Ce plugin ajoute une entrée à votre fichier /etc/hosts sur le système hôte.

Sur les commandes up, resume et reload, il essaie d'ajouter les informations, si elles n'existent pas déjà dans votre fichier hosts. S'il doit être ajouté, un mot de passe administrateur vous sera demandé, car il utilise sudo pour modifier le fichier.

Lors de l'arrêt, de la destruction et de la suspension, ces entrées seront à nouveau supprimées. En définissant config.hostsupdater.remove_on_suspend = false, suspend et halt ne les supprimera pas.
````
$ vagrant plugin install vagrant-hostsupdater

config.vm.network :private_network, ip: "192.168.3.10"
config.vm.hostname = "www.testing.de"
config.hostsupdater.aliases = ["alias.testing.de", "alias2.somedomain.com"]

````
