Réécriture d'URL
=============

Kanboard est capable de fonctionner de la même façon avec la réécriture d'URL activée ou pas. 

- Exemple d'URL réécrite: `/board/123`
- Autrement: `?controller=board&action=show&project_id=123`

Si vous utilisez Kanboard avec Apache et avec le mode réécriture activé, de belles URLs seront utilisées automatiquement.
Dans le cas où vous obtiendriez un "404 Not Found", vous pourriez avoir besoin de configurer au moins l'une des surcharges pour votre
DocumentRoot pour que vos fichiers .htaccess fonctionnent:

```sh
<Directory /var/www/kanboard/>
	AllowOverride FileInfo Options=All,MultiViews AuthConfig
</Directory>
```

URL raccourcies 
-------------

- Aller à la tâche n°123: **/t/123**
- Accéder au tableau du projet n°2: **/b/2**
- Accéder au calendrier du projet n°5: **/c/5**
- Accéder à la vue en liste du projet n°8: -**/l/8**
- Accéder aux préférences du projet n°42: **/p/42**

Configuration
-------------

Par défaut, Kanbord va vérifier si le mode réécriture d'Apache est activé.

Pour éviter la détection automatique de la réécriture d'URL par le serveur web, vous pouvez activer cette fonctionnalité dans votre fichier de configuration:

```php
define('ENABLE_URL_REWRITE', true);
```

Quand cette constante est à `true`:

- les URL générées via les outils en ligne de commande seront également converties
- Si vous utilisez un autre serveur web qu'Apache, par exemple Nginx ou Microsoft IIS, vous devrez configurer vous-même la réécriture d'URL

Note: Kanboard retourne toujours à l'ancienne URL quand ce n'est pas configuré, cette configuration est facultative.

Exemple de configuration de Nginx
---------------------------

Dans la section `server` de votre fichier de configuration de Nginx, vous pouvez utiliser cet exemple:

```bash
index index.php;

location / {
    try_files $uri $uri/ /index.php$is_args$args;

    # Si Kanboard est dans un sous-répertoire
    # try_files $uri $uri/ /kanboard/index.php;
}

location ~ \.php$ {
    try_files $uri =404;
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    fastcgi_pass unix:/var/run/php5-fpm.sock;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    fastcgi_index index.php;
    include fastcgi_params;
}

# Interdit l'accès au répertoire data
location ~* /data {
    deny all;
    return 404;
}

# Interdit l'accès au .htaccess
location ~ /\.ht {
    deny all;
    return 404;
}
```

Dans votre `config.php` de Kanboard:

```php
define('ENABLE_URL_REWRITE', true);
```

Un autre exemple avec Kanboard dans un sous-répertoire:

```
server {
    listen 443 ssl default_server;
    listen [::]:443 ssl default_server;

    root /var/www/html;
    index index.php index.html index.htm;
    server_name _;

    location / {
        try_files $uri $uri/ =404;
    }

    location ^~ /kanboard {

        location /kanboard {
            try_files $uri $uri/ /kanboard/index.php$is_args$args;
        }

        location ~ ^/kanboard/(?:kanboard|config.php|config.default.php) {
            deny all;
        }

        location ~* /kanboard/data {
            deny all;
        }

        location ~ \.php(?:$|/) {
            fastcgi_split_path_info ^(.+\.php)(/.+)$;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_param PATH_INFO $fastcgi_path_info;
            fastcgi_param HTTPS on; # Use only if HTTPS is configured
            include fastcgi_params;
            fastcgi_pass unix:/var/run/php5-fpm.sock;
        }

        location ~ /kanboard/\.ht {
            deny all;
        }
    }
}
```

Adaptez l'exemple ci-dessus selon votre propre configuration.

Exemple de configuration de IIS
-------------------------

1. Télécharer et installer le module Rewrite pour IIS: [lien de télécharement](http://www.iis.net/learn/extensions/url-rewrite-module/using-the-url-rewrite-module)
2. Créer un web.config dans votre répertoire d'installation:

```xml
<?xml version="1.0"?>
<configuration>
    <system.webServer>
        <defaultDocument>
            <files>
                <clear />
                <add value="index.php" />
            </files>
        </defaultDocument>
        <rewrite>
            <rules>
                <rule name="Kanboard URL Rewrite" stopProcessing="true">
                    <match url="^(.*)$" ignoreCase="false" />
                    <conditions logicalGrouping="MatchAll">
                        <add input="{REQUEST_FILENAME}" matchType="IsFile" ignoreCase="false" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="index.php" appendQueryString="true" />
                </rule>
            </rules>
        </rewrite>
    </system.webServer>
</configuration>
```

Dans le `config.php` de votre Kanboard:

```php
define('ENABLE_URL_REWRITE', true);
```

Adaptez l'exemple ci-dessus selon votre propre configuration.

