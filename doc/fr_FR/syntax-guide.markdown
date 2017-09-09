Guide de syntaxe
============

Kanboard utilise la [syntaxe Markdown](http://en.wikipedia.org/wiki/Markdown) pour les commentaires ou les descriptions des tâches.
En voici certains exemples:

Gras et italique
----------------

- Texte gras: utilisez 2 astérisques ou 2 souslignés
- Texte italique: utilisez 1 astérisque ou 1 sousligné

### Source
```
Ce **mot** est très __important__.

Et ici, un mot *en italique* avec un _sousligné_.
```

### Rendu

Ce **mot** est très __important__.

Et ici, un mot *en italique* avec un _sousligné_.

Listes non ordonnées
---------------

Les listes non ordonnées peuvent utiliser des astérisques, des moins ou des plus.

### Source

```
- Elément 1
- Elément 2
- Elément 3

ou

* Elément 1
* Elément 2
* Elément 3
```

### Rendu

- Elément 1
- Elément 2
- Elément 3

Listes ordonnées
-------------

Les listes ordonnées sont préfixées par un nombre comme pr exemple:

### Source

```
1. Faire ça en premier
2. Faire ceci
3. Et ça
```

### Rendu

1. Faire ça en premier
2. Faire ceci
3. Et ça

Liens
-----

### Source

```
[Mon titre de lien](https://kanboard.net/)

<https://kanboard.net>

```

### Rendu

[Mon titre de lien](https://kanboard.net/)

<https://kanboard.net>

Code source 
-----------

### Code dans le texte

Utilisez une apostrophe inversée simple.

```
Exécuter cette commande: `tail -f /var/log/messages`.
```

### Rendu

Exécuter cette commande: `tail -f /var/log/messages`.

### Blocs de code

Utilisez 3 apostrophes inversées simples suivis éventuellement du nom d'un langage.

<pre>
<code class="language-markdown">```php
&lt;?php

phpinfo();

?&gt;
```
</code>
</pre>

### Rendu

```
<?php

phpinfo();

?>
```

Titres
------

### Source

```
# Titre niveau 1

## Titre niveau 2

### Titre niveau 3
```
