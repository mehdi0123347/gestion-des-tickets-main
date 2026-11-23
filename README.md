# Gestion des tickets

Application web de gestion des demandes de support. Elle centralise la création et le suivi des tickets, leur attribution aux techniciens et les échanges entre les personnes concernées.

## Fonctionnalités

- **Employés** : créer, consulter et suivre leurs tickets, ajouter des commentaires et gérer leur profil.
- **Techniciens** : consulter les tickets qui leur sont attribués, mettre à jour leur suivi, commenter et gérer leur profil.
- **Administrateurs** : gérer les utilisateurs, les tickets et les référentiels (catégories, priorités et statuts).
- **Suivi des demandes** : associer chaque ticket à son créateur, à une catégorie, à une priorité et à un statut ; possibilité d'attribution à un technicien.
- **Notifications** : notifications dans l'application et courriel lors de l'attribution d'un ticket (selon la configuration de messagerie).
- **Authentification et accès par rôle** : espaces distincts pour les administrateurs, les employés et les techniciens.

## Technologies

- PHP 8.2 ou supérieur
- Laravel 11
- SQLite par défaut (autres moteurs configurables via Laravel)
- Blade, Vite, Tailwind CSS et JavaScript
- Composer et npm

## Prérequis

Installez PHP et les extensions requises par Laravel, Composer, Node.js et npm. Pour utiliser la base par défaut, l'extension SQLite de PHP doit être activée.

## Installation

Depuis la racine du projet :

```bash
composer install
npm ci
```

Créez le fichier d'environnement et générez la clé de l'application.

**PowerShell**

```powershell
Copy-Item .env.example .env
php artisan key:generate
New-Item -ItemType File -Path database/database.sqlite -Force
```

**macOS / Linux**

```bash
cp .env.example .env
php artisan key:generate
touch database/database.sqlite
```

Dans `.env`, vérifiez que `DB_CONNECTION=sqlite`. Vous pouvez renseigner les paramètres `DB_*` si vous utilisez un autre moteur de base de données. Configurez également les paramètres `MAIL_*` pour envoyer de vrais courriels ; la configuration d'exemple journalise les messages au lieu de les transmettre.

Créez ensuite le schéma de base de données et compilez les ressources :

```bash
php artisan migrate --seed
npm run build
```

Le seeder fourni crée un utilisateur de démonstration. Il ne configure pas à lui seul un environnement complet avec tous les rôles et comptes nécessaires ; aucun identifiant de connexion de production n'est fourni.

## Lancer l'application

Dans un premier terminal :

```bash
php artisan serve
```

Ouvrez l'adresse indiquée par Artisan, généralement [http://127.0.0.1:8000](http://127.0.0.1:8000), puis accédez à la page de connexion. Pour développer les ressources front-end avec rechargement à chaud, lancez dans un autre terminal :

```bash
npm run dev
```

## Tests

Lancer la suite de tests Laravel :

```bash
php artisan test
```

## Structure du projet

```text
app/                  Contrôleurs, modèles, middleware et courriels
database/migrations/  Schéma de la base de données
database/seeders/     Données de démonstration
resources/views/      Interfaces Blade par rôle
resources/css/        Feuilles de style
resources/js/         JavaScript de l'application
routes/web.php        Routes web et accès par rôle
tests/                Tests automatisés
```

## Configuration et déploiement

Ne publiez jamais le fichier `.env` ni les clés ou mots de passe qu'il contient. Pour un déploiement, configurez un environnement sécurisé, désactivez le mode debug (`APP_DEBUG=false`), définissez les paramètres de base de données et de messagerie adaptés, puis suivez le guide de déploiement de [Laravel](https://laravel.com/docs/11.x/deployment).

## Licence

Le projet déclare actuellement la licence MIT dans `composer.json`. Vérifiez les droits et les conditions applicables avant toute redistribution.
