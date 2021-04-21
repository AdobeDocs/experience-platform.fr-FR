---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Guide de dépannage des Privacy Service
topic-legacy: troubleshooting
description: Ce document fournit des réponses aux questions fréquentes sur le Privacy Service, ainsi que des informations sur les erreurs courantes de l’API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 44%

---

# [!DNL Privacy Service] guide de dépannage

Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour aider les sociétés à gérer les demandes de confidentialité des données client. Avec [!DNL Privacy Service], vous pouvez envoyer des demandes d&#39;accès et de suppression de données personnelles ou privées sur vos clients, ce qui facilite la conformité automatisée aux réglementations en matière de confidentialité organisationnelle et juridique.

Ce document fournit des réponses aux questions fréquentes sur [!DNL Privacy Service], ainsi que des informations sur les erreurs courantes de l&#39;API.

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


## Puis-je utiliser [!DNL Privacy Service] pour nettoyer les données qui ont été envoyées accidentellement à [!DNL Platform] ?

Adobe ne prend pas en charge l&#39;utilisation de [!DNL Privacy Service] pour effacer les données qui ont été envoyées accidentellement à un produit. [!DNL Privacy Service] est conçu pour vous aider à remplir vos obligations en matière de requêtes d’accès ou de suppression des titulaires de données (ou consommateurs). Ces requêtes sont sensibles au facteur temps et sont effectuées en fonction des lois de confidentialité applicables. La présentation de demandes qui ne sont pas des demandes d&#39;accès aux données/aux consommateurs ou de suppression a un impact sur tous les clients [!DNL Privacy Service] et sur la capacité de [!DNL Privacy Service] de prendre en charge les délais légaux appropriés.

Veuillez contacter votre gestionnaire de compte (CDM) pour coordonner vos efforts et fournir un niveau de service adéquat en matière de suppression des données personnelles identifiables (PII) ou des problèmes relatifs aux données.

## Comment puis-je obtenir des informations sur l’état d’une requête ou d’une tâche de confidentialité ?

Vous pouvez récupérer des détails sur une tâche particulière à l’aide de l’API [!DNL Privacy Service] ou de l’interface utilisateur.

### Utilisation de l’API

Pour récupérer l’état d’une tâche particulière à l’aide de l’API [!DNL Privacy Service], envoyez une requête au point de terminaison racine (`GET /`) en utilisant l’ID de la tâche dans le chemin de requête. Pour plus d’informations, consultez la section relative à la [vérification de l’état d’une tâche](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide de développement de [!DNL Privacy Service]

### Utilisation de l’interface utilisateur

Toutes les requêtes de tâche actives sont répertoriées dans le widget **[!UICONTROL Requêtes de tâche]** accessible depuis le tableau de bord de l’interface utilisateur de [!DNL Privacy Service] L’état de chaque requête de tâche est affiché sous la colonne **[!UICONTROL État]**. Pour plus d’informations sur l’affichage des requêtes de tâche dans l’interface utilisateur, consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md).

## Comment télécharger les résultats de tâches de confidentialité terminées ?

L&#39;API [!DNL Privacy Service] et l&#39;interface utilisateur fournissent toutes deux des méthodes pour télécharger les résultats des tâches terminées au format ZIP.

### Utilisation de l’API

Envoyez une requête au point de terminaison racine (`GET /`) de l’API en indiquant l’identifiant de la tâche dont vous souhaitez télécharger les résultats dans le chemin d’accès de la requête. [!DNL Privacy Service] Si l’état de la tâche est terminé, l’API inclut un attribut `downloadURL` dans le corps de la réponse. Cet attribut contient une URL que vous pouvez coller dans la barre d’adresse de votre navigateur pour télécharger le fichier ZIP.

Pour plus d’informations, reportez-vous à la section relative à la [recherche d’une tâche par son identifiant](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide de développement de [!DNL Privacy Service]

### Utilisation de l’interface utilisateur

Sur le tableau de bord d&#39;interface utilisateur [!DNL Privacy Service], recherchez la tâche que vous souhaitez télécharger à partir du widget **Demandes de tâche**. Sélectionnez l’ID de la tâche pour ouvrir la page Détails de la tâche. À partir de là, sélectionnez **Télécharger** dans le coin supérieur droit pour télécharger le fichier ZIP. Consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md) pour obtenir des instructions plus détaillées.

## Messages d’erreur courants

Le tableau suivant présente quelques erreurs courantes dans [!DNL Privacy Service], avec des descriptions pour aider à résoudre leurs problèmes respectifs.

| Message d’erreur | Description |
| --- | --- |
| ID utilisateur introuvable. | Certains des ID utilisateur fournis dans la demande sont introuvables et ont été ignorés. Assurez-vous d’utiliser les espaces de nommage et les valeurs d’ID corrects dans la charge utile de la demande. Voir le document sur [la fourniture de données d&#39;identité](./identity-data.md) pour une explication plus détaillée. |
| Espace de nommage non valide | Un espace de nommage d&#39;identité fourni pour un ID d&#39;utilisateur n&#39;était pas valide. Voir la section [espaces de nommage d&#39;identité standard](./api/appendix.md#standard-namespaces) dans l&#39;annexe du guide du développeur [!DNL Privacy Service] pour une liste d&#39;espaces de nommage acceptés. Si vous utilisez un espace de nommage personnalisé, veillez à définir la propriété `type` de l’identifiant sur &quot;personnalisé&quot;. |
| Partiellement terminé | La tâche s&#39;est terminée correctement, mais certaines données n&#39;étaient pas applicables à la demande donnée et ont été ignorées. |
| Les données ne sont pas au format requis. | Une ou plusieurs valeurs de données pour l’application spécifiée étaient incorrectement formatées. Pour plus d’informations, consultez les détails de la tâche. |
| L&#39;organisation IMS n&#39;a pas été configurée. | Ce message se produit lorsque votre organisation IMS n&#39;a pas été configurée pour [!DNL Privacy Service]. Contactez votre administrateur pour plus d’informations. |
| L’accès et les autorisations sont requis. | L&#39;accès et les autorisations sont nécessaires pour utiliser [!DNL Privacy Service]. Contactez votre administrateur pour obtenir un accès. |
| Un problème est survenu lors du transfert et de l&#39;archivage des données d&#39;accès. | Lorsque cette erreur se produit, rechargez les données d’accès et réessayez. |
| La charge de travail a été dépassée pour la limite de taux de document actuelle. | Lorsque cette erreur se produit, réduisez le taux d’envoi et réessayez. |
