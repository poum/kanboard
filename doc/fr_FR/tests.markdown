Tests automatisés
===============

[PHPUnit](https://phpunit.de/) est utilisé pour exécuter des tests automatisés sur Kanboard.

Vous pouvez exécuter des tests sur plusieurs bases de données (Sqlite, Mysql et Postgres) pour être sûr que le résultat sera le même partout.

Pré-requis
------------

- une machine Linux/Unix
- PHP
- PHPUnit installé
- Mysql et Postgresql (facultatif)
- Selenium (facultatif)
- Firefox (facultatif)

Tests unitaires
----------

### Tests avec Sqlite

Les tests Sqlite utilisent une base de données en mémoire, rien n'est écrit dans le système de fichiers.

Le fichier de confiuration PHPUnit est `tests/units.sqlite.xml`.
Depuis votre répertoire Kanboard, exécutez la commande `phpunit -c tests/units.sqlite.xml`.

Exemple:

```bash
phpunit -c tests/units.sqlite.xml

PHPUnit 5.0.0 by Sebastian Bergmann and contributors.

...............................................................  63 / 649 (  9%)
............................................................... 126 / 649 ( 19%)
............................................................... 189 / 649 ( 29%)
............................................................... 252 / 649 ( 38%)
............................................................... 315 / 649 ( 48%)
............................................................... 378 / 649 ( 58%)
............................................................... 441 / 649 ( 67%)
............................................................... 504 / 649 ( 77%)
............................................................... 567 / 649 ( 87%)
............................................................... 630 / 649 ( 97%)
...................                                             649 / 649 (100%)

Time: 1.22 minutes, Memory: 151.25Mb

OK (649 tests, 43595 assertions)
```

### Tests avec Mysql

Vous devez avoir installé Mysql ou Mariadb sur votre machine locale.

Par défaut, ces éléments d'authentification sont utilisés:

- Nom de machine: **localhost**
- Nom d'utilisateur: **root**
- Mot de passe: aucun 
- Base de données: **kanboard_unit_test**

A chaque exécution, la base de données est supprimée et créée de nouveau.

Le fichier de configuration PHPUnit est `tests/units.mysql.xml`.
Depuis votre répertoire Kanboard, exécutez la commande `phpunit -c tests/units.mysql.xml`.

### Tests avec Postgresql

Vous devez avoir installé Postgresql sur votre machine locale.

Par défaut, ces éléments d'authentification sont utilisés:

- Nom de machine: **localhost**
- Nom d'utilisateur: **postgres**
- Mot de passe: aucun 
- Base de données: **kanboard_unit_test**

Assurez-vous de permettre à l'utilisateur `postgres` de créer et de supprimer des bases de données.
La base de données est recréée à chaque exécution.

Le fichier de configuration PHPUnit est `tests/units.postgres.xml`.
Depuis votre répertoire Kanboard, exécutez la commande `phpunit -c tests/units.postgres.xml`.

Tests d'intégration
-----------------

Les tests d'intégration sont principalement utilisés pour tester l'API.
Les suites de tests effectuent de vrais appels HTTP à l'application qui est exécutée dans un conteneur.

### Pré-requis

- PHP
- Composer
- Système d'exploitation Unix (Mac OS ou Linux)
- Docker
- Docker Compose

### Exécuter les tests d'intégration

Les tests d'intégration utilisent des conteneurs docker.
Il y a 3 environnements différents disponibles pour exécuter les tests pour chacune des bases de données prises en charge.

Vous pouvez utiliser ces commandes pour exécuter chacune des suites de test:

```bash
# Exécuter les tests avec Sqlite
make integration-test-sqlite

# Exécuter les tests avec Mysql
make integration-test-mysql

# Exécuter les tests avec Postgres
make integration-test-postgres
```

Tests de recette
----------------

Les tests de recette (appelés également parfois tests de bout en bout ou tests fonctionnels) testent les fonctionnalités réelles de l'interface utilisateur dans un navigateur en utilisant Selenium.

De façon à exécuter ces tests, vous devez avoir installé un [serveur autonome Selenium ](http://www.seleniumhq.org/download/) et une version compatible de Firefox.

Le fichier de configuration PHPUnit est `tests/acceptance.xml`.
Une fois les applications Selenium et Kanboard en cours d'exécution, depuis le répertoire Kanboard, exécutez la commande `make test-browser`. Ceci va lancer la suite de tests et vous verrez Firefox d'ouvrir automatiquement et exécuter les actions définies dans les tests de recette.

Exemple:

```bash
$ make test-browser
PHPUnit 4.8.26 by Sebastian Bergmann and contributors.

..

Time: 5.59 seconds, Memory: 5.25MB

OK (2 tests, 5 assertions)
```


Intégration continue avec Travis-CI
-------------------------------------

Après chaque livraison de code poussée dans le dépôt principal, les tests unitaires sont exécutés sur 5 versions différentes de PHP: 

- PHP 7.0
- PHP 5.6
- PHP 5.5
- PHP 5.4
- PHP 5.3

Chaque version de PHP est testée sur les 3 bases de données prises en charge: Sqlite, Mysql et Postgresql.

Le fichier de configuration Travis `.travis.yml` se trouve dans le répertoire racine de Kanboard.
