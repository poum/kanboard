Comment exécuter Kanboard sur Cloudron
================================

[Cloudron](https://cloudron.io) est un serveur privé  sur lequel vous pouvez installer des applications web
telles que Kanboard. Vous pouvez installer Kanboard dans un domaine personnalisé et chaque 
installaion est sauvegardée et maintenue à jour automatiquement avec les livraisons de Kanboard.

[![Installation](https://cloudron.io/img/button.svg)](https://cloudron.io/button.html?app=net.kanboard.cloudronapp)

Comptes
--------

L'application s'intègre étroitement avec la gestion des utilisateurs de Cloudron (via LDAP). Seuls
les utilisateurs Cloudron peuvent accéder à Kanboard. De plus, tout administrateur Cloudron devient
automatiquement un administrateur Kanboard.

Installer des greffons
------------------

Les greffons peuvent être installés et configurés en utilisant l'outil [Cloudron CLI](https://git.cloudron.io/cloudron/cloudron-cli).
Voir la [description de l'application](https://cloudron.io/appstore.html?app=net.kanboard.cloudronapp) pour
plus d'information.

Code source de l'application
----------------------

Le code source de l'application Cloudron est [ici](https://git.cloudron.io/cloudron/kanboard-app).

