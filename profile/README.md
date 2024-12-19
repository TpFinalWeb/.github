# Présentation

Game-api est un projet visant à collecter, analyser et stocker des données provenant d'une api ouverte. Ces données seront ensuite exposées via une API RESTful, qui sera ensuite consommé par une application Web.

## 🚀 **Technologies Utilisées**

### Backend
- **Node.js** : Environnement d'exécution pour JavaScript côté serveur.
- **Express** : Framework web pour Node.js facilitant la création de l'API RESTful.
- **MongoDB** : Base de données NoSQL pour stocker les informations sur les jeux.
- **Mongoose** : ODM (Object Data Modeling) pour interagir avec MongoDB en utilisant des objets JavaScript.
- **TypeScript** : Superset de JavaScript permettant un typage statique et une meilleure maintenabilité du code.
- **Cron** : Outil permettant de planifier et d’automatiser l’exécution de tâches à des intervalles de temps définis. 
### Frontend
- **React** : Bibliothèque JavaScript pour construire des interfaces utilisateur interactives.
- **Axios** : Pour interagir avec l'API backend.
- **Chart.js** : Bibliothèque pour la création de graphiques interactifs.
- **TypeScript** : Utilisé également côté frontend pour bénéficier de la vérification statique des types.

## 🛠️ **Architecture du Projet**

### Backend

L'architecture backend suit une approche modulaire avec les composants suivants :
1. **Services** : Contiennent la logique métier (ex : récupérer ou manipuler les données des jeux).
2. **Modèles** : Définissent la structure des documents dans MongoDB avec Mongoose.
3. **Interfaces** : Définissent les types des objets pour une meilleure gestion des données avec TypeScript.
4. **Contrôleurs** : Gèrent les requêtes HTTP et appellent les services pour effectuer des actions.
5. **Routes** : Définissent les points d'entrée (endpoints) de l'API.
6. **Middleware** : Permettent de gérer des actions intermédiaires comme l'authentification, la gestion des erreurs, etc.

Voici la structure des dossiers du Backend :

```
├── logs                                  # Logs des opérations /GET /POST /PUT /DELETE
├── src/
│   ├── controllers/                      # Contrôleurs Express pour gérer les routes
│   ├── interfaces/                       # Interfaces TypeScript
│   ├── middlewares/                      # Middlewares Express
│   ├── models/                           # Modèles de données
│   ├── routes/                           # Définition des routes Express
│   ├── services/                         # Services pour la logique métier
│   ├── utils/                            # Utilitaires du projet
│   ├── app.ts                            # Configuration de l'application Express
|   ├── tests/                            # Tests du projets
├── package.json                          # Fichier de configuration des dépendances et scripts
├── tsconfig.json                         # Configuration de TypeScript
```

### Frontend

L'architecture du frontend repose sur **React** avec des hooks pour gérer l'état et les effets secondaires. **Axios** est utilisé pour envoyer des requêtes HTTP au backend et **Chart.js** est utilisé pour la visualisation des données.

Voici la structure des dossiers du Frontend :

```
├── public/
├── src/
│   ├── assets/                      # Utilisé pour stocker les ressources statiques telles que les images
│   ├── axios/                       # Contient les fichiers liés aux appels des utilisateurs
│   ├── components/                  # Contient des composants React, qui sont des éléments d'interface utilisateur réutilisables
│   ├── pages/                       # Toutes les pages du frontend
│   ├── app.tsx/                     # Le composant principal de l’application
├── package.json                     # Fichier de configuration des dépendances et scripts
```

