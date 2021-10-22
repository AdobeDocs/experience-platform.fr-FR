---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Guide de dépannage des Privacy Service
topic-legacy: troubleshooting
description: Ce document fournit des réponses aux questions fréquemment posées sur le Privacy Service, ainsi que des informations sur les erreurs courantes rencontrées dans l’API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 41%

---

# Guide de dépannage du [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour aider les entreprises à gérer les demandes de confidentialité des données client. Avec [!DNL Privacy Service], vous pouvez soumettre des demandes d’accès et de suppression de données clients privées ou personnelles, ce qui facilite la conformité automatisée aux réglementations en matière de confidentialité organisationnelle et juridique.

Ce document fournit des réponses aux questions fréquemment posées au sujet de [!DNL Privacy Service], ainsi que des informations sur les erreurs fréquemment rencontrées dans l’API.

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


## Puis-je utiliser [!DNL Privacy Service] pour nettoyer les données qui ont été envoyées accidentellement à [!DNL Platform]?

Adobe ne prend pas en charge l’utilisation [!DNL Privacy Service] pour effacer les données qui ont été envoyées accidentellement à un produit. [!DNL Privacy Service] est conçu pour vous aider à remplir vos obligations en matière de requêtes d’accès ou de suppression des titulaires de données (ou consommateurs). Ces requêtes sont sensibles au facteur temps et sont effectuées en fonction des lois de confidentialité applicables. La présentation de demandes qui ne sont pas des demandes d&#39;accès aux données/aux consommateurs ou de suppression a des répercussions sur toutes les [!DNL Privacy Service] clients et capacité pour [!DNL Privacy Service] à l&#39;appui des délais légaux appropriés.

Veuillez contacter votre gestionnaire de compte (CDM) pour coordonner vos efforts et fournir un niveau de service adéquat en matière de suppression des données personnelles identifiables (PII) ou des problèmes relatifs aux données.

## Comment puis-je obtenir des informations sur l’état d’une requête ou d’une tâche de confidentialité ?

Vous pouvez récupérer les détails d’un travail particulier en utilisant l’attribut [!DNL Privacy Service] API ou interface utilisateur.

### Utilisation de l’API

Pour récupérer le statut d&#39;une tâche particulière à l&#39;aide de la [!DNL Privacy Service] API, effectuez une demande à la racine (`GET /`), en utilisant l&#39;ID de la tâche dans le chemin d&#39;accès de la demande. Pour plus d’informations, consultez la section sur [vérification de l&#39;état d&#39;un travail](api/privacy-jobs.md#check-the-status-of-a-job) dans la [!DNL Privacy Service] Guide de l’API.

### Utilisation de l’interface utilisateur

Toutes les requêtes de tâche actives sont répertoriées dans le widget **[!UICONTROL Requêtes de tâche]** accessible depuis le tableau de bord de l’interface utilisateur de [!DNL Privacy Service] L’état de chaque requête de tâche est affiché sous la colonne **[!UICONTROL État]**. Pour plus d’informations sur l’affichage des requêtes de tâche dans l’interface utilisateur, consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md).

## Comment télécharger les résultats de tâches de confidentialité terminées ?

Le [!DNL Privacy Service] L’API et l’interface utilisateur fournissent toutes deux des méthodes pour télécharger les résultats des travaux terminés au format ZIP.

### Utilisation de l’API

Envoyez une requête au point de terminaison racine (`GET /`) de l’API en indiquant l’identifiant de la tâche dont vous souhaitez télécharger les résultats dans le chemin d’accès de la requête. [!DNL Privacy Service] Si l’état de la tâche est terminé, l’API inclut un attribut `downloadURL` dans le corps de la réponse. Cet attribut contient une URL que vous pouvez coller dans la barre d’adresse de votre navigateur pour télécharger le fichier ZIP.

Pour plus d’informations, consultez la section sur [recherche d&#39;une tâche par son ID](api/privacy-jobs.md#check-the-status-of-a-job) dans la [!DNL Privacy Service] Guide de l’API.

### Utilisation de l’interface utilisateur

Sur la [!DNL Privacy Service] Tableau de bord de l’interface utilisateur, recherchez la tâche que vous souhaitez télécharger à partir du **Demandes de travaux** widget. Sélectionnez l&#39;ID de la tâche pour ouvrir la page Détails de la tâche. À partir de là, sélectionnez **Télécharger** dans le coin supérieur droit pour télécharger le fichier ZIP. Consultez le [guide d’utilisation de Privacy Service](ui/user-guide.md) pour obtenir des instructions plus détaillées.

## Messages d’erreur courants

Le tableau suivant présente quelques erreurs courantes dans [!DNL Privacy Service], avec des descriptions pour aider à résoudre leurs problèmes respectifs.

| Message d’erreur | Description |
| --- | --- |
| ID utilisateur introuvable. | Certains ID utilisateur fournis dans la demande sont introuvables et ont été ignorés. Assurez-vous d’utiliser les espaces de noms et les valeurs d’ID corrects dans la charge utile de la demande. Voir le document sur [fourniture de données d’identité](./identity-data.md) pour une explication plus détaillée. |
| Espace de noms non valide | Un espace de noms d&#39;identité fourni pour un ID utilisateur n&#39;était pas valide. Consultez la section sur [espaces de noms d’identité standard](./api/appendix.md#standard-namespaces) dans la [!DNL Privacy Service] Annexe du guide d’API pour une liste d’espaces de noms acceptés. Si vous utilisez un espace de noms personnalisé, assurez-vous de définir l’ID `type` à &quot;custom&quot;. |
| Partiellement terminé | La tâche s&#39;est terminée avec succès, mais certaines données n&#39;étaient pas applicables à la demande donnée et ont été ignorées. |
| Les données ne sont pas dans le format requis. | Une ou plusieurs valeurs de données pour l&#39;application spécifiée n&#39;ont pas été correctement formatées. Pour plus d’informations, consultez les détails de la tâche. |
| L&#39;organisation IMS n&#39;a pas été configurée. | Ce message se produit lorsque votre organisation IMS n&#39;a pas été configurée pour [!DNL Privacy Service]. Pour plus d’informations, contactez votre administrateur. |
| L’accès et les autorisations sont requis. | L’accès et les autorisations sont requis pour utiliser [!DNL Privacy Service]. Contactez votre administrateur pour obtenir l’accès. |
| Un problème est survenu lors du chargement et de l&#39;archivage des données d&#39;accès. | Lorsque cette erreur se produit, rechargez les données d’accès et réessayez. |
| La charge de travail a été dépassée pour la limite de taux de document actuelle. | Lorsque cette erreur se produit, réduisez le taux d’envoi et réessayez. |
