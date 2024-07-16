---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Guide de dépannage de Privacy Service
description: Ce document fournit des réponses aux questions fréquentes sur Privacy Service, ainsi que des informations sur les erreurs courantes rencontrées dans l’API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 89%

---

# Guide de dépannage de [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour aider les sociétés à gérer les requêtes de données relatives à la confidentialité des clients. Avec [!DNL Privacy Service], vous pouvez envoyer des requêtes d’accès et de suppression de données clients personnelles ou privées, ce qui facilite l’automatisation de la conformité aux réglementations de confidentialité légales et au sein de l’organisation.

Ce document répond aux questions les plus fréquemment posées sur [!DNL Privacy Service], ainsi que des informations sur les erreurs courantes rencontrées dans l’API.

## Lors de la création de requêtes de confidentialité dans l’API, quelle est la différence entre un utilisateur et un identifiant utilisateur ?  {#user-ids}

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

Le tableau contient deux objets représentant des utilisateurs individuels identifiés par leurs valeurs `key` (« DavidSmith » et « user12345 »). « DavidSmith » n’a qu’un identifiant (son adresse e-mail), tandis que « user12345 » en a deux (son adresse e-mail et son ECID).

Pour plus d’informations sur la fourniture des informations d’identité des utilisateurs, consultez le guide sur les [données d’identité pour les demandes d’accès à des informations personnelles](identity-data.md).


## Puis-je utiliser [!DNL Privacy Service] pour nettoyer les données envoyées accidentellement à [!DNL Platform] ?

Adobe n’est pas compatible avec l’utilisation de [!DNL Privacy Service] comme solution pour effacer les données envoyées accidentellement à un produit. [!DNL Privacy Service] est conçu pour vous aider à remplir vos obligations en matière de requêtes d’accès ou de suppression des titulaires de données (ou consommateurs). Toute autre utilisation de Privacy Service pour le nettoyage ou la maintenance des données n’est ni prise en charge ni autorisée.

Les requêtes d’accès à des informations personnelles sont sensibles au facteur temps et sont effectuées en fonction des lois de confidentialité applicables. L’envoi de requêtes autres que les requêtes relatives à l’accès ou à la suppression de titulaires de données ou de clientes et clients a des répercussions sur les clientes et clients de [!DNL Privacy Service] et sur la capacité de [!DNL Privacy Service] à respecter les délais légaux appropriés. Une limite de chargement quotidienne stricte est maintenant en place pour prévenir les abus du service.

Veuillez contacter votre équipe Adobe en charge des comptes pour coordonner vos efforts et fournir un niveau de service adéquat en matière de suppression des données personnelles identifiables (PII) ou des problèmes relatifs aux données.

## Comment puis-je obtenir des informations sur le statut d’une requête ou d’une tâche de confidentialité ?

Vous pouvez obtenir des détails sur une tâche spécifique à l’aide de l’API ou de l’interface utilisateur [!DNL Privacy Service].

### Utilisation de l’API

Pour obtenir le statut d’une tâche spécifique à l’aide de l’API [!DNL Privacy Service], envoyez une requête au point d’entrée racine (`GET /`) en indiquant l’identifiant de la tâche dans le chemin d’accès de la requête. Pour plus d’informations, consultez la section relative à la [vérification du statut d’une tâche](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide de développement de l’API [!DNL Privacy Service].

### Utilisation de l’interface utilisateur

Toutes les requêtes de tâche actives sont répertoriées dans le widget **[!UICONTROL Requêtes de tâche]** accessible depuis le tableau de bord de l’interface utilisateur de [!DNL Privacy Service] L’état de chaque requête de tâche est affiché sous la colonne **[!UICONTROL État]**. Pour plus d’informations sur l’affichage des requêtes de tâche dans l’interface utilisateur, consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md).

## Comment télécharger les résultats de tâches de confidentialité terminées ?

L’API et l’interface utilisateur [!DNL Privacy Service] fournissent toutes deux des méthodes pour télécharger au format ZIP les résultats des tâches terminées.

### Utilisation de l’API

