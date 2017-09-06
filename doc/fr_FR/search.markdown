Syntaxe de la recherche avancée
======================

Kanboard dispose d'un langage simple pour faire des recherches avancées.
Vous pouvez pour faire des recherches dans les tâches, les commentaires, les sous-tâches, les liens ainsi que dans le flux d'activité.

Exemple de requête
----------------

Cet exemple retournera tous les tâches qui me sont affectées ayant une date d'échéance fixée à demain et un titre qui contient "mon titre":

```
assigne:me due:tomorrow mon titre
```

Recherche globale
-------------

### Recherche par identifiant de tâche ou par titre

- Recherche par identifiant de tâche: '#123'
- Recherche par identifiant de tâche et par titre de tâche: `123`
- Recherche par titre de tâche: tout ce qui ne correspond pas à l'un des attributs de recherche

### Recherche par état

Attribut: **status**

- Recherche pour trouver les tâches en cours: `status:open`
- Recherche pour trouver les tâches terminées: `status:closed`

### Rercherche par personne affectée

Attribut: **assignee**

- Recherche avec le nom complet: assignee:"Adeline Poumaroux"`
- Recherche avec l'identifiant: `assignee:apoumaroux`
- Recherche sur plusieurs personnes affectées: `assignee:utilisateur1 assignee:"Jean Dupont"`
- Recherche pour les tâches sans personne affectée: `assignee:nobody`
- Recherche pour les tâches qui me sont affectées: `assignee:me`

### Recherche par créateur de tâche

Attribut: **creator**

- Tâches créées par moi: `creator:me`
- Tâches créés par John Doe: `creator:"John Doe"`
- Tâches créées par l'utilisateur ayant l'identifiant numéro 1: `creator:1`

### Recherche par la personne affectée à une sous-tâche

Attribut: **subtask:assignee**

- Exemple: `subtask:assignee:"John Doe"`

### Recherche par couleur

Attribut: **color**

- Requête pour chercher par identifiant de couleur: `color:blue`
- Requête pour chercher par nom de couleur: `color:"Deep Orange"`

### Recherche par date d'échéance

Attribut: **due**

- Recherche des dates ayant une échéance pour aujourd'hui: `due:today`
- Recherche des dates ayant une échéance pour demain: `due:tomorrow`
- Recherche des dates ayant une échéance pour hier: `due:yesterday`
- Recherche des tâches ayant une échéance fixée à une date précise: `due:2015-06-29`

La date doit respecter le format ISO 8601: ***AAAA-MM-JJ**.

Tous les formats de date pris en charge par la fonction `strtotime()` sont pris en charge, par exemple `next Thursday`, `-2 days`, `+2 months`, `tomorrow`, etc.

Opérateurs pris en charge pour les dates:

- Supérieure à: **due:>2015-06-29**
- Inférieur à: **due:<2015-06-29**
- Supérieure ou égale à: **due:>=2015-06-29**
- Inférieure ou égale à: **due:<=2015-06-29**

### Recherche par date de modification

Attribut: **modified** ou **updated**

Les formats de date sont les mêmes que ceux des dates d'échéance.

Il existe aussi un filtre pour les tâches récemment modifiées: ̀`modified:recently`.

Cette requête utilisera la même valeur que celle de la période de mise en valeur du tableau qui a été configurée dans les préférences.

### Recherche par date de création

Attribut: **created**

Fonctionne de la même façon que les requêtes de date de modification.

### Recherche par date de démarrage

Attribut: **started**

### Recherche par description

Attribut: **description** ou **desc**

Exemple: `description:"recherche de texte"`

### Recherche des tâches achevées

Attribut: **completed**

### Recherche par référence externe

La référence d'une tâche est un identifiant externe de votre tâche, par exemple un numéro de ticket issu d'un autre logiciel.

- Trouver les tâches ayant une référence: `ref:1234` ou `reference:TICKET-1234`
- Recherche avec joker: `ref:TICKET-*`

### Recherche par catégorie

Attribut: **category**

- Trouve les tâches ayant une catégorie spécifique: `category:"Demande de fonctionnalité"`
- Trouve toutes les tâches ayant ces catégories: `category:"Bug" category:"Amélioration"`
- Trouve les tâches n'ayant aucune catégorie d'affectée: `category:none`

### Recherche par projet

Attribut: **project**

- Trouve les tâches par nom de projet: `project:"Mon nom de projet"`
- Trouve les tâches par identifiant de projet: `project:23`
- Trouve les tâches de plusieurs projets: `project:"Mon projet A" project:"Mon projet B"`

### Recherche par colonnes

Attribut: **column**

- Trouve les tâches par nom de colonne: `column:"Travail en cours"`
- Trouve les tâches pour plusieurs colonnes: `column:"Backlog" column:prêt`

### Recherche par ligne

Attribut: **swimlane**

- Recherche les tâches par ligne: `swimlane:"Version 42"`
- Trouver les tâches dans plusieurs lignes: `swimlane:"Version 1.2" swimlane:"Version 1.3"`

### Recherche par lien de tâche

Attribut: **link**

- Trouve les tâches par nom de lien: `link:"is a milestone of"`
- Trouve les tâches selon plusieurs types de liens: `link:"is a milestone of" link:"relates to"`

### Recherche par commentaire

Attribut: **comment**

- Trouve les commentaires qui contiennent ce titre: `comment:"Mon message de commentaire"`

### Recherche par étiquettes

Attribut: **tag**

- Exemple: `tag:"Mon étiquette"`

Recherche dans le flux d'activité
----------------------

### Recherche des événements par titre de tâche

Attribut: **title** ou aucun (valeur par défaut)

- Exemple: `title:"Ma tâche"`
- Recherche par identifiant de tâche: `#123`

### Recherche d'événements par état de tâche

Attribut: **status**

### Rechercher par créateur d'événement

Attribut: **creator**

### Recherche par date de création d'événement

Attribut: **created**

### Recherche d'événements par projet

Attribut: **project**
