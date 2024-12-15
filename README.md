# Présentation

Game-api est un projet visant à collecter, analyser et stocker des données provenant d'une api ouverte. Ces données seront ensuite exposées via une API RESTful, qui sera ensuite consommé par une application Web.

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
