---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Guide de dépannage des Privacy Service
description: Ce document fournit des réponses aux questions fréquentes sur Privacy Service, ainsi que des informations sur les erreurs courantes de l’API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 41%

---

# Guide de dépannage du [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour aider les entreprises à gérer les demandes de confidentialité des données clients. Avec [!DNL Privacy Service], vous pouvez soumettre des demandes d’accès et de suppression de données clients privées ou personnelles, ce qui facilite la conformité automatisée aux réglementations de confidentialité organisationnelles et juridiques.

Ce document répond aux questions les plus fréquemment posées sur les sujets suivants : [!DNL Privacy Service], ainsi que des informations sur les erreurs courantes de l’API.

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


## Puis-je utiliser [!DNL Privacy Service] pour nettoyer les données qui ont été accidentellement envoyées à [!DNL Platform]?

Adobe ne prend pas en charge l’utilisation de [!DNL Privacy Service] pour effacer les données qui ont été soumises accidentellement à un produit. [!DNL Privacy Service] est conçu pour vous aider à remplir vos obligations en matière de requêtes d’accès ou de suppression des titulaires de données (ou consommateurs). Ces requêtes sont sensibles au facteur temps et sont effectuées en fonction des lois de confidentialité applicables. L’envoi de requêtes qui ne sont pas des requêtes d’accès ou de suppression des titulaires de données/consommateurs impacte toutes les [!DNL Privacy Service] les clients et la possibilité pour [!DNL Privacy Service] pour prendre en charge les délais légaux appropriés.

Veuillez contacter votre gestionnaire de compte (CDM) pour coordonner vos efforts et fournir un niveau de service adéquat en matière de suppression des données personnelles identifiables (PII) ou des problèmes relatifs aux données.

## Comment puis-je obtenir des informations sur l’état d’une requête ou d’une tâche de confidentialité ?

Vous pouvez récupérer les détails d’une tâche spécifique à l’aide de la fonction [!DNL Privacy Service] API ou interface utilisateur.

### Utilisation de l’API

Pour récupérer l’état d’une tâche spécifique à l’aide de la fonction [!DNL Privacy Service] API, envoyez une requête à la racine (`GET /`), à l’aide de l’identifiant de la tâche dans le chemin d’accès de la requête. Pour plus d’informations, reportez-vous à la section sur [vérification de l’état d’une tâche](api/privacy-jobs.md#check-the-status-of-a-job) dans le [!DNL Privacy Service] Guide de l’API.

### Utiliser l’interface utilisateur

Toutes les requêtes de tâche actives sont répertoriées dans le widget **[!UICONTROL Requêtes de tâche]** accessible depuis le tableau de bord de l’interface utilisateur de [!DNL Privacy Service] L’état de chaque requête de tâche est affiché sous la colonne **[!UICONTROL État]**. Pour plus d’informations sur l’affichage des requêtes de tâche dans l’interface utilisateur, consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md).

## Comment télécharger les résultats de tâches de confidentialité terminées ?

Le [!DNL Privacy Service] L’API et l’interface utilisateur fournissent toutes deux des méthodes pour télécharger les résultats des tâches terminées au format ZIP.

### Utilisation de l’API

Envoyez une requête au point de terminaison racine (`GET /`) de l’API en indiquant l’identifiant de la tâche dont vous souhaitez télécharger les résultats dans le chemin d’accès de la requête. [!DNL Privacy Service] Si l’état de la tâche est terminé, l’API inclut un attribut `downloadURL` dans le corps de la réponse. Cet attribut contient une URL que vous pouvez coller dans la barre d’adresse de votre navigateur pour télécharger le fichier ZIP.

Pour plus d’informations, reportez-vous à la section sur [recherche d’une tâche par son identifiant](api/privacy-jobs.md#check-the-status-of-a-job) dans le [!DNL Privacy Service] Guide de l’API.

### Utiliser l’interface utilisateur

Sur le [!DNL Privacy Service] Dans le tableau de bord de l’interface utilisateur, recherchez la tâche que vous souhaitez télécharger à partir du **Requêtes de tâche** widget. Sélectionnez l’identifiant de la tâche pour ouvrir la page Détails de la tâche. À partir de là, sélectionnez **Télécharger** dans le coin supérieur droit pour télécharger le fichier ZIP. Consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md) pour obtenir des instructions plus détaillées.

## Messages d’erreur courants

Le tableau suivant présente quelques erreurs courantes de la variable [!DNL Privacy Service], avec des descriptions pour aider à résoudre leurs problèmes respectifs.

| Message d’erreur | Description |
| --- | --- |
| Les ID utilisateur sont introuvables. | Certains des identifiants d’utilisateur fournis dans la requête sont introuvables et ont été ignorés. Assurez-vous que vous utilisez les valeurs d’identifiant et d’espace de noms correctes dans le payload de la requête. Consultez le document sur [fournir des données d’identité](./identity-data.md) pour une explication plus détaillée. |
| Espace de noms non valide | Un espace de noms d’identité fourni pour un identifiant utilisateur n’était pas valide. Voir la section sur [espaces de noms d’identité standard](./api/appendix.md#standard-namespaces) dans le [!DNL Privacy Service] annexe du guide d’API pour obtenir une liste des espaces de noms acceptés. Si vous utilisez un espace de noms personnalisé, veillez à définir les identifiants `type` à &quot;custom&quot;. |
| Partiellement terminé | La tâche s’est terminée avec succès, mais certaines données n’étaient pas applicables pour la requête donnée et ont été ignorées. |
| Les données ne sont pas au format requis. | Une ou plusieurs valeurs de données pour l’application spécifiée n’étaient pas correctement formatées. Pour plus d’informations, consultez les détails de la tâche. |
| L’organisation IMS n’a pas été configurée. | Ce message se produit lorsque votre organisation IMS n’a pas été configurée pour [!DNL Privacy Service]. Pour plus d’informations, contactez votre administrateur. |
| Des accès et des autorisations sont requis. | L’accès et les autorisations sont requis pour utiliser [!DNL Privacy Service]. Contactez votre administrateur pour obtenir l’accès. |
| Un problème est survenu lors du chargement et de l’archivage des données d’accès. | Lorsque cette erreur se produit, rechargez les données d’accès et réessayez. |
| La charge de travail a été dépassée pour la limite de débit de document actuelle. | Lorsque cette erreur se produit, réduisez le taux d’envoi et réessayez. |
