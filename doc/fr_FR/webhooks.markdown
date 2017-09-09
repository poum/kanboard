Webhooks
========

Webhooks sont très utiles pour réaliser des actions avec des applications externes.

- les webhooks peuvent être utilisés pour créer une tâche en appelant une simple URL (vous pouvez également faire ceci en utilisant l'API)
- une URL externe peut être appelée automatiquement quand un événement se produit dans Kanboard (création d'une tâche, mise à jour d'un commentaire, etc.)

Comment écrire un récepteur de web hook ?
---------------------------------

Tous les événements internes de Kanboard peuvent être envoyés à une URL externe.

- L'URL du web hook doit être définie dans **Préférences > Webhooks > URL des Webhook**.
- Quand un événement est déclenché, Kanboard appelle automatiquement l'URL prédéfinie
- Les données sont encodées au format JSON et envoyées via une requête HTTP POST
- le jeton du web hook est également envoyé sous forme d'un paramètre de la requête, donc vous pouvez vérifier si la requête vient bien de Kanboard.
- **Votre URL personnalisée doit répondre en moins d'1 seconde**, ces requêtes sont synchrones (une limitation de PHP) et ceci peut ralentir l'interface utilisateur si votre script est trop lent !

### Liste des événements pris en charge

- comment.create
- comment.update
- comment.delete
- file.create
- task.move.project
- task.move.column
- task.move.position
- task.move.swimlane
- task.update
- task.create
- task.close
- task.open
- task.assignee_change
- subtask.update
- subtask.create
- subtask.delete
- task_internal_link.create_update
- task_internal_link.delete

### Exemple de requête HTTP

```
POST https://votre_url_de_webhook/?token=JETON_WEBHOOK_ICI
User-Agent: Kanboard Webhook
Content-Type: application/json
Connection: close

{
    "event_name": "task.move.column",
    "event_data": {
        "task_id": "4",
        "task": {
            "id": "4",
            "reference": "",
            "title": "Ma tâche",
            "description": "",
            "date_creation": "1469314356",
            "date_completed": null,
            "date_modification": "1469315422",
            "date_due": "1469491200",
            "date_started": "0",
            "time_estimated": "0",
            "time_spent": "0",
            "color_id": "green",
            "project_id": "1",
            "column_id": "1",
            "owner_id": "1",
            "creator_id": "1",
            "position": "1",
            "is_active": "1",
            "score": "0",
            "category_id": "0",
            "priority": "0",
            "swimlane_id": "0",
            "date_moved": "1469315422",
            "recurrence_status": "0",
            "recurrence_trigger": "0",
            "recurrence_factor": "0",
            "recurrence_timeframe": "0",
            "recurrence_basedate": "0",
            "recurrence_parent": null,
            "recurrence_child": null,
            "category_name": null,
            "swimlane_name": null,
            "project_name": "Projet par défaut",
            "default_swimlane": "Ligne par défaut",
            "column_title": "Backlog",
            "assignee_username": "admin",
            "assignee_name": null,
            "creator_username": "admin",
            "creator_name": null
        },
        "changes": {
            "src_column_id": "2",
            "dst_column_id": "1",
            "date_moved": "1469315398"
        },
        "project_id": "1",
        "position": 1,
        "column_id": "1",
        "swimlane_id": "0",
        "src_column_id": "2",
        "dst_column_id": "1",
        "date_moved": "1469315398",
        "recurrence_status": "0",
        "recurrence_trigger": "0"
    }
}
```
Toutes les données utiles d'un événement possèdent le format suivant:

```json
{
  "event_name": "model.event_name",
  "event_data": {
    "clef1": "valeur1",
    "clef2": "valeur2",
    ...
  }
}
```

Les valeurs `event_data` ne sont pas forcément normalisées d'un événement à l'autre.

### Exemples de données utiles pour un événement

Création d'une tâche:

```json
{
    "event_name": "task.create",
    "event_data": {
        "task_id": 5,
        "task": {
            "id": "5",
            "reference": "",
            "title": "Ma nouvelle tâche",
            "description": "",
            "date_creation": "1469315481",
            "date_completed": null,
            "date_modification": "1469315481",
            "date_due": "0",
            "date_started": "0",
            "time_estimated": "0",
            "time_spent": "0",
            "color_id": "orange",
            "project_id": "1",
            "column_id": "2",
            "owner_id": "1",
            "creator_id": "1",
            "position": "1",
            "is_active": "1",
            "score": "3",
            "category_id": "0",
            "priority": "2",
            "swimlane_id": "0",
            "date_moved": "1469315481",
            "recurrence_status": "0",
            "recurrence_trigger": "0",
            "recurrence_factor": "0",
            "recurrence_timeframe": "0",
            "recurrence_basedate": "0",
            "recurrence_parent": null,
            "recurrence_child": null,
            "category_name": null,
            "swimlane_name": null,
            "project_name": "Projet de démonstration",
            "default_swimlane": "Ligne par défaut",
            "column_title": "Prêt",
            "assignee_username": "admin",
            "assignee_name": null,
            "creator_username": "admin",
            "creator_name": null
        }
    }
}
```

Modification d'une tâche:

```json
{
    "event_name": "task.update",
    "event_data": {
        "task_id": "5",
        "task": {
            "id": "5",
            "reference": "",
            "title": "Ma nouvelle tâche",
            "description": "Nouvelle description",
            "date_creation": "1469315481",
            "date_completed": null,
            "date_modification": "1469315531",
            "date_due": "1469836800",
            "date_started": "0",
            "time_estimated": "0",
            "time_spent": "0",
            "color_id": "purple",
            "project_id": "1",
            "column_id": "2",
            "owner_id": "1",
            "creator_id": "1",
            "position": "1",
            "is_active": "1",
            "score": "3",
            "category_id": "0",
            "priority": "2",
            "swimlane_id": "0",
            "date_moved": "1469315481",
            "recurrence_status": "0",
            "recurrence_trigger": "0",
            "recurrence_factor": "0",
            "recurrence_timeframe": "0",
            "recurrence_basedate": "0",
            "recurrence_parent": null,
            "recurrence_child": null,
            "category_name": null,
            "swimlane_name": null,
            "project_name": "Projet de démonstration",
            "default_swimlane": "Ligne par défaut",
            "column_title": "Prêt",
            "assignee_username": "admin",
            "assignee_name": null,
            "creator_username": "admin",
            "creator_name": null
        },
        "changes": {
            "description": "Nouvelle description",
            "color_id": "purple",
            "date_due": 1469836800
        }
    }
}
```

Les événements de mise à jour d'une tâche possèdent un champ appelé `changes` qui contient les données mises à jour.

Création d'un commentaire:

```json
{
    "event_name": "comment.create",
    "event_data": {
        "comment": {
            "id": "1",
            "task_id": "5",
            "user_id": "1",
            "date_creation": "1469315727",
            "comment": "Mon commentaire.",
            "reference": null,
            "username": "admin",
            "name": null,
            "email": null,
            "avatar_path": null
        },
        "task": {
            "id": "5",
            "reference": "",
            "title": "My new task",
            "description": "Nouvelle description",
            "date_creation": "1469315481",
            "date_completed": null,
            "date_modification": "1469315531",
            "date_due": "1469836800",
            "date_started": "0",
            "time_estimated": "0",
            "time_spent": "0",
            "color_id": "purple",
            "project_id": "1",
            "column_id": "2",
            "owner_id": "1",
            "creator_id": "1",
            "position": "1",
            "is_active": "1",
            "score": "3",
            "category_id": "0",
            "priority": "2",
            "swimlane_id": "0",
            "date_moved": "1469315481",
            "recurrence_status": "0",
            "recurrence_trigger": "0",
            "recurrence_factor": "0",
            "recurrence_timeframe": "0",
            "recurrence_basedate": "0",
            "recurrence_parent": null,
            "recurrence_child": null,
            "category_name": null,
            "swimlane_name": null,
            "project_name": "Projet de démonstration",
            "default_swimlane": "Ligne par défaut",
            "column_title": "Prêt",
            "assignee_username": "admin",
            "assignee_name": null,
            "creator_username": "admin",
            "creator_name": null
        }
    }
}
```

Création d'une sous-tâche:

```json
{
    "event_name": "subtask.create",
    "event_data": {
        "subtask": {
            "id": "1",
            "title": "Ma sous-tâche",
            "status": "0",
            "time_estimated": "0",
            "time_spent": "0",
            "task_id": "5",
            "user_id": "1",
            "position": "1",
            "username": "admin",
            "name": null,
            "timer_start_date": 0,
            "status_name": "Todo",
            "is_timer_started": false
        },
        "task": {
            "id": "5",
            "reference": "",
            "title": "Ma nouvelle tâche",
            "description": "Nouvelle description",
            "date_creation": "1469315481",
            "date_completed": null,
            "date_modification": "1469315531",
            "date_due": "1469836800",
            "date_started": "0",
            "time_estimated": "0",
            "time_spent": "0",
            "color_id": "purple",
            "project_id": "1",
            "column_id": "2",
            "owner_id": "1",
            "creator_id": "1",
            "position": "1",
            "is_active": "1",
            "score": "3",
            "category_id": "0",
            "priority": "2",
            "swimlane_id": "0",
            "date_moved": "1469315481",
            "recurrence_status": "0",
            "recurrence_trigger": "0",
            "recurrence_factor": "0",
            "recurrence_timeframe": "0",
            "recurrence_basedate": "0",
            "recurrence_parent": null,
            "recurrence_child": null,
            "category_name": null,
            "swimlane_name": null,
            "project_name": "Projet de démonstration",
            "default_swimlane": "Ligne par défaut",
            "column_title": "Prêt",
            "assignee_username": "admin",
            "assignee_name": null,
            "creator_username": "admin",
            "creator_name": null
        }
    }
}
```

Envoi de fichier:

```json
{
    "event_name": "task.file.create",
    "event_data": {
        "file": {
            "id": "1",
            "name": "kanboard-latest.zip",
            "path": "tasks/5/6f32893e467e76671965b1ec58c06a2440823752",
            "is_image": "0",
            "task_id": "5",
            "date": "1469315613",
            "user_id": "1",
            "size": "4907308"
        },
        "task": {
            "id": "5",
            "reference": "",
            "title": "Ma nouvelle tâche",
            "description": "Nouvelle description",
            "date_creation": "1469315481",
            "date_completed": null,
            "date_modification": "1469315531",
            "date_due": "1469836800",
            "date_started": "0",
            "time_estimated": "0",
            "time_spent": "0",
            "color_id": "purple",
            "project_id": "1",
            "column_id": "2",
            "owner_id": "1",
            "creator_id": "1",
            "position": "1",
            "is_active": "1",
            "score": "3",
            "category_id": "0",
            "priority": "2",
            "swimlane_id": "0",
            "date_moved": "1469315481",
            "recurrence_status": "0",
            "recurrence_trigger": "0",
            "recurrence_factor": "0",
            "recurrence_timeframe": "0",
            "recurrence_basedate": "0",
            "recurrence_parent": null,
            "recurrence_child": null,
            "category_name": null,
            "swimlane_name": null,
            "project_name": "Projet de démonstation",
            "default_swimlane": "Ligne par défaut",
            "column_title": "Prêt",
            "assignee_username": "admin",
            "assignee_name": null,
            "creator_username": "admin",
            "creator_name": null
        }
    }
}
```

Création d'un lien de tâche:

```json
{
    "event_name": "task_internal_link.create_update",
    "event_data": {
        "task_link": {
            "id": "2",
            "opposite_task_id": "5",
            "task_id": "4",
            "link_id": "3",
            "label": "is blocked by",
            "opposite_link_id": "2"
        },
        "task": {
            "id": "4",
            "reference": "",
            "title": "Ma tâche",
            "description": "",
            "date_creation": "1469314356",
            "date_completed": null,
            "date_modification": "1469315422",
            "date_due": "1469491200",
            "date_started": "0",
            "time_estimated": "0",
            "time_spent": "0",
            "color_id": "green",
            "project_id": "1",
            "column_id": "1",
            "owner_id": "1",
            "creator_id": "1",
            "position": "1",
            "is_active": "1",
            "score": "0",
            "category_id": "0",
            "priority": "0",
            "swimlane_id": "0",
            "date_moved": "1469315422",
            "recurrence_status": "0",
            "recurrence_trigger": "0",
            "recurrence_factor": "0",
            "recurrence_timeframe": "0",
            "recurrence_basedate": "0",
            "recurrence_parent": null,
            "recurrence_child": null,
            "category_name": null,
            "swimlane_name": null,
            "project_name": "Projet de démonstration",
            "default_swimlane": "Ligne par défaut",
            "column_title": "Backlog",
            "assignee_username": "admin",
            "assignee_name": null,
            "creator_username": "admin",
            "creator_name": null
        }
    }
}
```
