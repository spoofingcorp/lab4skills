# LAB VLAN 2/3 - 03042024

# Déroulé journée

- Récap et correction de l'exercice du Lab4skills VLAN 1/3 du 06012023 (Routage Inter-VLAN N2 et N3)

- Consignes du jour et présentation des attentes *(Ne pas faire en même temps, suivre et prendre des notes)*  


# Consignes Lab4skills VLAN 2/3

Vous êtes salarié d'une sociéte de prestation de service (BestNetworkTech) et intervenez chez votre client Ubisoft à Bordeaux.

- Vous devez analyser les informations fournis par l'architecte réseau pour implémenter les configurations du routeur et des switchs.

- Dans un premier temps, souvenez-vous, faites de la relève d'info (Dénomination des interfaces `Fa` ou `Gi` ? `G0/0` ou `Fa0/1` ?)

- Utilisez les commandes `sh run` et  `sh ip int br` pour observer les dénominations des interfaces de chaque équipement.

- Dans un second temps, avec Notepad++ ou un autre éditeur de texte, créer les configurations pour les injecter sur les équipement sur site facilement. (Mettre en correspondance l'ID du VLAN / Services / Poste) 

- **Vous trouverez des exemples des commandes pour chaque équipement, pour la création d'un VLAN sur le routeur, les switchs...** *(Exemple VLAN 32 Developpeur).*

- Adapter les commandes grâce aux exemples pour créer les autres VLAN (Serveurs, DevOps, Chef de Projet, Management)  


# LAB Packet Tracer VLAN Ubisoft

[Lien - LAB Packet Tracer - VLAN_Ubisoft.pka](https://github.com/spoofingcorp/lab4skills/blob/3dbd2f78c3402cfde91362ad5a1b8ebdad9fff99/other_lab/vlan%202/MC%20Ubisoft%20VLAN2.pkt)  

[Lien - Logiciel Packet Tracer 8.2.0](https://skillsforall.com/course/getting-started-cisco-packet-tracer?userLang=fr-FR) *(Il faudra vous créer un compte Cisco Skills for All)*

# Critère d'évaluation / rendu

Vous ne pourrez pas partir de chez Ubisoft sans que les services réseau fonctionnent, les sorties de JustDance 2024 et Assansin's Creed n'attendent pas !

Une fois les configurations réalisées, renseigner les IP/Masque/Paserelle sur les hôtes et tester de pinguer les passerelles de chaque VLAN.

**Vous allez y arriver !**

**Tu vas y arriver !!!**

Comme la semaine dernière, vous devrez nous faire parvenir votre sauvegarde de l'exercice Packet Tracer Ubisoft dans la boite de dépôt suivante.  


# Ressources / Cours

## Cours VLAN
[Lien - Cours VLAN](https://learn.spoofing.cloudns.pro/ccna2/course/module3/index.html#3.2.1.1)

[Lien - Cours Modification port VLAN](https://learn.spoofing.cloudns.pro/ccna2/course/module3/index.html#3.2.1.4)

## Cours Router On Stick 
[Lien - Cours Router_On_Stick](https://learn.spoofing.cloudns.pro/ccna2/course/module5/index.html#5.1.3.2)

## Cours Relay DHCP
[Lien - Cours Relay DHCP](https://learn.spoofing.cloudns.pro/ccna2/course/module10/index.html#10.1.2.3)

## Cours réseau Cisco CCNA 1 à 4
[Lien - Cisco CCNA](https://learn.spoofing.cloudns.pro)

## Cours réseau (Présentation Master Class VLAN 1/2)
[Lien - Présentation](https://github.com/spoofingcorp/lab4skills/blob/main/files/%5BCOURS%5D%20Cisco%20CCNAv7.pdf)


# Pour aller plus loin / améliorations
## Conditions - Avoir terminé les consignes précédentes 

- Configurer le relay DHCP sur les sous-interfaces et tester que les postes obtiennent une @IP dynamique

##### Exemple Relay DHCP pour le VLAN 32 - Developpeur *(Sur les sous-interfaces du routeur)*

```
int  G0/0/1.32
ip helper-adress 172.16.27.100
```


- Créer des SVI sur les switchs pour pouvoir les administrer en SSH grâce au VLAN 199 *(Une IP différente par Switch)* 

[Lien - Confguration SVI](https://cisco.goffinet.org/ccna/vlans/configuration-vlan-cisco-ios/#23-linterface-vlanx-de-gestion-svi)

##### Exemple administration Switch L2-01 via une SVI

```
interface vlan 199
ip address 192.168.199.251 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.199.1
```
Vous pouvez ensuite administrer depuis un poste en SSH le switch via l'IP de la SVI


- Activer SSH sur les switch pour les manager à distance sur le VLAN 199 

[Lien - Confguration SSH 01](https://learn.spoofing.cloudns.pro/ccna2/course/module2/index.html#2.2.1.2)

[Lien - Confguration SSH 02](https://w7cloud.com/configuration-of-ssh-on-cisco-switch/)



- Changer le VLAN natif untagged vlan 1 par un VLAN 99 taggued (Pas le VLAN 199 Management)
*(Créer un nouveau VLAN 99 pour la communication native entre les switchs pour le protocole STP par exemple, DTP...)*

[Lien - Switch Sécurisation VLAN Natif](https://www.connecteddots.online/resources/cisco-reference/switchport-trunk-native-vlan)

#### VLAN Natif 99 - Configuration des interfaces Trunk des Switchs sur le VLAN Natif 99

```
int G0/1
switchport trunk native vlan 99

do sh int trunk

```



# Correction VLAN Ubisoft

## Router_On_Stick

```
en
conf t

int G0/0/1
no sh

int G0/0/1.27
encapsulation dot1Q 27
ip address 172.16.27.1 255.255.255.0
no sh

int G0/0/1.32
encapsulation dot1Q 32
ip address 172.16.32.1 255.255.255.0
no sh
ip helper-address 172.16.27.100

int G0/0/1.68
encapsulation dot1Q 68
ip address 172.16.68.1 255.255.255.0
no sh
ip helper-address 172.16.27.100

int G0/0/1.97
encapsulation dot1Q 97
ip address 172.16.97.1 255.255.255.0
no sh
ip helper-address 172.16.27.100

int G0/0/1.199
encapsulation dot1Q 199
ip address 172.16.199.1 255.255.255.0
no sh

int G0/0/1.99
encapsulation dot1Q 99
ip address 172.16.99.1 255.255.255.0
no sh

do wr mem
```

## Switch L2-01 et Switch L02-02

```
en
conf t


vlan 27
vlan 32
vlan 68
vlan 97
vlan 199
vlan 99


int range Fa0/1-6
switchport mode access
switchport access vlan 32

int range Fa0/7-12
switchport mode access
switchport access vlan 68

int range Fa0/13-16
switchport mode access
switchport access vlan 97

int range Fa0/20-22
switchport mode access
switchport access vlan 27

int G0/1
switchport mode trunk
switchport trunk allowed vlan all
switchport trunk native vlan 99

int G0/2
switchport mode trunk
switchport trunk allowed vlan all
switchport trunk native vlan 99


# Changer l'IP du la SVI sur chaque switch
int vlan 199
ip address 172.16.199.251 255.255.255.0
no shutdown

ip default-gateway 172.16.199.1

hostname Switch01

ip domain-name domain.com.
service password-encryption
crypto key generate rsa general-keys modulus 1024
username cisco privilege 15 secret cisco
enable secret cisco
line vty 0 15
login local
transport input ssh
ip ssh version 2
banner motd # ATTENTION VOUS ENCOUREZ DES POURSUITES #

do wr mem
```


## Debug SSH - (Stagiaire 1 - Formateur 0)

C'est ma faute, j'avais renseigné `ip default-gateway 192.168.199.1` sur mes switchs, alors que c'est `ip default-gateway 172.16.199.1` la gateway sur le VLAN 199.

J'ai corrigé le fichier de conf, on peut se connecter en SSH sur les switch depuis tous les postes dans n'importe quel VLAN.

Idem correction ci-dessus corrigée 
`ip default-gateway 172.16.199.1`

### Test depuis un PC vers SSH Switch 01
`ssh -l cisco 172.16.199.251`

### Test depuis un PC vers SSH Switch 02
`ssh -l cisco 172.16.199.252`

___________________

## A vous maintenant



