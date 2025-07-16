# Projet MONITORACK - BTS CIEL 2025

## Présentation du projet

Le projet **MONITORACK** est réalisé dans le cadre de l'épreuve E6 du BTS CIEL (Informatique et Réseaux), session 2025. Ce projet vise à mettre en place un système de surveillance centralisée pour des baies informatiques équipées d'onduleurs. Il permet de monitorer l'état des équipements (température, humidité, état des onduleurs, etc.) afin d'assurer la continuité de service en cas de panne de courant.

**Partenaire professionnel**: CI Solutions  
**Étudiants chargés du projet**:
- VIGNEAU Noah
- SHEPHO Raad
- MATTI YOUSIF Youssif
- DUFAU Esteban

**Professeurs ou Tuteurs responsables**:
- DARRIBEYROS Lilian
- DELBOY Laurent
- METREF William (PC)
- NAUDY Patrice

## Contexte et Objectifs

CI Solutions est une entreprise spécialisée dans le déploiement et la gestion de serveurs dans des baies informatiques. L'entreprise souhaite implémenter un système centralisé permettant de surveiller l'état des onduleurs ainsi que les conditions environnementales des baies, comme la température et l'humidité.

### Problématique
Les onduleurs utilisés actuellement (APC Smart UPS 3000VA) ne permettent pas de surveillance à distance ni d'alerte en cas de défaillance. Cela représente un risque pour la continuité du service, notamment en cas de coupure de courant.

### Solution
L'objectif du projet est de développer une **passerelle de surveillance** capable de :
- Acquérir et stocker les données des onduleurs à intervalles réguliers.
- Suivre l'état des onduleurs et alerter en cas de coupure de courant.
- Surveiller les intrusions (ouverture de la baie).
- Surveiller la température et l'humidité dans la baie.

### Technologies et Protocoles
- **AP9631** : carte d'extension pour récupérer les données de l'onduleur via SSH/TELNET, HTTP ou Modbus TCP.
- **Capteurs** : température, humidité et capteurs de contact pour les intrusions.
- **LoraWAN** : pour assurer la communication entre la passerelle onduleur et le serveur Monitorack, indépendamment du réseau informatique principal.
- **Serveur Monitorack** : pour centraliser et visualiser les données.

## Architecture du Système

Voici un diagramme de l'infrastructure prévue :

