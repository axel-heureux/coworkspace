# 01. Architecture et Choix Techniques

## 1. Vue d'Ensemble du Projet

* **Projet :** CoWork'Space MVP
* **Durée :** 2 semaines
* **Format :** Développeur Solo
* **Architecture :** Découplée (Frontend SPA / Backend API REST)

---

## 2. Stack Technique Retenue

| Layer | Technologie | Description / Rôle |
| :--- | :--- | :--- |
| **Backend** | **Symfony 7** (PHP 8.2+) | Framework Backend puissant pour fournir l'API RESTful. |
| **Frontend** | **React** | Framework JS pour créer une interface utilisateur dynamique (SPA). |
| **Base de Données** | **MySQL** | SGBDR relationnel pour la persistance des données. |
| **ORM** | **Doctrine ORM** | Mapping objet-relationnel pour la gestion de la BDD. |
| **Authentification** | **JWT** | Tokens sécurisés via `LexikJWTAuthenticationBundle`. |

---

## 3. Pourquoi le Framework Symfony pour le Backend ?

Face au défi d'exécuter ce projet **seul en seulement 2 semaines** (au lieu d'une équipe de 3 personnes), l'utilisation de Symfony par rapport à du PHP natif est le choix le plus stratégique pour garantir vitesse, propreté et sécurité.

### A. Développement Accéléré (Time-to-Market)
Développer en PHP natif nécessiterait de coder à la main un routeur, la gestion d'injection de dépendances, le hashing de mot de passe et le middleware d'API REST. 
Grâce à Symfony et au composant `MakerBundle`, il est possible de générer les entités, contrôleurs et migrations en quelques lignes de commande CLI. Cela représente un gain de temps crucial.

### B. Découpage Modulaire & Architecture Propre
L'architecture découplée API REST / Front SPA exige une séparation stricte des responsabilités. Symfony isole parfaitement le Backend grâce aux contrôleurs d'API et au conteneur de services (Dependency Injection), garantissant un code évolutif et facile à maintenir.

### C. Écosystème de Packages Éprouvés
Au lieu de réinventer la roue, le projet s'appuie sur des composants matures :
* **Doctrine ORM :** Manipulation rapide de la BDD et protection native contre les injections SQL.
* **LexikJWTAuthenticationBundle :** Sécurisation robuste et clé-en-main des routes API via des tokens JWT.
* **Symfony Mailer & Serializer :** Gestion des notifications par email (confirmation, rappels 24h) et conversion sérialisée des objets PHP en JSON.
* **DompdfBundle / KnpSnappyBundle :** Génération rapide des exports PDF pour les réservations.

### D. Sécurité Native
`Symfony Security` prend en charge le hachage sécurisé des mots de passe (Bcrypt/Argon2i) et le contrôle d'accès basé sur les rôles (`ROLE_USER`, `ROLE_ADMIN`), évitant ainsi toute faille de sécurité majeure.