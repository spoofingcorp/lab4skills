# **Lab4skills VLAN 3/3 - 20012023**

# Déroulé journée

- Cours Routage Inter VLAN de Niveau 3 - Switch L3

- Cours Troubleshooting Top to Down, Down to Top

- Consignes du jour et présentation des attentes *(Ne pas faire en même temps, suivre et prendre des notes)*  


# Consignes Lab4skills VLAN 3/3

Vous êtes salarié de la sociéte de prestation de service **BestNetworkTech** et intervenez cette semaine chez un nouveau client **Wood4Tree**.

- Vous devez analyser les informations fournis par l'architecte réseau pour dépanner les services du client.

- Vous devez résoudre le/les panne(s) avec méthodologie, ne pas modifier les configurations des équipements sans backup des informations. (Noter, copier, sauvegarder les infos)

- Commencer par étudier la synchro des cables Ethernet *(Couche 1 - OSI)*

- **Ne chercher pas trop loin, il y a beaucoup de services (DNS, DHCP, Mail), le client ne sait jamais formuler la problématique, installez-vous à son poste et passer les commandes suivantes:**

| Commande | Descriptif |
| -------- | ---------- |
| `ipconfig /all`  |  Affiche les informations réseau du poste client > APIPA > Pas bien !|
| `ipconfig /release` | Relache le bail DHCP |
| `ipconfig /renew` | Demande un nouveau bail DHCP - DORA > APIPA ? > Pas bien ! |
|`ping passerelle` | Nécessaire pour communiquer en dehors du VLAN *(Ne taper pas "passerelle" mais son IP*) |
| `ping IP_serveur_DNS_de_la_société` | Test la communication avec le serveur DNS interne |
| `nslookup les_noms_de_domaine_interne` | Test la résolution des enregistrements DNS internes |
| `ping 8.8.8.8` | Test internet en IP |
|`nslookup google.com` | Test résolution d'un nom de domaine externe public en une adresse IP |
| `ping google.com` | Test résolution d'un nom de domaine externe public en une adresse IP + Test ICMP vers internet en IP après la résolution DNS |


- Tester, verifier les configurations IP des postes, le client de messagerie gmail, le WLAN, les login, mot de passe, les URL des services internes comme l'accès à l'ERP ou au WinCC Siemens depuis la Prod... 

- Utilisez les commandes `sh run` et  `sh ip int br` pour observer les configurations des switchs et routeurs.

- Utilisez les commandes `sh vlan` ou `sh int trunk` pour vérifier les configurations des switchs.

- Noter le resultat de votre troubleshooting avec le numéro de l'exercice sur papier ou sur un doc pour nous soumettre vos réponses en fin de scéance *(Merci de ne pas partager vos résultats, cela nuirait à l'acquisition des compétences des autres stagiaires)*

**N'oubliez pas de noter vos resultats (la panne que vous avez identifiée et corrigée) / numéro de l'exercice**


# LAB Packet Tracer TROUBLESHOOTING

## Prérequis
#### Pour ceux qui n'ont pas encore Packet Tracer, il faudra au préalable télécharger Packet Tracer 8.2.0 et vous créer un compte sur Cisco Skills for All

