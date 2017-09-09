Configuration de la messaerie
===================

Réglages utilisateur
-------------

Pour recevoir des notifications par messagerie, les utiisateurs de Kanboard doivent avoir:

- les notifications activées dans leurs profils
- avoir une adresse de messagerie valide dans leurs profils
- Être membre du projet qui va déclencher les notifications

Note: l'utilisateur connecté qui exécute l'action ne recevra aucune notification, seuls les autres membres du projet en recevront.

Transmission des messages électroniques
----------------

Il y a plusieurs émetteurs de messages électroniques disponibles:

- SMTP
- Sendmail
- la fonction de messagerie native de PHP
- d'autres méthodes peuvent être fournies par des greffons externes: Postmark, Sendgrid et Mailgun

Réglages du serveur
---------------

Par défaut, Kanboard utilisera la fonction de messagerie incluse dans PHP pour envoyer les messages électroniques.
Habituellement, ceci ne requiert aucune configuration si votre serveur peut déjà envoyer des messages électroniques.

Cependant, il est possible d'utiliser d'autres méthodes, le protocole SMTP et Sendmail.

### Configuration SMTP 

Renommez le fichier `config.default.php` en `config.php` et modifiez ces valeurs:

```php
// Nous choisissons "smtp" comme émetteur des messages électroniques
define('MAIL_TRANSPORT', 'smtp');

// Nous définissons nos réglages serveur
define('MAIL_SMTP_HOSTNAME', 'mail.exemple.com');
define('MAIL_SMTP_PORT', 25);

// Paramètres d'authentification du serveur SMTP (pas obligatoire)
define('MAIL_SMTP_USERNAME', 'identifiant');
define('MAIL_SMTP_PASSWORD', 'super mot de passe');
```

Il est également possible d'utiliser une connexion sécurisée, TLS ou SSL:

```php
define('MAIL_SMTP_ENCRYPTION', 'ssl'); // Les valeurs autorisées sont "null", "ssl" ou "tls"
```

### Configuration Sendmail

Par défaut, la commande sendmail sera `/usr/sbin/sendmail -bs` mais vous pouvez la personnaliser dans votre fichier de configuration.

Exemple:

```php
// Nous choisissons "sendmail" comme émetteur des messages électroniques 
define('MAIL_TRANSPORT', 'sendmail');

// Si vous avez besoin de modifier la commande sendmail, remplacez la valeur
define('MAIL_SENDMAIL_COMMAND', '/usr/sbin/sendmail -bs');
```

### Fonction de messagerie native de PHP

Ceci est la configuration par défaut:

```php
define('MAIL_TRANSPORT', 'mail');
```

### L'adresse de messagerie de l'émetteur

Par défaut, les messages électroniques utiliseront comme adresse d'émetteur `notifications@kanboard.local`.
Il n'est pas possible de répondre à cette adresse.

Vous pouvez personnaliser cette adresse en modifiant la valeur de la constante `MAIL_FROM` dans votre fichier de configuration.

```php
define('MAIL_FROM', 'kanboard@mondomaine.tld');
```

Ceci peut être utile si la configuration de votre serveur SMTP n'accepte pas l'adresse par défaut.

### Comment afficher un lien vers la tâche dans les notifications ?

Pour faire cela, vous devez indiquer l'URL de votre installation Kanboard dans les [réglages de l'application](https://kanboard.net/documentation/application-configuration).
Par défaut, rien n'est défini, donc les liens ne seront pas affichés.

Exemples:

- http://demo.kanboard.net/
- http://monserveur/kanboard/
- http://kanboard.mondomaine.com/

N'oubliez pas le slash `/` final.

Vous avez besoin de définir ceci manuellement car Kanboard ne peut pas deviner l'URL à partir d'un script en ligne de commande et certaines personnes ont une configuration très spécifique.

Dépannage
---------------

Si aucun message électronique n'est envoyé et que vous êtes sûrs que tout est configuré correctement:

- Vérifiez votre dossier des pourriels
- Activez le mode de débogage et contrôlez le fichier de débogage `data/debug.log`, vous pourriez y voir l'erreur exacte
- Soyez sûr que votre serveur ou votre hébergeur vous permet d'envoyer des messages électroniques
- Si vous utilisez SeLinux, autorisez PHP à envoyer des messages électroniques
