Déployer Kanbard sur Heroku
=========================

Vous pouvez essayer Kanboard gratuitement sur [Heroku](https://www.heroku.com/).
Vous pouvez utiliser ce bouton d'installation en un clic ou suivre la procédure manuelle ci-dessous:

[![Deployer](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/kanboard/kanboard)

Pré-requis
------------

- compte Heroku, vous pouvez utiliser un compte gratuit
- Outils Heroku en ligne de commande installés

Procédure manuelle
-------------------

```bash
# Obtenir la dernière version de développement
git clone https://github.com/kanboard/kanboard.git
cd kanboard

# Pousser le code sur Heroku (vous pouvez également utiliser SSH si git via HTTP ne fonctionne pas)
heroku create
git push heroku master

# Démarrer une nouvelle dyno avec une base de données Postgresql
heroku ps:scale web=1
heroku addons:add heroku-postgresql:hobby-dev

# Ouvrez votre navigateur
heroku open
```

Limitations
-----------

Le stockage sur le disque local sur Heroku est éphémère:

- Les fichiers téléchargés ne sont pas persistants après un redémarrage. Vous pourriez vouloir installer un greffon pour enregistrer vos fichiers chez un fournisseur de stockage de cloud tel que [Amazon S3](https://github.com/kanboard/plugin-s3).
- Les greffons installés via l'interface web sont enregistrés sur le système de fichiers local. Vous devriez inclure et déployer vos greffons avec votre propre copie de Kanboard.

Certaines fonctionnalités de Kanboard nécessitent que vous exécutiez [un job quotidien en tâche de fond](cronjob.markdown).
