Foire aux questions
==========================

Pouvez-vous recommander un hébergeur pour Kanboard ?
------------------------------------------------------

Kanboard fonctionne bien avec tous kes grands fournisseurs d'hébergement virtuels privés tels que
[Digital Ocean](https://www.digitalocean.com/?refcode=4b541f47aae4),
[Linode](https://www.linode.com/?r=4e381ac8a61116f40c60dc7438acc719610d8b11) ou [Gandi](https://www.gandi.net/).

Pour obtenir les meilleures performances, choisissez un fournisseur avec des entrées/sorties disque rapides car
Kanboard utilise Sqlite par défaut.
Evitez les hébergeurs qui utilisent un point de montage NFS partagé.


J'ai une erreur "There is no suitable CSPRNG installed on your system"
-----------------------------------------------------------------------

Si vous utilisez PHP < 7.0, vous devez avoir activé l'extension openssl ou `/dev/urandom` accessible par l'application si elle est restreinte par une restriction `open_basedir`.


Page non trouvée et l'URL semble erronée (&amp;amp;)
--------------------------------------------------

- L'URL ressemble à `/?controller=auth&amp;action=login&amp;redirect_query=` au lieu de `?controller=auth&action=login&redirect_query=`
- Kanboard retourne une erreur "Page non trouvée"

Ce problème est causé par la configuration de PHP, la valeur de `arg_separator.output` n'est pas la valeur par défaut de PHP, il y a plusieurs façons de corriger ça:

Modifier la valeur directement dans votre `php.ini` si vous le pouvez:

```
arg_separator.output = "&"
```

Surchargez la valeur avec un `.htaccess`:

```
php_value arg_separator.output "&"
```

Autrement Kanboard essaiera de surcharger la valeur directement dans PHP.


Echec d'authentification avec l'API et Apache + PHP-FPM
--------------------------------------------------------

php-cgi sous Apache ne passe par défaut pas l'utilisateur/mot de passe HTTP Basic à PHP.
Pour que ce contournement fonctionne, ajoutez ces lignes à votre fichier `.htaccess`:

```
RewriteCond %{HTTP:Authorization} ^(.+)$
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
```


Problèmes connus avec eAccelerator
------------------------------

Kanboard ne fonctionne pas très bien avec [eAccelerator](http://eaccelerator.net).
Le problème peut causé par une page vierge ou un plantage d'Apache:

```
[Wed Mar 05 21:36:56 2014] [notice] child pid 22630 exit signal Segmentation fault (11)
```

Le meilleur moyen d'éviter ce problème est de désactiver eAccelerator ou de définir manuellement quels fichiers vous voulez mettre en cache à l'aide du paramètre de configuration `eaccelerator.filter`.

Le projet [eAccelerator semble mort et n'a pas connu de mise à jour depuis 2012](https://github.com/eaccelerator/eaccelerator/commits/master).
Nous recommandons de passer à la dernière version de PHP car elle embarque [OPcache](http://php.net/manual/en/intro.opcache.php).


Pourquoi le pré-requis minimum est PHP 5.3.3 ?
-----------------------------------------

Kanboard utilise la fonction `password_hash()` pour chiffrer les mots de passe mais elle n'est disponible que pour PHP >= 5.5.

Cependant, il y a un rétro portage pour les [versions antérieures de PHP](https://github.com/ircmaxell/password_compat#requirements).
Cette bibliothèque nécessite au moins PHP 5.3.7 pour fonctionner correctement.

Apparemment, Centos et Debian ont rétro porté des correctifs de sécurité donc PHP 5.3.3 doit être ok.

Kanboard v1.0.10 et v1.0.11 nécessite au moins PHP 5.3.7 mais cette modification a été annulée pour être compatible avec PHP 5.3.3 avec Kanboard >= v1.0.12


Comment tester Kanboard avec le serveur web embarqué de PHP ?
------------------------------------------------------

Si vous ne voulez pas installer un serveur web tel qu'Apache sur la machine locale, vous pouvez faire vos tests avec [le serveur web embarqué de PHP](http://www.php.net/manual/en/features.commandline.webserver.php):

```bash
unzip kanboard-VERSION.zip
cd kanboard
php -S localhost:8000
open http://localhost:8000/
```


Comment installer Kanboard sur Yunohost ?
------------------------------------

[YunoHost](https://yunohost.org/) est un système d'exploitation serveur destiné à rendre l'auto hébergement accessible à tout le monde.

Il existe un [paquet pour installer facilement Kanboard sur Yunohost](https://github.com/mbugeia/kanboard_ynh).


Où puis-je trouver une liste de projets liés ?
--------------------------------------------

- [client python pour l'API Kanboard de @freekoder](https://github.com/freekoder/kanboard-py)
- [Afficheur Kanboard de David Eberlein](https://github.com/davideberlein/kanboard-presenter)
- [CSV2Kanboard de @ashbike](https://github.com/ashbike/csv2kanboard)
- [Kanboard pour Yunohost de @mbugeia](https://github.com/mbugeia/kanboard_ynh)
- [script d'import Trello de @matueranet](https://github.com/matueranet/kanboard-import-trello)
- [extension Chrome de Timo](https://chrome.google.com/webstore/detail/kanboard-quickmenu/akjbeplnnihghabpgcfmfhfmifjljneh?utm_source=chrome-ntp-icon), [Source code](https://github.com/BlueTeck/kanboard_chrome_extension)
- [script client Python de @dzudek](https://gist.github.com/fguillot/84c70d4928eb1e0cb374)
- [script shell pour la migration de SQLite à MySQL/MariaDB de @oliviermaridat](https://github.com/oliviermaridat/kanboard-sqlite2mysql)
- [Hooks Git pour l'intégration avec Kanboard de Gene Pavlovsky](https://github.com/gene-pavlovsky/kanboard-git-hooks)


Existe-t'il des tutoriels sur Kanboard dans d'autres langages ?
-----------------------------------------------------------

- [Série d'article en allemand concernant Kanboard](http://demaya.de/wp/2014/07/kanboard-eine-jira-alternative-im-detail-installation/)


Astuces
----

- [La manière facile de supprimer la contrainte de nomage dans une base de données SQLite](https://github.com/kanboard/kanboard/issues/1508)
