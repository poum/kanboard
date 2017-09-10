Performances de Kanboard
=====================

Selon votre configuration, certaines fonctionnalités peuvent ralentir l'utilisation de Kanboard.
Par défaut, toutes les opérations sont synchrones et exécutées dans le même processus que la requête HTTP.
Ceci est une limitation de PHP.
Cependant, il est possible d'améliorer ça.

Selon les greffons que vous installez, la communication avec des services externes peuvent prendre des centaines de millisecondes voir des secondes.
Pour éviter le blocage du processus principal, il est possible de déléguer ces opérations à un ensemble de [workers en tâche de fond](worker.markdown).
Cette configuration nécessite que vous installiez des logiciels supplémentaires à votre infrastructure.

Comment détecter les goulets d'étranglement ?
-----------------------------

- Activer le mode de débogage
- Surveiller le fichier log
- Faire quelque chose dans Kanboard (glisser déposer une tâche par exemple)
- Toutes les opérations sont loguées avec leur temps d'exécution (requêtes HTTP, notifications par messagerie électronique, requêtes SQL)

Améliorer la vitesse des notifications par messages électroniques
---------------------------------

En utiliser la méthode SMTP avec un serveur externe peut être très lent.

Solutions possibles:

- Utiliser des workers en tâche de fond si vous voulez continuer à utiliser SMTP
- Utiliser un relai local de messagerie avec Postfix et utilisez le transport "mail"
- Utilisez un fournisseur de messagerie qui utilise une API HTTP pour envoyer des messages électroniques (Sendgrid, Mailgun ou Postmark)

Améliorer les performances de Sqlite
---------------------------

Solutions possibles:

- Ne pas utiliser Sqlite quand vous avec beaucoup de concurrence (de nombreux utilisateurs), choisissez Postgres ou Mysql à la place
- Ne pas utiliser Sqlite sur un point de montage NFS partagé
- Ne pas utiliser Sqlite sur un disque avec un faible IOPS, il est toujours préférable d'utiliser des disques SSD locaux
