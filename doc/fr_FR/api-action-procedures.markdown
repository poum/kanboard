Procédures des actions automatiques de l'API
================================

## getAvailableActions

- Objectif: **Obtenir la liste des actions automatiques disponibles**
- Paramètres: aucun
- Résultat en cas de succès: **liste des actions**
- Résultat en cas d'échec: **false**

Exemple de requête:

```json
{
    "jsonrpc": "2.0",
    "method": "getAvailableActions",
    "id": 1217735483
}
```

Exemple de réponse:

```json
{
    "jsonrpc": "2.0",
    "id": 1217735483,
    "result": {
        "\Kanboard\Action\TaskLogMoveAnotherColumn": "Add a comment logging moving the task between columns",
        "\Kanboard\Action\TaskAssignColorUser": "Assign a color to a specific user",
        "\Kanboard\Action\TaskAssignColorColumn": "Assign a color when the task is moved to a specific column",
        "\Kanboard\Action\TaskAssignCategoryColor": "Assign automatically a category based on a color",
        "\Kanboard\Action\TaskAssignColorCategory": "Assign automatically a color based on a category",
        "\Kanboard\Action\TaskAssignSpecificUser": "Assign the task to a specific user",
        "\Kanboard\Action\TaskAssignCurrentUser": "Assign the task to the person who does the action",
        "\Kanboard\Action\TaskUpdateStartDate": "Automatically update the start date",
        "\Kanboard\Action\TaskAssignUser": "Change the assignee based on an external username",
        "\Kanboard\Action\TaskAssignCategoryLabel": "Change the category based on an external label",
        "\Kanboard\Action\TaskClose": "Close a task",
        "\Kanboard\Action\CommentCreation": "Create a comment from an external provider",
        "\Kanboard\Action\TaskCreation": "Create a task from an external provider",
        "\Kanboard\Action\TaskDuplicateAnotherProject": "Duplicate the task to another project",
        "\Kanboard\Action\TaskMoveColumnAssigned": "Move the task to another column when assigned to a user",
        "\Kanboard\Action\TaskMoveColumnUnAssigned": "Move the task to another column when assignee is cleared",
        "\Kanboard\Action\TaskMoveAnotherProject": "Move the task to another project",
        "\Kanboard\Action\TaskOpen": "Open a task"
    }
}
```

## getAvailableActionEvents

- Objectif: **Obtenir la liste des événements disponibles pour les actions**
- Paramètres: aucun
- Résultat en cas de succès: **liste des événements**
- Résultat en cas d'échec: **false**

Exemple de requête:

```json
{
    "jsonrpc": "2.0",
    "method": "getAvailableActionEvents",
    "id": 2116665643
}
```

Exemple de réponse:

```json
{
    "jsonrpc": "2.0",
    "id": 2116665643,
    "result": {
        "bitbucket.webhook.commit": "Bitbucket commit received",
        "task.close": "Closing a task",
        "github.webhook.commit": "Github commit received",
        "github.webhook.issue.assignee": "Github issue assignee change",
        "github.webhook.issue.closed": "Github issue closed",
        "github.webhook.issue.commented": "Github issue comment created",
        "github.webhook.issue.label": "Github issue label change",
        "github.webhook.issue.opened": "Github issue opened",
        "github.webhook.issue.reopened": "Github issue reopened",
        "gitlab.webhook.commit": "Gitlab commit received",
        "gitlab.webhook.issue.closed": "Gitlab issue closed",
        "gitlab.webhook.issue.opened": "Gitlab issue opened",
        "task.move.column": "Move a task to another column",
        "task.open": "Open a closed task",
        "task.assignee_change": "Task assignee change",
        "task.create": "Task creation",
        "task.create_update": "Task creation or modification",
        "task.update": "Task modification"
    }
}
```

## getCompatibleActionEvents

- Objectif: **Obtenir la liste des événements compatibles avec une action**
- Paramètres:
    - **action_name** (string, required)
- Résultat en cas de succès: **liste des événements**
- Résultat en cas d'échec: **false**

Exemple de requête:

```json
{
    "jsonrpc": "2.0",
    "method": "getCompatibleActionEvents",
    "id": 899370297,
    "params": [
        "\Kanboard\Action\TaskClose"
    ]
}
```

Exemple de réponse:

```json
{
    "jsonrpc": "2.0",
    "id": 899370297,
    "result": {
        "bitbucket.webhook.commit": "Bitbucket commit received",
        "github.webhook.commit": "Github commit received",
        "github.webhook.issue.closed": "Github issue closed",
        "gitlab.webhook.commit": "Gitlab commit received",
        "gitlab.webhook.issue.closed": "Gitlab issue closed",
        "task.move.column": "Move a task to another column"
    }
}
```

## getActions

- Objectif: **Obtenir la liste des actions pour un projet**
- Paramètres:
    - **project_id** (integer, required)
- Résultat en cas de succès: **liste des propriétés des actions**
- Résultat en cas d'échec: **false**

Exemple de requête:

```json
{
    "jsonrpc": "2.0",
    "method": "getActions",
    "id": 1433237746,
    "params": [
        "1"
    ]
}
```

Exemple de réponse:

```json
{
    "jsonrpc": "2.0",
    "id": 1433237746,
    "result": [
        {
            "id" : "13",
            "project_id" : "2",
            "event_name" : "task.move.column",
            "action_name" : "\Kanboard\Action\TaskAssignSpecificUser",
            "params" : {
                "column_id" : "5",
                "user_id" : "1"
            }
        }
    ]
}
```

## createAction

- Objectif: **Créer une action**
- Paramètres:
    - **project_id** (integer, required)
    - **event_name** (string, required)
    - **action_name** (string, required)
    - **params** (key/value parameters, required)
- Résultat en cas de succès: **action_id**
- Résultat en cas d'échec: **false**

Exemple de requête:

```json
{
    "jsonrpc": "2.0",
    "method": "createAction",
    "id": 1433237746,
    "params": {
        "project_id" : "2",
        "event_name" : "task.move.column",
        "action_name" : "\Kanboard\Action\TaskAssignSpecificUser",
        "params" : {
            "column_id" : "3",
            "user_id" : "2"
        }
    }
}
```

Exemple de réponse:

```json
{
    "jsonrpc": "2.0",
    "id": 1433237746,
    "result": 14
}
```

## removeAction

- Objectif: **Supprimer une action**
- Paramètres:
    - **action_id** (integer, required)
- Résultat en cas de succès: **true**
- Résultat en cas d'échec: **false**

Exemple de requête:

```json
{
    "jsonrpc": "2.0",
    "method": "removeAction",
    "id": 1510741671,
    "params": [
        1
    ]
}
```

Exemple de réponse:

```json
{
    "jsonrpc": "2.0",
    "id": 1510741671,
    "result": true
}
```
