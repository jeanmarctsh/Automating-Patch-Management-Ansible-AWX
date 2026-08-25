
<h1 align="center">   🚀 Projet: PATCH MANAGEMENT AVEC AWX ET ANSIBLE </h1>

__🔄 Etant dans un monde technologique en constante évolution, ce projet reste ouvert à l'ajout de nouvelles fonctionnalités, en fonction de l'évolution  des besoins__

---

## Problématique

Au sein d'une entreprise fortement exposée aux technologies, aux données sensibles et aux utilisateurs, la gestion d'un parc informatique  constitue un enjeu majeur pour assurer la disponibilité, la sécurité et la maîtrise des ressources IT. L'absence d'une vision globale de ces différents éléments constitue généralement un risque sécuritaire non négligeable pouvant à la longue ralentir ou compromettre le bon fonctionnement du système informatique. Afin de limiter ces risques, il est donc  nécessaire  de disposer d'une plateforme permettant de centraliser la gestion du parc, d'intégrer d'autres technologies pouvant rendre l'environnement  plus fluide, sécurisée et auditable.

## 📝 BUT

Déployer AWX grâce à AWX Operator afin de centraliser la gestion d'un environnement IT de manière fluide (exécution des différents playbooks Ansible via une interface graphique), sécurisée (gestion des clés SSH, RBAC et gestion des utilisateurs avec un annuaire LDAP), planifiée et surtout automatisée grâce aux mécanismes d'intégration et de synchronisation.


## A propos de l'outil

awx est un projet open source qui permet de centraliser et d'orchestrer ansible. Il fournit une interface web et une API permettant de gérer les inventaires statiques ou dynamiques, les credentials, les projets, les playbooks, les templates de jobs et les workflows, ainsi que de planifier et suivre l'exécution des automatisations.


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

## INSTALLATION DE L'OUTIL

La documentation complète de l'installation et de la configuration d'AWX Operator est disponible ici :

👉 [Consulter la documentation pour installer AWX Operator](https://github.com/jeanmarctsh/awx-operator-minikube/tree/awx/DAT)

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

## DEMO

Voici une démo de l'utilisation de l'outil en installant un paquet linux .deb depuis le serveur de référentiel local

1. Installation du package curl

👉 **[Voir la démonstration vidéo](Demo/install_curl_from_awx.mp4)**

2. Désinstallation du package curl

👉 **[Voir la démonstration vidéo](Demo/remove_curl_from_awx.mp4)**

---

## LIMITES

Bien qu'AWX permette de centraliser et d'automatiser la gestion d'un parc informatique, son déploiement et son utilisation nécessitent la prise en compte de plusieurs contraintes de sécurité et d'exploitation.

Voici quelques-uns des principaux points de vigilance :

## Limites et points de vigilance

| Limite | Description |
|---|---|
| Mises à jour | Les mises à jour d'AWX, de l'Operator et de Kubernetes nécessitent de vérifier la compatibilité entre les différentes versions. |
| Centralisation des credentials | La centralisation des clés SSH et autres credentials augmente l'impact potentiel d'une compromission. |
| Abstraction technique | L'interface AWX simplifie l'utilisation d'Ansible, mais peut masquer les mécanismes techniques exécutés en arrière-plan. |
| Erreurs d'automatisation | Une erreur dans un playbook ou un workflow peut être propagée à plusieurs machines simultanément. |
| Dépendance à Kubernetes | AWX Operator dépend du bon fonctionnement du cluster Kubernetes hébergeant AWX. |
| Disponibilité | Une indisponibilité d'AWX peut empêcher l'exécution des automatisations centralisées. |
| Montée en charge | Un nombre important de jobs simultanés peut nécessiter davantage de ressources CPU, RAM et stockage. |
| Contrôle des accès | Une mauvaise configuration des rôles et permissions peut donner des privilèges excessifs aux utilisateurs. |

__Note__

## Limites

Cette implémentation est centrée sur l'installation et la prise en main d'AWX Operator dans un environnement Minikube, notamment à travers la centralisation des tâches d'administration, l'exécution et l'automatisation des playbooks Ansible, la gestion des utilisateurs et des accès via LDAP/RBAC, ainsi que la synchronisation des projets et des inventaires. L'exploitation avancée, la haute disponibilité, la reprise après sinistre et le déploiement en production ne sont pas couverts dans cette version.

---

## Avantages

Il existe certains avantages comme:

| Avantage | Description |
|---|---|
| Autonomie | Permet de mieux comprendre et administrer l'environnement Ansible de manière autonome. |
| Réflexes techniques et sécuritaires | Favorise le développement de réflexes d'administration, d'automatisation et de sécurité lors de la conception et de l'exploitation de l'environnement. |
| Environnement d'apprentissage | Constitue un environnement pratique permettant de se familiariser avec les concepts d'Ansible Automation Platform (AAP). |
| Centralisation | Centralise les inventaires, credentials, projets, playbooks et workflows Ansible. |
| Automatisation | Permet de planifier et d'automatiser l'exécution des tâches d'administration. |
| Traçabilité | Permet de suivre les exécutions et de conserver un historique des opérations réalisées. |

---

## Vérifications préalables

AWX Operator reposant sur Kubernetes, il est nécessaire de vérifier l'état du cluster et de ses composants avant toute installation, modification ou opération de dépannage.

| Élément à vérifier | Commande | Objectif |
|---|---|---|
| Nœuds Kubernetes | `kubectl get nodes` | Vérifier que les nœuds sont disponibles |
| Pods | `kubectl get pods -A` | Vérifier l'état général des workloads |
| Namespaces | `kubectl get namespaces` | Vérifier la présence des espaces nécessaires |
| Operator | `kubectl get pods -n awx` | Vérifier l'état de l'AWX Operator |
| Ressources AWX | `kubectl get awx -n awx` | Vérifier l'état de l'instance AWX |
| Événements | `kubectl get events -n awx --sort-by=.lastTimestamp` | Identifier les erreurs récentes |
| Logs Operator | `kubectl logs -n awx deployment/awx-operator-controller-manager` | Analyser les erreurs de l'Operator |
| Services | `kubectl get svc -n awx` | Vérifier l'exposition des services |
| Stockage | `kubectl get pvc -n awx` | Vérifier les volumes persistants |



## ✍️ AUTEUR
- Nom : Ngandu Jean-Marc
- [![Email](https://img.shields.io/badge/Email-red?style=for-the-badge&logo=gmail)](mailto:jeanmarctshimbombo@gmail.com)
- [![LinkedIn](https://img.shields.io/badge/LinkedIn-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/jean-marc-ngandu-b60796222)
- [![GitHub](https://img.shields.io/badge/GitHub-black?style=for-the-badge&logo=github)](https://github.com/jeanmarctsh)