![Diagramme d'Infrastructure](./assets/visio (2).png)

Le système est constitué de plusieurs composants :
- **Passerelle Onduleur** : collecte les données des onduleurs et des capteurs, puis les envoie à une passerelle LoRaWAN.
- **Serveur Monitorack** : situé sur la DMZ de l'entreprise, il reçoit et stocke les données.
- **Interface Web** : pour consulter en temps réel les données des baies.

## Diagramme des Cas d'Utilisation

![Diagramme des Cas d'Utilisation](./assets/screen%20diagramme%20usecase.PNG)

## Tâches des Étudiants

### VIGNEAU Noah (Passerelle Onduleur / Serveur)
- Développement de l'application de collecte et de stockage des données des onduleurs.
- Création de modules de récupération des valeurs de la carte AP9631 et du capteur DHT11.
- Développement de l'ordonnancement de l'application et gestion des logs.

### SHEPHO Raad (Passerelle Onduleur / Serveur)
- Gestion de la communication avec la carte AP9631 et la passerelle LoRaWAN.
- Paramétrage du réseau LoraWAN et du firewall de l'entreprise.

### MATTI YOUSIF Youssif (Serveur de stockage des données)
- Installation et configuration du serveur Monitorack sous Ubuntu Server.
- Développement des webservices pour le stockage et la visualisation des données.

### DUFAU Esteban (Serveur de stockage des données - Frontend)
- Développement de l'interface web pour visualiser en temps réel les données des baies.
- Création de fonctionnalités d'exportation des données.

## Matériels et Logiciels Utilisés

### Matériel
- **Carte AP9631** pour les onduleurs
- **Capteur DHT11** (température et humidité)
- **Passerelle LoRaWAN** Milesight
- **Raspberry Pi 3** pour la passerelle onduleur
- **Serveurs sous Ubuntu Server 22.04** (virtualisés)

### Logiciels
- **C++** avec Qt pour la programmation des modules embarqués
- **Symfony 5** pour le développement du backend et de l'interface web
- **MariaDB** pour la gestion des données
- **Framework Twig** et **Bibliothèques Javascript** pour le frontend

## Installation

1. **Prérequis** :
   - Raspberry Pi 3 avec Raspbian installé.
   - Serveur Ubuntu 22.04 pour héberger Monitorack.
   - Accès à un réseau LoRaWAN pour la communication.

2. **Étapes d'installation** :
   - Configurer la passerelle LoRaWAN et la connecter au réseau.
   - Déployer les services backend sur le serveur Monitorack.
   - Installer les dépendances pour le frontend et les modules de surveillance.

## Tests et Validation

- **Tests unitaires** : Chaque module développé sera testé individuellement.
- **Tests d'intégration** : L'ensemble du système sera testé pour garantir son bon fonctionnement.

## Documentation

- **Documentation technique** : Un document détaillant l'architecture du projet et le processus de développement est disponible dans le répertoire `docs`.

## Licence

Ce projet est sous licence MIT.

---

# Fonctionnement du Dépôt GitHub

Ce dépôt GitHub est organisé pour faciliter le développement et la gestion du projet. Voici une brève explication du fonctionnement, ainsi que des règles à suivre pour contribuer efficacement :

### Structure du dépôt

- **/src** : Contient tous les fichiers sources du projet, y compris le code pour la passerelle onduleur, les modules de communication et le backend.
- **/assets** : Images, diagrammes et autres fichiers visuels utilisés dans la documentation.
- **/docs** : Documentation technique et rapports de développement.
- **/frontend** : Code relatif à l'interface utilisateur (IHM) pour la visualisation des données des baies.

### Branches

Le projet utilise des branches pour organiser le développement de manière modulaire :
- **main** : Branche principale contenant le code stable.
- **dev** : Branche de développement pour les nouvelles fonctionnalités et tests.
- **feature/<nom de la fonctionnalité>** : Branche spécifique pour chaque fonctionnalité développée.
- **fix/<nom du bug ou de la correction>** : Branche dédiée à la correction d'un bug ou d'un problème.

### Workflow Git

1. **Fork** le projet pour votre propre copie.
2. **Clonez** le dépôt sur votre machine locale.
3. **Créez une branche** pour la fonctionnalité ou la correction que vous souhaitez développer :
   - Si vous travaillez sur une **nouvelle fonctionnalité**, créez une branche avec le préfixe `feat/` suivi du nom de la fonctionnalité, par exemple : `feat/ajout-capteur-humidite`.
   - Si vous travaillez sur un **bug fix**, créez une branche avec le préfixe `fix/` suivi de la description du bug, par exemple : `fix/correction-température-capteur`.
4. **Développez vos modifications** sur cette branche, en effectuant des commits réguliers et en veillant à ce que vos messages de commit soient clairs et explicites.
5. **Push** vos changements vers votre dépôt distant sur GitHub.
6. **Soumettez une pull request** (PR) pour intégrer vos modifications dans la branche `dev`. Assurez-vous de bien décrire les changements dans la PR, notamment le contexte de la fonctionnalité ou du bug corrigé.
7. **Revues de code** : Un ou plusieurs membres de l'équipe examineront votre PR pour s'assurer que les modifications respectent les bonnes pratiques et que le code est fonctionnel.

### Règles de Nommage des Branches

- **Nouvelles fonctionnalités** : Utilisez le préfixe `feat/` suivi d'un nom descriptif de la fonctionnalité, par exemple :  
  `feat/ajout-capteur-humidite`, `feat/système-alertes`.
  
- **Corrections de bugs** : Utilisez le préfixe `fix/` suivi d'une brève description du problème, par exemple :  
  `fix/bug-lecture-valeurs-onduleur`, `fix/probleme-temperature-capteur`.

- **Autres types de changements** : Pour des modifications spécifiques comme la mise à jour de la documentation ou des améliorations techniques, utilisez les préfixes suivants :
  - `docs/` pour des changements dans la documentation, ex. : `docs/ajout-section-presentation`.
  - `chore/` pour les tâches d'entretien général, ex. : `chore/mise-a-jour-dependances`.

### Exemple de Processus de Contribution

1. Forker le dépôt principal.
2. Cloner le dépôt forké localement :  
   `git clone https://github.com/votre-utilisateur/monitorack.git`
3. Créer une branche pour la fonctionnalité ou le bug à corriger :  
   `git checkout -b feat/ajout-interface-web`
4. Effectuer les modifications et tester votre code.
5. Ajouter les fichiers modifiés à l'index Git :  
   `git add .`
6. Committer les changements avec un message clair :  
   `git commit -m "Ajout de l'interface web pour la visualisation des données"`
7. Pusher les modifications vers votre dépôt distant :  
   `git push origin feat/ajout-interface-web`
8. Créer une **pull request** sur GitHub en ciblant la branche `dev` du dépôt principal.

### Bonnes pratiques pour les commits

- Les messages de commit doivent être clairs et explicites.
- Utilisez un format de message de commit structuré :  
  - **Ajout** : `feat/ajout-nouvelle-fonctionnalité`  
  - **Correction** : `fix/correction-bug-description`
  - **Modification** : `chore/amélioration-performance`

En suivant ces étapes et ces règles, vous contribuez efficacement au projet tout en maintenant une structure claire et facile à gérer pour toute l'équipe de développement.

---

Pour toute question ou commentaire, n'hésitez pas à nous contacter à [prjmonitorack@gmail.com].
