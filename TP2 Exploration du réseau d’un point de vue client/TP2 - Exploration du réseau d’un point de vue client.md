
# TP2 - Exploration du *réseau* d'un point de vue *client*
***20/12/2018***  - Bordeaux Ynov Campus Informatique B1 B
## Auteurs
* **BOUFFARTIGUE** Pierre 
* **BRUNO** Lúca
* **LE COZ** Yann 
* **PETIT** Martin
# I. Exploration locale en solo
## 1. Affichage d'informations sur la pile TCP/IP locale
**En ligne de commande**

Commande utilisée dans le powershell : `ipconfig /all`
Commande sous linux : `$ ip a`

![](https://i.imgur.com/6H0Tvvb.png)


Carte wifi :
 * Nom : `Killer Wireless-n/a/ac 1535 Wireless Network Adapter`
 * Adresse mac : `9C-B6-D0-1F-1A-59`
 * Ip : `10.33.3.47`
 * Adresse réseau : `10.33.0.0`
 * Adresse broadcast : `10.33.3.255`

Ethernet : 
 * Nom : `enp4s0f1`
 * Adresse MAC : `F0:79:59:22:5D:2D`
 * Passerelle : `10.33.3.253`

**En graphique (GUI : Graphical User Interface)** 

 ![](https://i.imgur.com/obrJOot.png)


> Ip : `10.33.3.47`
MAC : `9C-B6-D0-1F-1A-59`
Passerelle : `10 .33.3.253`

**Question :**
A quoi elle sert la passerelle pour Ingésup : 
>Elle permet d’accéder au réseau internet via l’extérieur.

## 2. Modifications des informations
>**A. Modification d'adresse IP - pt. 1**

 ![](https://i.imgur.com/Hh5BCVb.png)


 * Première ip : `10.33.0.1`
 * Dernière ip : `10.33.3.254`

 ![](https://i.imgur.com/FVL3oP8.png)


>**B. nmap**
 
![](https://i.imgur.com/HMqJHp7.png)

![](https://i.imgur.com/hNSv8xb.png)

![](https://i.imgur.com/jYPC1Ny.png)

 

 

>**C. Modification d'adresse IP - pt. 2**

Après vérification et modification de l’ip, j’ai pu me rendre sur internet.
## II. Exploration locale en duo

### II.1 Modification d'adresse IP

Modification des adresses IP en static:
`10.1.40.25` (Lúca)
`10.1.40.12` (Yann)

Ping depuis Lúca vers Yann et inversement.

![](https://i.imgur.com/NJa4lET.png)

### II.2 Utilisation d'un des deux comme gateway

Modification du masque de sous réseau en : `255.255.255.0`

![](https://i.imgur.com/PvsfOWB.png)

![](https://i.imgur.com/vHLoShl.png)

![](https://i.imgur.com/PMrYgcb.png)

Vous pouvez voir ci-dessous le changement d'adresse IP et le remplacement de l'adresse Passerelle par l'adresse IP de l'autre ordinateur connecté à Internet:
![](https://i.imgur.com/oxTeZVx.png)

### II.3. Petit chat privé ?

Vous pouvez voir sur la capture ci-dessous le paramétrage pour configurer le chat privé.

![](https://i.imgur.com/LvzyKXi.png)

### II.4. Wireshark

* Pendant un `ping` :

![](https://i.imgur.com/ZUsw6d9.png)

## III. Manipulations d'autres outils/protocoles côté client
### III.1 DHCP
* Adresse IP serveur DHCP : `169.254.4.231`
### III.1 DNS
- Adresse IP serveur DNS : `172.0.0.53`
-  Adresse IP de :
	* google.com : `216.58.213.142`
	* ynov.com : `217.70.184.38`
- Nom de domaine de l'adresse :
	* `78.78.21.21` : ``$ dig +noall +answer -x 78.78.21.21
21.21.78.78.in-addr.arpa. 3599  IN      PTR     host-78-78-21-21.mobileonline.telia.com.``
	* `92.16.54.88` :``$ dig +noall +answer -x 92.16.54.88
88.54.16.92.in-addr.arpa. 7199  IN      PTR     host-92-16-54-88.as13285.net.``

