Programmation des jobs en tâche de fond
=========================

Pour fonctionner correctement, Kanboard nécessite qu'un job en tâche de fond s'exécute de manière quotidienne.
Habituellement sur les plates-formes, ce processus est réalisé par `cron`.

Ce job en tâche de fond est nécessaire pour ces fonctionnalités:

- Les rapports et les statistiques (calcule les statistiques quotidiennes de chaque projet)
- Envoi des notifications des tâches en retard
- Exécuter des actions automatiques connectées à l'événement "Job quotidien en tâche de fond des tâches"

Confiuration sur les plates-formes Unix et Linux
-----------------------------------------

Il existe de multiples façons de définir un cronjob sur les systèmes d'exploitation Unix/Linux, cet exemple est pour Ubuntu 14.04.
La proécdure est similaire à d'autres systèmes.

Modifiez le fichier crontab de l'utilisateur de votre serveur web:

```bash
sudo crontab -u www-data -e
```

Exemple pour exécuter le cronjob quotidien à 8 heures du matin:

```bash
0 8 * * * cd /chemin/vers/kanboard && ./cli cronjob >/dev/null 2>&1
```

Note: le processus du cronjob doit disposer des droits d'écriture à la base de données dans le cas où vous utiliseriez Sqlite.
Habituellement, exécuter le cronjob en tant que l'utilisateur du web server est suffisant.

Configuraion sur le serveur Microsoft Windows
-----------------------------------------

Avant de configurer la tâche récurrente, créez un fichier batch (*.bat ou *.cmd) qui exécute le script CLI de Kanboard.

Voici un exemple (`C:\kanboard.bat`):

```
"C:\php\php.exe" -f "C:\inetpub\wwwroot\kanboard\kanboard" cronjob
```

**Vous devez modifier le chemin de l'exécutable PHP et le chemin du script de Kanboard conformément à votre installation.**

Configurer le programmateur des tâches de Windows:

1. Aller dans "Outils d'administration"
2. Ouvrir le "Programmateur de tâches"
3. Sur la droite, choisir "Créer une tâche"
4. Choisir un nom, par exemple, vous pouvez utiliser "Kanboard"
5. Sous "Options de sécurité", choisir un utilisateur qui peut écrire dans la base de données dans le cas où vous utiliseriez Sqlite (ce peut être IIS_IUSRS selon votre configuration)
6. Créez un nouveau "Trigger", choisissez quotidien et une heure, minuit par exemple
7. Ajoutez une nouvelle action, choisissez "Démarrer un programme" et choisissez le fichier batch créé précédemment
