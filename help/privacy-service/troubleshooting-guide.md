---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: FAQ sur Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 48%

---


# [!DNL Privacy Service] guide de dépannage

Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface to help companies manage customer data privacy requests. With [!DNL Privacy Service], you can submit requests to access and delete private or personal customer data, facilitating automated compliance with organizational and legal privacy regulations.

Ce document fournit des réponses aux questions les plus fréquentes sur [!DNL Privacy Service]l’API, ainsi que des informations sur les erreurs fréquemment rencontrées dans l’API.

## Lors de la création de requêtes de confidentialité dans l’API, quelle est la différence entre un utilisateur et un identifiant utilisateur ? {#user-ids}

Pour effectuer une nouvelle tâche de confidentialité dans l’API, le payload JSON de la requête doit contenir un tableau `users` contenant des informations spécifiques pour chaque utilisateur concerné par la requête de confidentialité. Chaque élément du tableau `users` est un objet qui représente un utilisateur spécifique identifié par sa valeur `key`.

De même, chaque objet utilisateur (ou `key`) contient son propre tableau `userIDs`. Ce tableau indique les valeurs d’identifiant spécifiques **pour cet utilisateur**.

Consultez l’exemple de tableau `users` suivant :

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

Le tableau contient deux objets représentant des utilisateurs individuels identifiés par leurs valeurs `key` (« DavidSmith » et « user12345 »). « DavidSmith » n’a qu’un identifiant (son adresse électronique), tandis que « user12345 » en a deux (son adresse électronique et son ECID).

Pour plus d’informations sur la fourniture des informations d’identité des utilisateurs, consultez le guide sur les [données d’identité pour les demandes d’accès à des informations personnelles](identity-data.md).


## Can I use [!DNL Privacy Service] to clean up data that was accidentally sent to [!DNL Platform]?

Adobe does not support using [!DNL Privacy Service] for clearing out data that was accidentally submitted to a product. [!DNL Privacy Service] est conçu pour vous aider à remplir vos obligations en matière de requêtes d’accès ou de suppression des titulaires de données (ou consommateurs). Ces requêtes sont sensibles au facteur temps et sont effectuées en fonction des lois de confidentialité applicables. Submission of requests which are not data-subject/consumer access or delete requests impacts all [!DNL Privacy Service] customers and the ability for [!DNL Privacy Service] to support the appropriate legal timelines.

Veuillez contacter votre gestionnaire de compte (CDM) pour coordonner vos efforts et fournir un niveau de service adéquat en matière de suppression des données personnelles identifiables (PII) ou des problèmes relatifs aux données.

## Comment puis-je obtenir des informations sur l’état d’une requête ou d’une tâche de confidentialité ?

You can retrieve details about a particular job by using the [!DNL Privacy Service] API or user interface.

### Utilisation de l’API

To retrieve the status of a particular job using the [!DNL Privacy Service] API, make a request to the root (`GET /`) endpoint, using the job&#39;s ID in the request path. Pour plus d’informations, consultez la section relative à la [vérification de l’état d’une tâche](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide de développement de [!DNL Privacy Service]

### Utilisation de l’interface utilisateur

Toutes les requêtes de tâche actives sont répertoriées dans le widget **[!UICONTROL Requêtes de tâche]** accessible depuis le tableau de bord de l’interface utilisateur de [!DNL Privacy Service] L’état de chaque requête de tâche est affiché sous la colonne **[!UICONTROL État]**. Pour plus d’informations sur l’affichage des requêtes de tâche dans l’interface utilisateur, consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md).

## Comment télécharger les résultats de tâches de confidentialité terminées ?

The [!DNL Privacy Service] API and user interface both provide methods for downloading the results of completed jobs in ZIP format.

### Utilisation de l’API

Envoyez une requête au point de terminaison racine (`GET /`) de l’API en indiquant l’identifiant de la tâche dont vous souhaitez télécharger les résultats dans le chemin d’accès de la requête. [!DNL Privacy Service] Si l’état de la tâche est terminé, l’API inclut un attribut `downloadURL` dans le corps de la réponse. Cet attribut contient une URL que vous pouvez coller dans la barre d’adresse de votre navigateur pour télécharger le fichier ZIP.

Pour plus d’informations, reportez-vous à la section relative à la [recherche d’une tâche par son identifiant](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide de développement de [!DNL Privacy Service]

### Utilisation de l’interface utilisateur

On the [!DNL Privacy Service] UI dashboard, find the job you want to download from the **Job Requests** widget. Cliquez sur l’identifiant de la tâche pour ouvrir la page Détails de la tâche. Ensuite, cliquez sur **Télécharger** dans le coin supérieur droit pour télécharger le fichier ZIP. Consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md) pour obtenir des instructions plus détaillées.

## Messages d’erreur courants

Le tableau ci-dessous présente quelques erreurs courantes dans [!DNL Privacy Service]le fichier, avec des descriptions pour aider à résoudre leurs problèmes respectifs.

| Message d’erreur | Description |
| --- | --- |
| ID utilisateur introuvable. | Certains des ID utilisateur fournis dans la demande sont introuvables et ont été ignorés. Assurez-vous d’utiliser les espaces de nommage et les valeurs d’ID corrects dans la charge utile de la demande. Consultez le document sur la [fourniture de données](./identity-data.md) d&#39;identité pour une explication plus détaillée. |
| Espace de nommage non valide | Un espace de nommage d&#39;identité fourni pour un ID d&#39;utilisateur n&#39;était pas valide. Consultez la section relative aux espaces de nommage [d&#39;identité](./api/appendix.md#standard-namespaces) standard dans l&#39;annexe du guide de [!DNL Privacy Service] développement pour une liste d&#39;espaces de nommage acceptés. Si vous utilisez un espace de nommage personnalisé, veillez à définir la `type` propriété de l’identifiant sur &quot;personnalisé&quot;. |
| Partiellement terminé | La tâche s&#39;est terminée correctement, mais certaines données n&#39;étaient pas applicables à la demande donnée et ont été ignorées. |
| Les données ne sont pas au format requis. | Une ou plusieurs valeurs de données pour l’application spécifiée étaient incorrectement formatées. Pour plus d’informations, consultez les détails de la tâche. |
| L&#39;organisation IMS n&#39;a pas été configurée. | Ce message se produit lorsque votre organisation IMS n’a pas été configurée pour [!DNL Privacy Service]. Contactez votre administrateur pour plus d’informations. |
| L’accès et les autorisations sont requis. | L&#39;accès et les autorisations sont requis pour l&#39;utilisation [!DNL Privacy Service]. Contactez votre administrateur pour obtenir un accès. |
| Un problème est survenu lors du transfert et de l&#39;archivage des données d&#39;accès. | Lorsque cette erreur se produit, rechargez les données d’accès et réessayez. |
| La charge de travail a été dépassée pour la limite de taux de document actuelle. | Lorsque cette erreur se produit, réduisez le taux d’envoi et réessayez. |