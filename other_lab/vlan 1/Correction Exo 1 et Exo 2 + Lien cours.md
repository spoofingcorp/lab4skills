# Cours et correction Master Class VLAN 1/3 - 06012023

## Lien Exercice Packet Tracer VLAN 1/3
[Lien](https://viacesifr-my.sharepoint.com/:u:/g/personal/remi_brusse_viacesi_fr/ETVlYZLCWFlHr3ipHvfpkIkBrdN2k-hrUQnWk0KueYzuWw?e=rl0SVh)


### Envoyer votre Packet Tracer terminé sur le dépôt suivant nommé de la façon suivante:
[Lien](https://nc.spoofing.cloudns.pro/s/FZcJSsD4DTyZQ7C)

Nom_Prénom_MC_VLAN1
Vous ne verrez pas votre fichier ce n'est qu'une boite de dépôt


## Cours réseau (Présentation Master Class)
[Lien](https://viacesifr-my.sharepoint.com/:b:/g/personal/remi_brusse_viacesi_fr/EYv26XNoUKhHuX_aq4yDplsBBgkrrQ8iKtDhOI5x6-8SGA?e=0MsZYg)

## Cours réseau Cisco CCNA 1 à 4
[Lien](https://learn.spoofing.cloudns.pro)

Rappel:

- Port mode access = Un seul VLAN sur l'interface
- Port mode trunk = Plusieurs VLAN sur l'interface

# Exercice 01 - VLAN N2

### Cours VLAN
[Lien](https://learn.spoofing.cloudns.pro/ccna2/course/module3/index.html#3.2.1.1)

```
en

conf t

vlan 10
vlan 20

int range fa0/1-12
switchport mode access
switchport access vlan 10

int range fa0/13-24
switchport mode access
switchport access vlan 20


do wr
```

### Mettre en correspondance les interfaces du switch avec les PC dans le bon VLAN
### Tester de pinguer les postes de vlan20 à vlan20 et de vlan20 à vlan10
### Les PC du VLAN 20 doivent pouvoir se pinguer
### Les PC du VLAN 20 ne peuvent pas pinguer les PC du VLAN 10 et inverssement


# Exercice 02 - Routeur + VLAN N2

### Switch (la configuration est similaire au 1er exercice, c'est l'ajout du routeur en tant que passerelle qui va permettre de router le traffic de VLAN 10 à 20, et inverssement.

```
en

conf t

vlan 10
vlan 20

int range fa0/1-12
switchport mode access
switchport access vlan 10

int range fa0/13-24
switchport mode access
switchport access vlan 20


do wr
```

## Configuration du Routeur
### Cours configuration routeur
[Lien](https://learn.spoofing.cloudns.pro/ccna2/course/module4/index.html#4.1.3.2)

```
en
conf t

int G0/0/0
ip address 192.168.10.1 255.255.255.0
no sh

int G0/0/1
ip address 192.168.20.1 255.255.255.0
no sh

do wr
```

### Mettre en correspondance les interfaces du switch avec les PC dans le bon VLAN, idem pour les interfaces du routeur.
### Tester de pinguer les postes de vlan20 à vlan20 et de vlan20 à vlan10 
### Cette fois le routage opéré par le routeur permet de router le traffic entre les VLAN 10 et 20


# Exercice 03 - Router On Stick + VLAN Trunk

### Configuration du switch avec un port en mode Trunk vers le routeur on stick

```
en

conf t

vlan 10
vlan 20

int range fa0/1-12
switchport mode access
switchport access vlan 10

int range fa0/13-24
switchport mode access
switchport access vlan 20

int G0/1
switchport mode trunk
switchport trunk allowed vlan all

int G0/2
switchport mode trunk
switchport trunk allowed vlan all

do wr mem
```

# Configuration du routeur on stick
## Cours Router On Stick 

[Lien](https://learn.spoofing.cloudns.pro/ccna2/course/module5/index.html#5.1.3.2)

```
en

conf t

interface G0/0/1.10  
encapsulation dot1Q 10 
ip add 192.168.10.1 255.255.255.0 
no sh

interface G0/0/1.20  
encapsulation dot1Q 20 
ip add 192.168.20.1 255.255.255.0 
no sh

int G0/0/1
no sh

do wr 
```

### Mettre en correspondance les interfaces du switch avec les PC dans le bon VLAN, idem sur le routeur.
### Tester de pinguer les postes de vlan20 à vlan20 et de vlan20 à vlan10.
### Cette fois le routage opéré par le routeur on stick permet de router le traffic entre les VLAN 10 et 20 et inverssement.


# Exercice 4 - SVI Switch Virtual Interface - Switch L3
## Cours Switch niveau 3
[Lien](https://learn.spoofing.cloudns.pro/ccna2/course/module5/index.html#5.3.1.3)

```
en

conf t

ip routing

vlan 10
vlan 20

int vlan 10
ip address 192.168.10.1 255.255.255.0
no sh

int vlan 20
ip address 192.168.20.1 255.255.255.0
no sh


int range G1/0/1-12
switchport mode access
switchport access vlan 10

int range G1/0/13-24
switchport mode access
switchport access vlan 20


do wr mem
```

### Mettre en correspondance les interfaces du switch avec les PC dans le bon VLAN.
### Tester de pinguer les postes de vlan20 à vlan20 et de vlan20 à vlan10 
### Cette fois le routage opéré par le Switch en mode Niveau 3 permet de router le traffic entre les VLAN 10 et 20 et inverssement.



# Commande de diagnostic sur Switch et Routeur

## Etudier votre configuration globale

```
sh run
do sh run
```

## Etudier les interfaces physiques et VLAN

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

## Dépolluer un routeur (Supprime la config) :warning:

```
wr erase
relaod
no
```

## Dépolluer un switch (Supprime la config) :warning:

```
delete flash:vlan.dat
wr erase
relaod
no
```







