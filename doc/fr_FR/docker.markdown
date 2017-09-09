Comment exécuter Kanboard avec Docker ?
================================

Kanboard peut s'exécuter facilement avec [Docker](https://www.docker.com).

La taille de l'image est d'approximativement **70 Mo** et contient:

- [Alpine Linux](http://alpinelinux.org/)
- Le [gestionnaire de processus S6](http://skarnet.org/software/s6/)
- Nginx
- PHP 7

Le job cron de Kanboard est également exécutétous les jours à minuit.
La réécriture d'URL est activée dans le fichier de configuration inclus.

Quand le conteneur est en cours d'exécution, l'utilisation de la mémoire est d'environ **30 Mo**.

Utiliser la version stable
----------------------

To fetch the latest stable release of Kanboard use the tag **stable**:

```bash
docker pull kanboard/kanboard
docker run -d --name kanboard -p 80:80 -t kanboard/kanboard:stable
```

Utiliser la version de développement (construction automatique)
---------------------------------------------

Chaque nouvelle livraison dans le dépôt déclenche un nouvel assemblage par [Docker Hub](https://registry.hub.docker.com/u/kanboard/kanboard/).

```bash
docker pull kanboard/kanboard
docker run -d --name kanboard -p 80:80 -t kanboard/kanboard:latest
```

L'étiquette **latest** est la **version de développement** de Kanboard à utiliser à vos risques et périls.

Construire votre propre image Docker
---------------------------

Il y a un `Dockerfile` dans le dépôt Kanboard pour construire votre propre image.
Clonez le dépôt Kanboard et exécutez la commande suivante:

```bash
docker build -t votreutilisateur/kanboard:master .
```

ou

```bash
make docker-image
```

Pour exécuter votre conteneur à l'arrière plan sur le port 80:

```bash
docker run -d --name kanboard -p 80:80 -t votreutilisateur/kanboard:master
```

Volumes
-------

Vous pouvez attacher 2 volumes à votre conteneur:

- dossier des données: `/var/www/app/data`
- dossier des greffons: `/var/www/app/plugins`

Utilisez l'option `-v` pour monter un volume sur la machine hôte comme c'est décrit dans [la documentation officielle Docker](https://docs.docker.com/engine/userguide/containers/dockervolumes/).

Mettre à jour votre conteneur
----------------------

- Récupérez la nouvelle image
- Supprimez l'ancien conteneur
- Redémarrez un nouveau conteneur avec les mêmes volumes

Variables d'environnement
---------------------

La liste des variables d'environnement est disponible sur [cette page](env.markdown).

Fichiers de configuration
------------

- le conteneur inclut déjà un fichier de configuration personnalisé qui se trouve dans `/var/www/app/config.php`.
- vous pouvez enregistrer votre propre fichier de configuration dans le volume des données: `/var/www/app/data/config.php`.

Références
----------

- [images officielles de Kanboard](https://registry.hub.docker.com/u/kanboard/kanboard/)
- [Documentation de Docker](https://docs.docker.com/)
- [Version stable du Dockerfile](https://github.com/kanboard/docker)
- [Version de développement du Dockerfile](https://github.com/kanboard/kanboard/blob/master/Dockerfile)
