Variables d'environnement
=====================

Les variables d'environnement peuvent être utiles quand Kanboard est déployé dans un conteneur (Docker).

| Variable                 | Description                                                                                                                     |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| DATABASE_URL             | `[type de base de données]://[nom utilisateur]:[mot de passe]@[hote]:[port]/[nom de la base de données]`, exemple: `postgres://foo:foo@monserveur:5432/kanboard`   |
| DEBUG                    | Active/Désactive le mode de débogage: "true" ou "false"                                                                                    |
| API_AUTHENTICATION_TOKEN | Jeton personnalisé de l'API                                                                                                                |
