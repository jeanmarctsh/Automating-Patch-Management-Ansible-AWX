# 🚀 Projet: PATCH MANAGEMENT AVEC AWX ET ANSIBLE

__🔄 Etant dans un monde technologique en constante évolution, ce projet reste ouvert à l'ajout de nouvelles fonctionnalités, en fonction de l'évolution  des besoins__

---

## 📍 SOMMAIRE

- [🚀 Projet: PATCH MANAGEMENT AVEC AWX ET ANSIBLE](#-projet-patch-management-avec-awx-et-ansible)
  - [📍 SOMMAIRE](#-sommaire)
  - [📝 OBJECTIF](#-objectif)
  - [🌟 WORKFLOW DU PROJET](#-workflow-du-projet)
  - [STRUCTURE GENERALE DU PROJET](#structure-generale-du-projet)
  - [🌐🖧 ARCHITECTURE PHYSIQUE DU PROJET](#-architecture-physique-du-projet)
  - [⚙️ MECANISME DE FONCTIONNEMENT DU PROJET](#️-mecanisme-de-fonctionnement-du-projet)
  - [🧰 OUTILS ET TECHNOLOGIES UTILISES](#-outils-et-technologies-utilises)
  - [✍️ AUTEUR](#️-auteur)

---

## 📝 OBJECTIF

Ce projet consiste à mettre en place une solution de gestion centralisée basée sur Ansible et AWX. Cette solution permet d’avoir une vision globale de différents correctifs (paquets, images, etc.) et d’effectuer des mises à niveau de manière plus sécurisée, contrôlée et planifiée. 
__Eléments clés : Sécurité (locale et utilisateur), l’automatisation, la synchronisation, le versioning et la planification.__

---

## 🌟 WORKFLOW DU PROJET

Voici le workflow général de notre projet:

![Schéma du Workflow](Images/WORKFLOW_GENERAL/WORKFLOW_GEN.png)

---

## STRUCTURE GENERALE DU PROJET 

```text
VERSION_FINALE/                 
├── Configuration/              
|   ├── ansible/                # Configuration de différents playbooks
|   ├── Awx_Kubernetes/        ├# Installation et configuration AWX-OPERATOR via minikube
|   ├── clients/                # Configuration de différentes machines clientes
|   ├── Gitea_docker/           # Installation via docker-compose du serveur Gitea pour le versionning
|   ├── Grafana_prometheus/     # Installation et supervision du parc local
|   ├── nginx/                  # Installation et configuration de nginx comme reverse proxy
|   ├── référentiel_local/      # Conception d'un dépôt local HTTP linux
|   └── windows_server/         # Installation AD et configuration des utilisateurs dédiés pour une connexion LDAD dans AWX
├── Demo/                       # Démonstration vidéo de différentes étapes (installation, désinstallation des paquets dans AWX)
├── Images/                     # Différentes captures du projet(syntaxe, code http, workflow, etc... )
├── Rapport_final/              # Documentation complète du projet (DAT)
└── README.md                   # Documentation principale du projet

```

## 🌐🖧 ARCHITECTURE PHYSIQUE DU PROJET

le projet comprend : 4 Serveurs Linux, 1 Serveur Windows et 2 machines clientes. 

* Configuration matérielle recommandée :
  
  1. Disque : SSD (recommandé pour la réactivité du cluster Kubernetes/AWX).
  2. RAM : 16 Go minimum (pour supporter l'ensemble des VMs et le cluster Minikube installé)

* Serveur Linux
  
  1. Linux : Pour le serveur AWX 
  2. Linux : Pour le serveur Gitea
  3. Linux : Pour le référentiel local
  4. Linux : Pour Ansible

* Serveur Windows

  1. Serveur Windows 2019


* Machines clientes
  
  1. Linux : client_1 (abstract)
  2. Linux : client_2 (marco1)

---

## ⚙️ MECANISME DE FONCTIONNEMENT DU PROJET

- Pour le serveur AWX : il sera le gestionnaire central de notre projet, synchronisé avec Gitea afin de récupérer automatiquement les différents fichiers de configuration. Et la mise à niveau  pourra se faire de manière contrôlée.

- Pour le serveur Gitea : il sera utilisé pour le versioning de nos différents fichiers de configuration et sera intégré à AWX pour une bonne synchronisation.

- Pour le serveur ansible: Sert d'environnement de développement pour tester les configurations avant de les pousser (Push) vers Gitea pour l'intégration finale.

- Pour le référentiel local : il permettra aux machines clientes d'effectuer une mise à niveau de manière sécurisée et contrôlée.

- Pour le serveur Windows 2019 : il permettra une authentification sécurisée afin d'intégrer l'utilisateur de service de l'Active Directory à AWX via le protocol LDAP.

- Pour les machines clientes : elles seront intégrées à AWX et via un utilisateur de service créé au niveau de ces dernières, les différentes configurations seront appliquées et les mises à jour ne se feront en local via le référentiel local déployé avec reprepro

---

## 🧰 OUTILS ET TECHNOLOGIES UTILISES

* Comme système d'exploitation nous avons utilisé :

  | ID | Système d'exploitation |
  |----|------------------------|
  | 1  | LINUX                  |
  | 2  | WINDOWS                |

* Comme outils pour mettre en place notre projet nous avons utilisé :


  | ID | OUTILS                                                                 | OBJECTIFS |
  |----|------------------------------------------------------------------------|-----------|
  | 1  | reprepro                                                               | Déploiement et mise en place d'un dépôt APT Local|
  | 2  | Serveur web (apache2 et nginx)                                          | Pour créer un lien symbolique du dépôt local, utiliser nginx comme reverse proxy, etc...    |
  | 3  | git et gitea                                                           | Pour le versionning et la gestion du code    |
  | 4  | Kubernetes                                                              | Déployer AWX-OPERATOR avec un cluster minikube |
  | 5  | Docker                                                                 | Déploiement et exécution de Gitea |
  | 6  | Openssl                                                                | Généreration des certificats de sécutité  |
  | 7  | Ansible                                                                | Configurer les machines clientes via différents Playbook |
  | 8  | Windows serveur                                                        | Pour une authentification sécurisée, gestion des droits nécessaires pour les utilisateurs |
  | 9 | Ssh                                                                    | Pour générer les clés SSH |
  | 10 | VS_code + MobaXterm                                                    | Accès à distance |
  | 11 | Rsync                                                                  | Pour le transfert de différents fichiers en local | 
  | 12 | LDAP                                                                   | Pour permettre la liaison entre un utilisateur (de service) de l'AD dans AWX |
  | 13 | Hyperviseur de type 2 (Vmware_workstation)                             | Construction et virtualisation de  l'architecture du projet |
    
---

## ✍️ AUTEUR
- Nom : Ngandu Jean-Marc
- [![Email](https://img.shields.io/badge/Email-red?style=for-the-badge&logo=gmail)](mailto:jeanmarctshimbombo@gmail.com)
- [![LinkedIn](https://img.shields.io/badge/LinkedIn-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/jean-marc-ngandu-b60796222)
- [![GitHub](https://img.shields.io/badge/GitHub-black?style=for-the-badge&logo=github)](https://github.com/jeanmarctsh)
