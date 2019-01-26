# TP 4 - Spéléologie réseau : descente dans les couches
## Auteur
**Yann LE COZ** - Bordeaux Ynov Campus Informatique - [Zocel](https://github.com/Zocel)
## Sommaire
* [Préparation d'une VM "patron"](#preparation-dune-vm-patron)
* [Mise en place du Lab](#i-mise-en-place-du-lab)
  * [Création des réseaux](#i1-création-des-réseaux)
  * [Création des VMs](#i2-création-des-vms)
## Préparation d'une VM "patron"
On a dû dans un premier temps créer et installer une VM patron avec les configurations suivantes :
* 512 Mo RAM
* 1 CPU
* une carte NAT
* un disque de 8Go
* l'`.iso` de CentOS 7 (sur le "contrôleur IDE")

**Ajouter une capture d'écran ici**

Dans un deuxième temps, nous avons dû la configurer à partir des lignes de commandes ci-dessous :
```bash
# Désactivation de SELinux
sudo setenforce 0 # temporaire
sudo sed -i 's/enforcing/permissive/g' /etc/selinux/config # permanent

# Mise à jour des dépôts
sudo yum update -y

# Installation de dépôts additionels
sudo yum install -y epel-release

# Installation de plusieurs paquets réseau dont on se sert souvent
sudo yum install -y traceroute bind-utils tcpdump nc nano

# Désactivation de la carte NAT au reboot
sudo nano /etc/sysconfig/network-scripts/ifcfg-enp0s3
# mettre ONBOOT à NO

# Eteindre la machine
sudo shutdown now
```

## I. Mise en place du Lab
### I.1 Création des réseaux
Nous avons ensuite créé deux nouveaux réseaux host-only dont les spécificités de ceux-ci sont les suivants :
* **vboxnet1** :
  * la carte réseau de l'hôte doit porter l'IP `10.1.0.1`
  * ce réseau n'a **PAS** de serveur DHCP
* **vboxnet2** :
  * la carte réseau de l'hôte doit porter l'IP `10.2.0.1`
  * ce réseau n'a **PAS** de serveur DHCP
  
**Ajouter la capture d'écran de la fenêtre host-only**
**Ajouter la capture d'écran du terminal**
  
### I.2 Création des VMs
Dans cette partie, nous avons cloner trois fois la *VM "patron"* pour obtenir trois VMs distinctes :
* **La VM Cliente** nommée `client1.tp4`
  * qui contient une carte réseau dans `vboxnet1` qui porte l'IP `10.1.0.10`
* **La VM Serveur** nommée `server1.tp4`
  * qui contient une carte réseau dans `vboxnet2` qui porte l'IP `10.2.0.10`
* **La VM Routeur** nommée `router1.tp4`
  * qui contient une carte réseau dans `vboxnet1` qui porte l'IP `10.1.0.254`  
  * qui contient une carte réseau dans `vboxnet2` qui porte l'IP `10.2.0.254`

De plus après avoir défini les adresses IPs statiques de chacunes d'elles, nous leur avons défini des noms de domaines, rempli leur fichier `/etc/hosts` et pour terminer nous les avons "pingé" entre elles :
* ping de `client1` vers `router1.tp4` sur l'IP `10.1.0.254`
* ping de `server1` vers `router1.tp4` sur l'IP `10.2.0.254`

**Tableau récapitulatif** :

Machine | `vboxnet1` | `vboxnet2`
--- | --- | ---
`client1.tp4` | `10.1.0.10` |
`router1.tp4` | `10.1.0.254` | `10.2.0.254`
`server1.tp4` || `10.2.0.10` 

### I.3 Mise en place du routage statique