Envoyez une requête au point d’entrée racine (`GET /`) de l’API [!DNL Privacy Service] en indiquant l’identifiant de la tâche dont vous souhaitez télécharger les résultats dans le chemin d’accès de la requête. Si l’état de la tâche est terminé, l’API inclut un attribut `downloadURL` dans le corps de la réponse. Cet attribut contient une URL que vous pouvez coller dans la barre d’adresse de votre navigateur pour télécharger le fichier ZIP.

Pour plus d’informations, reportez-vous à la section relative à la [recherche d’une tâche par son identifiant](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide de l’API [!DNL Privacy Service].

### Utilisation de l’interface utilisateur

Dans le tableau de bord de l’interface utilisateur de [!DNL Privacy Service], recherchez la tâche à télécharger dans le widget **Requêtes de tâche**. Sélectionnez l’identifiant de la tâche pour ouvrir la page Détails de la tâche. Ensuite, sélectionnez **Télécharger** dans le coin supérieur droit pour télécharger le fichier ZIP. Consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md) pour obtenir des instructions plus détaillées.

## Messages d’erreurs courantes {#common-error-messages}

Le tableau suivant présente quelques erreurs courantes dans [!DNL Privacy Service], avec des descriptions pour aider à résoudre leurs problèmes respectifs.

| Message d’erreur | Description |
| --- | --- |
| Les ID d’utilisateur sont introuvables. | Certains des ID d’utilisateur fournis dans la requête sont introuvables et ont été ignorés. Assurez-vous que vous utilisez les valeurs d’identifiant et d’espace de noms correctes dans la payload de requête. Consultez le document [Fournir des données d’identité](./identity-data.md) pour une explication plus détaillée. |
| Espace de noms non valide | Un espace de noms d’identité fourni pour un ID d’utilisateur n’était pas valide. Voir la section [Espaces de noms d’identité standard](./api/appendix.md#standard-namespaces) dans l’annexe du guide de l’API [!DNL Privacy Service] pour obtenir une liste des espaces de noms acceptés. Si vous utilisez un espace de noms personnalisé, veillez à définir la propriété `type` des identifiants sur « personnalisés». |
| Tâche en partie terminée | La tâche s’est terminée avec succès, mais certaines données n’étaient pas applicables pour la requête donnée et ont été ignorées. |
| Les données ne sont pas au format requis. | Une ou plusieurs valeurs de données pour l’application spécifiée n’étaient pas au format requis. Pour plus d’informations, consultez les détails de la tâche. |
| L’organisation IMS n’a pas été configurée. | Ce message se produit lorsque votre organisation n’a pas été configurée pour [!DNL Privacy Service]. Pour plus d’informations, contactez votre administrateur. |
| Des accès et des autorisations sont requis. | Des accès et des autorisations sont requis pour utiliser [!DNL Privacy Service]. Contactez votre administrateur pour obtenir un accès. |
| Un problème est survenu lors du chargement et de l’archivage des données d’accès. | Lorsque cette erreur se produit, rechargez les données d’accès, puis réessayez. |
| Dépassement de la charge de travail pour la limite de taux de documents actuelle. | Lorsque cette erreur se produit, réduisez le taux d’envoi, puis réessayez. |
| Trop de requêtes<br> (erreurs HTTP 429) | Si vos modèles d’envoi dépassent la limite surveillée des tâches de sujet de données autorisées, vous recevrez une erreur HTTP 429 en réponse au trafic continu de votre entreprise. Privacy Service est destiné au traitement des demandes d’accès à des informations personnelles des titulaires de données. Il ne doit pas être utilisé pour le nettoyage des données. Si vous recevez des erreurs HTTP 429, des limites de limitation et de requête sont mises en oeuvre pour protéger l’Adobe des abus qui pourraient mettre en danger le travail de conformité légitime.<br>Des méthodes alternatives pour minimiser vos données sont fournies en [définissant les plannings d’expiration de jeu de données](../hygiene/ui/dataset-expiration.md) et en utilisant la [fonction de suppression d’enregistrement](../hygiene/ui/record-delete.md). Pour plus d’informations sur l’application de ces fonctionnalités, consultez leur documentation respective. |
