## Use Case 1

L'entreprise X veut mettre en ligne son site Web PHP.

Pour garantir la haute disponibilité de l'application, un architecte Azure a recommandé de déployer 3 instances de l'application, 
répartis sur 3 zones géographiques.

Les 3 instances seront accessibles par une adresse http unique, derrière un load balancer de niveau 4.

[Démo de l'application]

**Objectifs formateur:**
- Montrer quelles sont les solutions techniques possible pour la publication et scalabilité d'une application Web
- Démontrer la différences en temps de build et en complexité pour chaque solution
- Déterminer la différence de coût entre chaque solution

### Solution à partir de Virtual Machines

1. Création d'une vm ubuntu
	- install apache/php
	- création index.php
2. Création d'une image à partir de la VM
3. Suppression de la VM et des dépendances (nsg/vnet/disk/...)
4. Création du Vnet/Subnet et NSG
5. Création de 3 instances de VM à partir de l'image créée
	- Définir le sku à utiliser
	- Utiliser vnet/subnet et nsg créé précédement
	- Pas ip public
6. Création d'un load balancer de niveau 4

> TODO: Tests de montée en charge (ou éteindre 1 VM ?)

### Solution à partir de WebApp by code

1. Création de la webapp
2. Publication FTP/SSH/Gitlocal de l'application php
3. Setting du scale out

### Solution à partir de WebApp by Container

1. Création et publish image à partir Dockerfile (registry existante et mutualisé)
2. Création webapp à partir image
3. Setting du scale out

### Solution à partir de Azure Function ?

> func tools déjà installé sur cloud shell

1. Création de la function app
2. Création de la function en HTTP Trigger (verb GET)
3. Publication de l'application
4. Scale out ?

### Comparatif pour chaque solution

- Durée de la phase build
- Budget mensuel Azure

## Use Case 2

Le site Web PHP a évolué et il faut à présent mettre à jour toutes les instances de l'application qui ont été déployés.

**Objectifs formateur:**
- Démontrer les conséquences du choix de la solution quand il s'agit de maintenir une application

### Solution à partir de Virtual Machines

1. Création d'une VM à partir de l'image déjà créé
2. Mise à jour de l'application dans la VM
3. Création d'une nouvelle image à partir de la VM mise à jour
4. Comment mettre à jour les 3 VM qui ont été créés à partir de l'image précédente ???

### Solution à partir de WebApp by code

1. Publication FTP/SSH/Gitlocal de la nouvelle version de l'application php

### Solution à partir de WebApp by Container

1. Rebuild de l'image Docker avec la nouvelle version de l'application php
2. Mise à jour des webapp ??? (automatique ?)
	
### Solution à partir de Azure Function ?

1. Publication func tools de la nouvelle fonction
	
### Comparatif pour chaque solution

- Durée de la phase de mise à jour
	