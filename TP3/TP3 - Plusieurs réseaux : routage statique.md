# B1 Réseau 2018 - TP3

***08/01/2019***  - Bordeaux Ynov Campus Informatique B1 B
## Auteurs
* **BOUFFARTIGUE** Pierre
* **BRUNO** Lúca
* **LE COZ** Yann 
* **PETIT** Martin
# I. Création et utilisation simples d'une VM CentOS
## 4. Configuration réseau d'une machine CentOS

**A faire :**

**A**. Le fait d'avoir une adresse ip prouve que nous sommes connectés à un réseau. Commande utilisée : `ip a`
![](https://i.imgur.com/zPkSbqW.png)

**B**. Le PC hôte et la VM peuvent communiquer grâce à un `ping 192.168.127.1`.
Ping de la VM vers le pc hôte :
![](https://i.imgur.com/Z8QVThr.png)
Ping du pc hôte vers la vm : 
![](https://i.imgur.com/ObFYz7O.png)
Les deux machines reçoivent des réponses, une communication est donc établie.

**C**. -------------------


## 5. Faire joujou avec quelques commandes

**A faire :**

* Ping :
Voir ci-dessus où une liaison a été créée entre le pc hôte et la vm grâce à la commande `ping 192.168.127.1`.
![](https://i.imgur.com/N1SCY96.png)
Nouvelle image du ping entre les deux machines.

* Afficher la table de routage :
La ligne qui leur permet de discuter a été mise en évidence sur chaque image : 
![](https://i.imgur.com/We1wMAM.png)

* depuis la VM utilisez curl (ou wget) pour télécharger un fichier sur internet : 
![](https://i.imgur.com/QyRHbDK.png)

* depuis la VM utilisez dig pour connaître l'IP de `ynov.com ` et `google.com`:
    * `dig` sur ynov.com
![](https://i.imgur.com/xG1eFFE.png)

    * `dig` sur google.com
![](https://i.imgur.com/xC2w4BS.png)




# II. Notion de ports et SSH
## 1. Exploration des ports locaux

* Utilisation de la commande `ss` pour lister les ports TCP sur la machine : 
![](https://i.imgur.com/Ja94Nto.png)
    * ss avec TCP (`ss -t`): 
![](https://i.imgur.com/P9amK5C.png)
    * ss avec listening (`ss -l`):
![](https://i.imgur.com/T1Qx2QJ.png)

* Utilisation des options :
    * `ss -n` :
![](https://i.imgur.com/WfzVB3c.png)

    * `ss -p` :

## 2. SSH

Connexion des PCs hôtes aux machines virtuelles :
* Hôte Linux :
![](https://i.imgur.com/cM2yki2.png)
* Hôte Windows :
![](https://i.imgur.com/TyVpVm2.png)



## 3. Firewall
* A. SSH :
Commande `ss` après modification du port `22` en `2222`

![](https://i.imgur.com/ox9RVC1.png)

La connexion doit échouer car le port n'est pas autorisé sur le firewall. La solution pour le faire marcher serait donc d'autoriser le port.

    * Linux
![](https://i.imgur.com/op7eWfy.png)


    * Windows
![](https://i.imgur.com/CXhLOMZ.png)

* B. `netcat`:
Liaison entre les deux machines via `netcat` :

![](https://i.imgur.com/ZoeNQHU.png)

Vérification de la liaison entre l'hôte et le client :

![](https://i.imgur.com/gYiU2BW.png)

# III. Routage statique
![](https://cdn.discordapp.com/attachments/503930596721164329/536897210793721856/Capture12.PNG)

Il faut faire la commande ci-dessus en changeant la première adresse IP et la dernière en fonction d'où on code.