[Lien - Prérequis Logiciel Packet Tracer 8.2.0](https://skillsforall.com/course/getting-started-cisco-packet-tracer?userLang=fr-FR) 



## Exercices Troubleshooting - Github

[Lien - LAB TB_01.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_01.pkt)  

[Lien - LAB TB_02.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_02.pkt)  

[Lien - LAB TB_03.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_03.pkt)

[Lien - LAB TB_04.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_04.pkt) 

[Lien - LAB TB_05.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_05.pkt)   

[Lien - LAB TB_06.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_06.pkt)  

[Lien - LAB TB_07.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_07.pkt)  

[Lien - LAB TB_08.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_08.pkt)  

[Lien - LAB TB_09.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_09.pkt)  

[Lien - LAB TB_10.pka](https://github.com/spoofingcorp/lab4skills/blob/8ab3079010d3544aaba1d8571248651a973ada1a/files/TB_10.pkt)  

# Critère d'évaluation / rendu

Comme le jour de l'examen TSSR en présence du jury, vous resolvez des pannes sur une maquette similaire à celle d'aujourd'hui pour valider vos compétences et votre méthodologie.

**Tu vas y arriver !!!**

Cette fois, vous devrez nous faire parvenir vos résultats en fin de scéance via un sondage sur Zoom. 

**N'oubliez pas de noter vos resultats (la panne que vous avez identifiée et corrigée) / numéro de l'exercice**


# Correction Troubleshooting

	
| Exercices | Pannes |
| -------- | ---------- |
| TB_01 |	Port Shutdown Switch_L2_01 > Laptop 01 |
|TB_02 |	WAN interface G0/0/0 shutdown |
|TB_03 |	Port TRUNK Switch L2_01 - VLAN Allowed 199 seulement |
|TB_04 |	Server DHCP - Mauvaise Adresse IP carte réseau Server DHCP |
|TB_05 |	Messagerie Internet - Mauvais mot de passe compte user2 + mauvais smtp user1 |
|TB_06 |	Server DNS mauvaise passerelle |
|TB_07	| PC's Prod - Mauvaise config carte réseau |
|TB_08 |	AP Wifi dans le mauvais VLAN + mauvais password dans l'AP |
|TB_09 |	Cable réseau + 100m (vue physique) + Laptop 03 n'est plus dans la couverture WLAN (vue physique)  + Laptop 02  inversion cablage tel IP port Switch/PC |
|TB_10 |	SVI Shutdown Switch L3 + Désactivation Services DHCP + Désactivation Services DNS + SVI VLAN 20 192.168.22.1 |


# Ressources / Cours

## Cours VLAN
[Lien - Cours VLAN](https://learn.spoofing.cloudns.pro/ccna2/course/module3/index.html#3.2.1.1)

## Cours réseau Cisco CCNA 1 à 4
[Lien - Cisco CCNA](https://learn.spoofing.cloudns.pro)

## Cours réseau (Présentation Master Class VLAN)
[Lien - Présentation](https://viacesifr-my.sharepoint.com/:b:/g/personal/remi_brusse_viacesi_fr/EYv26XNoUKhHuX_aq4yDplsBBgkrrQ8iKtDhOI5x6-8SGA?e=0MsZYg)

## Cours ITIL - Troubleshooting (Présentation VLAN 3/3)
[Lien - Présentation](https://viacesifr-my.sharepoint.com/:p:/g/personal/remi_brusse_viacesi_fr/EcVGU5lRZSFLrjfyN3RjSjwBIn-7hHLXgWmPG0zf5bVpyQ?e=lqS3zc)




# Pour aller plus loin / améliorations
## Conditions - Avoir terminé les consignes précédentes 

- Sauvegarder les configurations des switchs sur un serveur TFTP  que vous implémenterer de A à Z dans la topologie du client.

[Lien - Gestion des images logicielles Cisco IOS en TFTP](https://learn.spoofing.cloudns.pro/ccna3/course/module9/index.html#9.1.2.1)



- Mettre en place le protocole d'agrégation de liaisons entre le Switch_L3 et le Switch_L2_01 dans la topologie du client

[Lien - Agrégation de liaisons](https://learn.spoofing.cloudns.pro/ccna3/course/module3/index.html#3.2.1.2)


- Upgrade du Switch-L2_01 en TFTP *(Adapter l'image IOS pour le switch 2960 - Lister la version de l'IOS `sh version`)*

[Lien - Upgarde IOS via FTP](https://www.youtube.com/watch?v=kaZCZr6feyU)


- Etudier les paquets sur Packet Tracer avec un Sniffer

[Lien - Sniffer de paquet - Wireshark Like](https://www.youtube.com/watch?v=gsCSKQAVT2M)


_

# Lien des Lab4Skills VLAN 1 à 3

### **Lab4skills VLAN 1/3 - 06012023**
[Lien - Lab4skills VLAN 1/3 - Consignes + Exo + Correction](https://github.com/spoofingcorp/lab4skills/blob/3dbd2f78c3402cfde91362ad5a1b8ebdad9fff99/other_lab/vlan%201/Correction%20Exo%201%20et%20Exo%202%20+%20Lien%20cours.md)


### **Lab4skills VLAN 2/3 - 13012023**
[Lien - Lab4skills VLAN 2/3 - Consignes + Exo + Correction](https://github.com/spoofingcorp/lab4skills/blob/3dbd2f78c3402cfde91362ad5a1b8ebdad9fff99/other_lab/vlan%202/Lab4skills_VLAN_130123%20.md)


### **Lab4skills VLAN 3/3 - 20012023**
[Lien - Lab4skills VLAN 3/3 - Consignes + Exo](https://github.com/spoofingcorp/lab4skills/blob/3dbd2f78c3402cfde91362ad5a1b8ebdad9fff99/Lab4skills_VLAN_200123.md)

_


# Commande de diagnostic sur Switch et Routeur

## Etudier votre configuration globale

```
sh run
do sh run
```

## Etudier les interfaces physiques et interfaces VLAN

```
sh ip int br
do sh ip int br
```

## Etudier les interfaces Trunk

```
sh int trunk
do sh int trunk
```

## Etudier la table CAM du switch

```
show mac-address-table
do show mac-address-table
```

## Etudier la table de routage d'un routeur

```
sh ip route
do sh ip route
```