# Informations sur les données
# Source
L'API à partir de laquelle on prend nos données est nommé "Moby games". <br /><br />
Lien vers le site: [MobyGames](https://www.mobygames.com/)

MobyGames est un site web dédié au catalogage des jeux vidéo et de leurs créateurs. Il contient des informations sur presque 300,000 jeux éparpillés sur des centaines de plateformes allant des ordinateurs jusqu'au arcades. Les utilisateurs du site peuvent contribuer à la base de donnée en ajoutant des critiques et des votes sur leurs jeux du momment. C'est une ressources précieuse pour les amateurs de jeux vidéos.

Les données du site ne sont effectivement pas transmises en temps réel, il n'y a donc pas de nécessité à mettre a jour régulièrement notre base de donnée, Nous avons cependement prévu de faire une nouvelle requête a tous les 2 jours afin de rajouter les nouvelles informations dans notre base de donnée.

## Structure des données (requêtes pour obtenir un jeux)
Voici un exemple de données fournis par l'API de MobyGames lorsqu'on envoie une requête pour obtenir un jeu video:

```json
{
  "alternate_titles": [
    {
      "description": "Finnish title",
      "title": "Salaiset Kansiot"
    }
    "..."
  ],
  "description": "an extension of one of the most long-running television series of all time, The X-Files, ...",
  "game_id": 1,
  "genres": [
    {
      "genre_category": "Basic Genres",
      "genre_category_id": 1,
      "genre_id": 2,
      "genre_name": "Adventure"
    }
    "..."
  ],
  "moby_score": 7.1,
  "moby_url": "https://www.mobygames.com/game/1/the-x-files-game/",
  "num_votes": 57,
  "official_url": "https://www.hyperbole.com/xsite/",
  "platforms": [
    {
      "first_release_date": "1998",
      "platform_id": 3,
      "platform_name": "Windows"
    }
    "..."
  ],
  "sample_cover": {
    "height": 800,
    "image": "https://cdn.mobygames.com/covers/4062982-the-x-files-game-windows-front-cover.jpg",
    "platforms": [
      "Windows",
      "Macintosh"
    ],
    "thumbnail_image": "https://cdn.mobygames.com/872aed6c-aba4-11ed-a188-02420a00019a.webp",
    "width": 690
  },
  "sample_screenshots": [
    {
      "caption": "David Duchovny (from intro)",
      "height": 480,
      "image": "https://cdn.mobygames.com/screenshots/11073376-the-x-files-game-windows-david-duchovny-from-intro.jpg",
      "thumbnail_image": "https://cdn.mobygames.com/91b1118c-ac15-11ed-833b-02420a000131.webp",
      "width": 640
    }
    "..."
  ],
  "title": "The X-Files Game"
}
```
<br /><br />


La base de donnée contient assez d'information pour faire plusieurs analyses cependant nous avons décidé en amont de ce dont on avait besoin pour la réalisation de nos analyses. Voici un exemple de donnée une fois les données nécessaires extirpées:

```json
{
  "name": "Off the Rails 3D",
  "detailed_description": "No description",
  "num_vote": 0,
  "score": null,
  "sample_cover": {
    "height": 800,
    "image": "https://cdn.mobygames.com/covers/8637967-off-the-rails-3d-iphone-front-cover.jpg",
    "platforms": [
      "iPhone",
      "iPad"
    ],
    "thumbnail_image": "https://cdn.mobygames.com/4c489260-ac00-11ed-897b-02420a00012d.webp",
    "width": 800
  },
  "genres": [
    {
      "genre_category": "Basic Genres",
      "genre_category_id": 1,
      "genre_id": 1,
      "genre_name": "Action"
    }
    "..."
  ],
  "platforms": [
    {
      "first_release_date": "2019-11-28",
      "platform_id": 86,
      "platform_name": "iPhone"
    }
    "..."
  ]
}
```

Comme vous pouvez voir, les éléments qui ont étés filtrés sont:
- le titre alternatif
- les captures d'écran
- le lien vers Moby games 

## 🌐 **Déploiement et Configuration**

### Prérequis

1. **Node.js** et **npm** (ou **Yarn**) doivent être installés sur votre machine.
2. Une instance **MongoDB** doit être en fonctionnement.

### Installation Backend

1. Clonez ce dépôt :
  ```bash
   git clone https://github.com/TpFinalWeb/backend.git
  ```

2. Accédez au dossier backend :
  ```bash
   cd backend/
  ```

3. Installez les dépendances :
  ```bash
   npm i
  ```

4. Configurez le fichier .env avec les champs suivant:
  ```bash
   PORT=
   NODE_ENV=
   JWT_SECRET=
   SSL_KEY_PATH=
   SSL_CERT_PATH=
   MONGO_URI=
   SERVER_HTTP=
  ```
5. Démarrez le serveur :
  ```bash
   npm start
  ```

### Installation Frontend

1. Clonez ce dépôt :
  ```bash
   git clone https://github.com/TpFinalWeb/fe.git
  ```

2. Accédez au dossier backend :
  ```bash
   cd fe/
  ```

3. Installez les dépendances :
  ```bash
   npm i
  ```

4. Configurez le fichier .env avec les champs suivant:
  ```bash
   PORT=
  ```
5. Configurez le fichier src/axios/http-common.ts avec l'addresse et le port du backend:
  ```bash
   baseURL: "https://localhost:3005",
  ```

6. Démarrez le serveur :
  ```bash
   npm start
  ```

## 🛠️ **Utilisation de l'API**

### Endpoint CRUD

**GET /games/**
  - Description : Récupère tous les jeux.
  - Réponse : Liste des jeux avec leurs informations (nom, description, score, etc.).

**GET /games/:id**
  - Description : Récupère le jeu avec l'id fournie.
  - Réponse : Le jeux avec ses informations (nom, description, score, etc.).

**POST /games/**
  - Description : Crée un jeu et l'ajoute à la bd.
  - Réponse : Un message confirmant la création du jeu.

**PUT /games/:id**
  - Description : Modifier le jeu avec l'id fournie.
  - Réponse : Un message confirmant la modification du jeu.

**DELETE /games/:id**
  - Description : Supprimer le jeu avec l'id fournie.
  - Réponse : Un message confirmant la suppression du jeu.

### Endpoints Utilisateur

**POST /register**
  - Description : Créer un nouvel utilisateur.
  - Réponse : Un message confirmant la création de l'utilisateur.

**POST /login**
  - Description : Se connecter à son compte.
  - Réponse : Un message confirmant la connexion de l'utilisateur.

Sure, here is the raw content of the "Endpoints Statistiques" section:


### Endpoints Statistiques

**GET /getPlatformsPopularity**
- Description: Obtenir la popularité des plateformes basée sur les votes et le nombre de jeux.
- Réponse:
  - 200: Une liste de plateformes avec leur popularité moyenne.
  - 500: Erreur interne du serveur.

**GET /getPlatformsWhereGamesReleaseFirst**
- Description: Obtenir les plateformes où les jeux sont d'abord publiés.
- Réponse:
  - 200: Une liste de plateformes avec le nombre de jeux publiés en premier.
  - 500: Erreur interne du serveur.

**GET /getGamesPerPlatforms**
- Description: Obtenir le nombre de jeux par plateforme.
- Réponse:
  - 200: Une liste de plateformes avec le nombre de jeux.
  - 500: Erreur interne du serveur.

**GET /getGenrePopularity**
- Description: Obtenir la popularité des genres basée sur le nombre de jeux.
- Réponse:
  - 200: Une liste de genres avec leur popularité.
  - 500: Erreur interne du serveur.

**GET /getGenreYearlyPopularity**
- Description: Obtenir la popularité annuelle d'un genre spécifique.
- Paramètres:
  - genre_name (query, requis): Le nom du genre.
- Réponse:
  - 200: Une liste de données de popularité annuelle pour le genre spécifié.
  - 400: Veuillez fournir un nom de genre.
  - 500: Erreur interne du serveur.

**GET /getNumOfGameOfEachGenre**
- Description: Obtenir le nombre de jeux pour chaque genre.
- Réponse:
  - 200: Une liste de genres avec le nombre de jeux.
  - 500: Erreur interne du serveur.

**GET /getPlatPopularityBy2Months**
- Description: Obtenir la popularité des plateformes sur une période de deux mois spécifique.
- Paramètres:
  - startMonth (query, requis): Le mois de début (1-12).
  - endMonth (query, requis): Le mois de fin (1-12).
- Réponse:
  - 200: Une liste de plateformes avec leur popularité sur la période spécifiée.
  - 400: Veuillez fournir un mois valide.
  - 500: Erreur interne du serveur.

**GET /getTop10GamesOfPlatform**
- Description: Obtenir les 10 meilleurs jeux d'une plateforme spécifique.
- Paramètres:
  - platform_name (query, requis): Le nom de la plateforme.
- Réponse:
  - 200: Une liste des 10 meilleurs jeux pour la plateforme spécifiée.
  - 400: Veuillez fournir un nom de plateforme.
  - 500: Erreur interne du serveur.

**GET /getTop10GamesOfGenre**
- Description: Obtenir les 10 meilleurs jeux d'un genre spécifique.
- Paramètres:
  - genre_name (query, requis): Le nom du genre.
- Réponse:
  - 200: Une liste des 10 meilleurs jeux pour le genre spécifié.
  - 400: Veuillez fournir un nom de genre.
  - 500: Erreur interne du serveur.

**GET /getPlatformQualityByTime**
- Description: Obtenir la qualité d'une plateforme au fil du temps.
- Paramètres:
  - platform_name (query, requis): Le nom de la plateforme.
- Réponse:
  - 200: Une liste de données de qualité pour la plateforme spécifiée au fil du temps.
  - 400: Veuillez fournir un nom de plateforme.
  - 500: Erreur interne du serveur.

**GET /getGenreQualityByTime**
- Description: Obtenir la qualité d'un genre au fil du temps.
- Paramètres:
  - genre_name (query, requis): Le nom du genre.
- Réponse:
  - 200: Une liste de données de qualité pour le genre spécifié au fil du temps.
  - 400: Veuillez fournir un nom de genre.
  - 500: Erreur interne du serveur.

**GET /getGOTY**
- Description: Obtenir le jeu de l'année (GOTY) pour chaque année.
- Réponse:
  - 200: Une liste des GOTY pour chaque année.
  - 500: Erreur interne du serveur.

**GET /getAllGenres**
- Description: Obtenir une liste de tous les genres.
- Réponse:
  - 200: Une liste de tous les genres.
  - 500: Erreur interne du serveur.

**GET /getAllPlatforms**
- Description: Obtenir une liste de toutes les plateformes.
- Réponse:
  - 200: Une liste de toutes les plateformes.
  - 500: Erreur interne du serveur.

        
## 📈 **Visualisation de l'API**
Les données des jeux sont affichées sous forme de graphiques à l'aide de Chart.js dans l'interface frontend. Ces graphiques peuvent inclure des statistiques comme le nombre de votes, le score moyen, et d'autres métriques pertinentes extraites des jeux.

## 💡 **Défis et Solutions**
1. Trouver une API qui fonctionne bien avec MongoDB et qui a assez de données.
  - Solutions : Nous avons cherché une API qui retourne des valeurs qui s'entreposent facilement dans MongoDB et qui à plus de 300 000 données.

2. Créer les agrégations afin de prendre les données qu'on veut afficher sur des graphiques
  - Solutions : Faire de la recherche dans plusieurs documentations en ligne

## 📊 **Résultats des Tests**
## Vue d’Ensemble
Toutes les suites de tests ont été exécutées avec succès, garantissant que les services backend fonctionnent comme prévu. Voici un aperçu détaillé des résultats :
  ```bash
    Run npm test

> backend@1.0.0 test
> set NODE_ENV=test && jest --detectOpenHandles

PASS src/tests/games.test.ts (7.744 s)
  ● Console

    console.log
      Connected to MongoDB

      at src/utils/mongodb.utils.ts:10:21

    console.log
      {"level":"info","message":"GET /games/:id - getGame","timestamp":"2024-12-18T00:27:14.538Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      Error fetching games:

      at Function.getGame (src/services/game.service.ts:14:21)

    console.log
      {"level":"info","message":"GET /games/:id - Game not found","timestamp":"2024-12-18T00:27:14.570Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"POST /games/ - gameAdded","timestamp":"2024-12-18T00:27:14.643Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"POST /games/ - MissingInfo","timestamp":"2024-12-18T00:27:14.660Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"PUT /games/:id - GameModified","timestamp":"2024-12-18T00:27:14.760Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"PUT /games/:id - GameNotFound","timestamp":"2024-12-18T00:27:14.798Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"DELETE /games/:id - GameDeleted","timestamp":"2024-12-18T00:27:14.860Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"error","message":"DELETE /games/:id - Erreur interne du serveur","timestamp":"2024-12-18T00:27:14.893Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

PASS src/tests/users.test.ts
  ● Console

    console.log
      Connected to MongoDB

      at src/utils/mongodb.utils.ts:10:21

    console.log
      {"level":"info","message":"POST /register - UserCreated","timestamp":"2024-12-18T00:27:17.281Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"POST /register - IncorectFormat","timestamp":"2024-12-18T00:27:17.307Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"POST /register - IncorectFormat","timestamp":"2024-12-18T00:27:17.329Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"POST /login - UserConnected","timestamp":"2024-12-18T00:27:17.490Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"POST /login - MissingFields","timestamp":"2024-12-18T00:27:17.507Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)

    console.log
      {"level":"info","message":"POST /login - WrongEmailOrPassword","timestamp":"2024-12-18T00:27:17.643Z"}

      at Console.log (node_modules/winston/lib/winston/transports/console.js:87:23)


Test Suites: 2 passed, 2 total
Tests:       14 passed, 14 total
Snapshots:   0 total
Time:        10.616 s
Ran all test suites.
  ```
