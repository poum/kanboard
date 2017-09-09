Interface en ligne de commande
======================

Kanboard fournit une interface simple en ligne de commande qui peut être utilisée depuis n'importe quel terminal Unix.
Cet outil peut être utilisé seulement depuis la machine locale.

Cette fonctionnalité est utile pour exécuter des commandes en dehors des processus du serveur web.

Utilisation
-----

- Ouvrir un terminal et allez dans votre répertoire Kanboard (exemple: `cd /var/www/kanboard`)
- Exécutez la commande `./cli` ou `php cli`

```bash
Kanboard version master

Usage:
  command [options] [arguments]

Options:
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Available commands:
  cronjob                            Execute daily cronjob
  help                               Displays help for a command
  job                                Execute individual job (read payload from stdin)
  list                               Lists commands
  worker                             Execute queue worker
 db
  db:migrate                         Execute SQL migrations
  db:version                         Show database schema version
 export
  export:daily-project-column-stats  Daily project column stats CSV export (number of tasks per column and per day)
  export:subtasks                    Subtasks CSV export
  export:tasks                       Tasks CSV export
  export:transitions                 Task transitions CSV export
 locale
  locale:compare                     Compare application translations with the fr_FR locale
  locale:sync                        Synchronize all translations based on the fr_FR locale
 notification
  notification:overdue-tasks         Send notifications for overdue tasks
 plugin
  plugin:install                     Install a plugin from a remote Zip archive
  plugin:uninstall                   Remove a plugin
  plugin:upgrade                     Update all installed plugins
 projects
  projects:daily-stats               Calculate daily statistics for all projects
 trigger
  trigger:tasks                      Trigger scheduler event for all tasks
 user
  user:reset-2fa                     Remove two-factor authentication for a user
  user:reset-password                Change user password
```

Commandes disponibles
------------------

### Export CSV des tâches

Usage:

```bash
./cli export:tasks <id_projet> <date_debut> <date_de_fin>
```

Exemple:

```bash
./cli export:tasks 1 2014-10-01 2014-11-30 > /tmp/my_custom_export.csv
```

Les données CSV sont envoyées vers `stdout`.

### Export CSV des sous-tâches

Usage:

```bash
./cli export:subtasks <id_projet> <date_debut> <date_de_fin>
```

Exemple:

```bash
./cli export:subtasks 1 2014-10-01 2014-11-30 > /tmp/my_custom_export.csv
```

### Export CSV des transitions des tâches

Usage:

```bash
./cli export:transitions <id_projet> <date_debut> <date_de_fin>
```

Exemple:

```bash
./cli export:transitions 1 2014-10-01 2014-11-30 > /tmp/my_custom_export.csv
```

### Export des données des résumés quotidiens en CSV

Les données exportées seront affichées sur la sortie standard:

```bash
./cli export:daily-project-column-stats <id_projet_id> <date_debut> <date_de_fin>
```

Exemple:

```bash
./cli export:daily-project-column-stats 1 2014-10-01 2014-11-30 > /tmp/my_custom_export.csv
```

### Envoi de notification pour les tâches en retard

Les messages électroniques seront envoyés à tous les utilisateurs ayant activé les notifications.

```bash
./cli notification:overdue-tasks
```

Paramètres facultatifs:

- `--show`: affiche les notifications envoyées
- `--group`: Regroupe toutes les tâches en retard d'un utilisateur (de tous les projets) dans un seul message électronique
- `--manager`: Envoie toutes les tâches en retard au(x) gestionnaire(s) du projet dans un seul message électronique
- `-p|--project id_projet|identifiant`: Envoie des notifications seulement pour le projet spécifié

Vous pouvez également afficher les tâches en retard avec l'option `--show`:

```bash
./cli notification:overdue-tasks --show
+-----+---------+------------+------------+--------------+----------+
| Id  | Title   | Due date   | Project Id | Project name | Assignee |
+-----+---------+------------+------------+--------------+----------+
| 201 | Test    | 2014-10-26 | 1          | Project #0   | admin    |
| 202 | My task | 2014-10-28 | 1          | Project #0   |          |
+-----+---------+------------+------------+--------------+----------+
```

Example pour filtrer par projet:

```bash
./cli notification:overdue-tasks --project 123
```

Ou si vous avez défini un identifant de projet:

```bash
./cli notification:overdue-tasks --project MON_PROJET
```

### Exécutez les calculs des statistiques quotidiennes des projets

Cette commande calcule les statistiques de chaque projet:

```bash
./cli projects:daily-stats
Run calculation for Project #0
Run calculation for Project #1
Run calculation for Project #10
```

### Déclencheur pour les tâches

Cette commande envoi un "daily cronjob event" à toutes les tâche en cours de chacun des projets.

```bash
./cli trigger:tasks
Trigger task event: project_id=2, nb_tasks=1
```

### Réinitialiser le mot de passe utilisateur

```bash
./cli user:reset-password mon_utilisateur
```

Il vous sera demandé un mot de passe et une confirmation. Les caractères ne sont pas affichés à l'écran.

### Supprimer l'authentification à deux facteurs pour un utilisateur

```bash
./cli user:reset-2fa mon_utlisateur
```

### Installer un greffon

```bash
./cli plugin:install https://github.com/kanboard/plugin-github-auth/releases/download/v1.0.1/GithubAuth-1.0.1.zip
```

Note: Les fichiers installé ont les mêmes permissions que celles de l'utilisateur actuel

### Supprimer un greffon

```bash
./cli plugin:uninstall Budget
```

### Mettre à jour tous les greffons

```bash
./cli plugin:upgrade
* Updating plugin: Budget Planning
* Plugin up to date: Github Authentication
```

### Exécuter un worker en tâche de fond

```bash
./cli worker
```

### Exécuter un job individuel (principalement à des fins de débogage)

```bash
echo 'RAW_JOB_DATA' | ./cli job
```

### Exécuter des migrations de la base de données

Si le paramètre `DB_RUN_MIGRATIONS` est défini à `false`, vous devrez exécuter manuellement les migrations de la base de données:

```bash
./cli db:migrate
```

### Contrôler les versions du schéma de la base de données

```bash
./cli db:version
Current version: 95
Last version: 96
```
