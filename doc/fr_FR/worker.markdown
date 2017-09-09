Workers en tâche de fond
==================

**Cette fonctionnalité est expérimentale**.

Selon votre configuration, certains fonctionnalités peuvent ralentir l'application si elles sont exécutées dans le même processus que la requête HTTP.
Kanboard peut déléguer ces tâches à un worker en tâche de fond qui est à l'écoute des événements entrant.

Exemple de fonctionnalités qui peuvent ralentir Kanboard:

- Envoyer des messages électroniques via un serveur SMTP externe peut prendre plusieurs secondes
- Envoyer des notifications à des services externes

Cette fonctionnalité est optionnelle et nécessite l'installation d'un démon de gestion de file de travaux sur votre serveur.

### Beanstalk

[Beanstalk](http://kr.github.io/beanstalkd/) est une file de travaux simple et rapide.

- Pour installer Beanstalk, vous pouvez simplement utiliser le gestionnaire de paquets de votre distribution Linux
- Installer le [greffon Kanboard pour Beanstalk](https://kanboard.net/plugin/beanstalk)
- Démarrer le worker avec l'outil en ligne de commandes de Kanboard: `./cli worker`

### RabbitMQ

[RabbitMQ](https://www.rabbitmq.com/) est un système de messages robuste qui est plus adapté pour les infrastructures à haute disponibilité.

- Suivez la documentation officielle de RabbitMQ pour l'installation et la confiuration
- Installez le [greffon Kanboard pour RabbitMQ](https://kanboard.net/plugin/rabbitmq)
- Démarrer le worker avec l'outil en ligne de commandes de Kanboard: `./cli worker`

### Notes

- Vous devez lancer le worker de Kanboard avec un superviseur de processus (systemd, upstart ou supervisord)
- Le processus doit avoir accès au répertoire data si vous enregistrez les fichiers sur le système de fichiers local ou si vous utilisez Sqlite
