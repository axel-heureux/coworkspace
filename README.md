CoWork'Space - Application de Réservation d'Espaces de Coworking

Bienvenue sur le dépôt du projet CoWork'Space, une application web full-stack développée pour simplifier la gestion et la réservation de postes de travail et de salles de réunion dans un espace de coworking.

Note : Ce MVP (Minimum Viable Product) a été conçu et réalisé en 2 semaines par un développeur solo.

🚀 Stack Technique

Backend : Symfony 7 (PHP 8.2+), API RESTful

Frontend : React.js (Single Page Application)

Base de Données : Supabase avec Doctrine ORM

Authentification : JWT (LexikJWTAuthenticationBundle)

Documentation & Diagrammes : Markdown & Mermaid.js

🛠️ Prérequis

Avant de commencer, assurez-vous de disposer des éléments suivants sur votre machine :

PHP >= 8.2

Composer >= 2.x

Node.js >= 18.x & npm

Postgre >= 17

⚙️ Installation & Lancement

1. Cloner le projet

git clone https://github.com/votre-equipe/coworkspace.git
cd coworkspace


2. Configuration du Backend (Symfony)

# Se déplacer dans le dossier backend (ou à la racine si projet monorepo)
cd backend

# Installer les dépendances PHP
composer install

# Configurer les variables d'environnement (Copier .env en .env.local et régler la BDD)
cp .env .env.local

# Créer la base de données et exécuter les migrations
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate

# Générer les clés JWT pour l'authentification
php bin/console lexik:jwt:generate-keypair

# Lancer le serveur local backend
symfony server:start
# ou php -S localhost:8000 -t public


3. Configuration du Frontend (React)

# Dans un autre terminal, se déplacer dans le dossier frontend
cd frontend

# Installer les dépendances JavaScript
npm install

# Lancer le serveur de développement React
npm start


L'application sera accessible sur http://localhost:3000 et l'API sur http://localhost:8000.

📚 Documentation du Projet

La documentation complète et le dossier de conception se trouvent dans le répertoire /docs :

Architecture & Choix Techniques

Diagramme de Cas d'Utilisation

Modèle de Données (MCD / MLD)

Scénarios & Plans de Tests

👤 Auteur

Développeur : Équipe CoWork'Space (Projet Solo)

Établissement : La Plateforme - La Grande École du Numérique
