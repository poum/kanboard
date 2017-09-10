Synchroniser vos calendriers
======================

Kanboard prend en charge les flux iCal pour les projets et les utilisateurs.
Cette fonctionnalité vous permet d'importer les tâches Kanboard dans presque tous les programmes de calendrier (par exemple Microsoft Outlook, Mozilla Thunderbird et Google Calendar).

Les abonnements aux calendriers n'ont qu'un accès en **lecture seule**, vous ne pouvez pas créer de tâches depuis un logiciel de calendrier externe.
L'export de flux de calendrier respecte le standard iCal.

Note: seules les tâches dans une fenêtre de -2 mois à +6 mois sont exportées dans le flux iCalendar.

Calendriers des projets
-----------------

- Chaque projet possède son propre calendrier
- Le lien d'abonnement est unique pour chaque projet, le lien est activé quand vous autorisez l'accès public pour votre projet; **Préférences > Accès public**.
- Ce calendrier n'affiche que les tâches pour le projet sélectionné.

User calendars
Calendrier des utilisateurs
--------------

- Chaque utilisateur possède son propre calendrier.
- Le lien d'abonnement est unique pour chaque utilisateur, le lien est activé quand vous autorisez l'accès public pour votre utilisateur: **Préférences utilisateur > Accès public**.

Ajouter votre calendrier Kanboard à Apple Calendar
-----------------------------------------------

- Ouvrir Calendrier
- Sélectionner **Fichier > Nouvel abonnement à un calendrier**
- Copier coller l'URL du flux iCal depuis Kanboard

![Ajouter un abonnement iCal](screenshots/apple-calendar-add-subscription.png)

- Vous pouvez choisir de synchroniser le calendrier avec iCloud pour le rendre accessible sur tous vos appareils
- N'oubliez pas de choisir la fréquence de rafraîchissement

![Modifier l'abonnement iCal](screenshots/apple-calendar-edit-subscription.png)

Ajouter votre calendrier Kanboard à Microsoft Outlook
--------------------------------------------------

![Outlook Ajouter un calendrier internet](screenshots/outlook-add-subscription.png)

- Ouvrir Outlook
- Sélectionner **Ouvrir calendrier > Depuis Internet**
- Copier coller l'URL du flux iCal depuis Kanboard

![Outlook Modifier le calendrier Internet](screenshots/outlook-edit-subscription.png)

Ajouter votre calendrier Kanboard à Mozilla Thunderbird
----------------------------------------------------

- Installer l'extension **Lightning** pour ajouter la gestion des calendriers à Thunderbird
- Clic sur **Fichier > Nouveau calendrier**
- Dans la boîte de dialogue, choisir **Sur le réseau**

![Thunderbird Etape 1](screenshots/thunderbird-new-calendar-step1.png)

- Choisir le format iCalendar
- Copier coller l'URL du flux iCal depuis Kanboard

![Thunderbird Etape 2](screenshots/thunderbird-new-calendar-step2.png)

- Choisir les couleurs et les autres réglages puis finalement enregistrer

Ajouter votre calendrier Kanboard à Google Calendar
------------------------------------------------

- Cliquer sur la flèche vers le bas à côté de **Autres calendriers**.
- Choisir **Ajouter par URL** dans le menu.
- Copier coller l'URL du flux iCal depuis Kanboard

![Google Calendar](screenshots/google-calendar-add-subscription.png)

Votre calendrier Kanboard peut également être disponible depuis tous vos appareil Android si vous activez la synchronisation.

Note: Selon le support Google, les calendriers externes ne sont pas rafraîchis très souvent, [lisez la documentation](https://support.google.com/calendar/answer/37100?hl=en&ref_topic=1672445).
