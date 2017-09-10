Comment construire des éléments (fichiers Javascript et CSS)
==============================================

Les fichiers de feuilles de style et Javascript sont fusioonés ensemble et sont minifiés.

- les fichiers CSS originels sont enregistrés dans le dossier `assets/css/src/*.css`
- le code Javascript originel est enregistré dans le dossier `assets/js/src/*.js`
- `assets/*/vendor.min.*` sont les dépendances externes fusionnées et minifiées
- `assets/*/app.min.*` sont le code source de l'application fusionné et minifié

Pré-requis
------------

- [NodeJS](https://nodejs.org/) avec `npm`

Construire les fichiers Javascript et CSS
---------------------------------

Kanboard utilise [Gulp](http://gulpjs.com/) pour construire les éléments et [Bower](http://bower.io/) pour gérer les dépendances.
Ces outils sont installés comme dépendances NodeJS dans le projet.

### Tout exécuter

```bash
make static
```

### Construire `vendor.min.js` et `vendor.min.css`

```bash
gulp vendor
```

### Construire `app.min.js`

```bash
gulp js
```

### Construire `app.min.css`

```bash
gulp css
```

Notes
-----

Construire des éléments n'est pas possible depuis l'archive de Kanboard, vous devez cloner le dépôt.
