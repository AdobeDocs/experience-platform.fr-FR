---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: FAQ sur Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 64cb2de507921fcb4aaade67132024a3fc0d3dee
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---


# FAQ sur Privacy Service

Ce document répond aux questions les plus fréquentes sur Adobe Experience Platform Privacy Service.

Privacy Service fournit une API RESTful et une interface utilisateur pour aider les sociétés à gérer les demandes de confidentialité des données client. Grâce à Privacy Service, vous pouvez envoyer des demandes d’accès et de suppression de données personnelles ou privées sur vos clients, ce qui vous permet de vous conformer automatiquement aux réglementations en matière de confidentialité en vigueur au sein de l’organisation et de la législation.

## Lors de l’exécution de demandes de confidentialité dans l’API, quelle est la différence entre un utilisateur et un ID utilisateur ? {#user-ids}

Pour effectuer une nouvelle tâche de confidentialité dans l’API, la charge utile JSON de la requête doit contenir un tableau qui liste des informations spécifiques pour chaque utilisateur auquel la requête de confidentialité s’applique. `users` Chaque élément du `users` tableau est un objet qui représente un utilisateur particulier, identifié par sa `key` valeur.

En retour, chaque objet utilisateur (ou `key`) contient son propre `userIDs` tableau. Ce tableau liste des valeurs d&#39;ID spécifiques **pour cet utilisateur** particulier.

Consider the following example `users` array:

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

Le tableau contient deux objets, représentant des utilisateurs individuels identifiés par leurs `key` valeurs (&quot;DavidSmith&quot; et &quot;user12345&quot;). &quot;DavidSmith&quot; ne possède qu’un seul identifiant (son adresse électronique), tandis que &quot;user12345&quot; en a deux (son adresse électronique et son ECID).

Pour plus d&#39;informations sur la fourniture d&#39;informations d&#39;identité des utilisateurs, consultez le guide sur les données d&#39; [identité pour les demandes](identity-data.md)de confidentialité.


## Puis-je utiliser Privacy Service pour nettoyer les données qui ont été envoyées accidentellement à Platform ?

Adobe ne prend pas en charge l’utilisation de Privacy Service pour effacer les données qui ont été envoyées accidentellement à un produit. Privacy Service est conçu pour vous aider à remplir vos obligations en ce qui concerne l&#39;accès aux données ou la suppression des demandes d&#39;accès ou de suppression des personnes concernées (ou des consommateurs). Ces demandes sont sensibles au temps et sont complétées en fonction de la loi sur la protection des renseignements personnels. La présentation de demandes qui ne sont pas des demandes d&#39;accès aux données ou aux consommateurs ou de suppression a des répercussions sur tous les clients du Service de la protection des renseignements personnels et sur la capacité du Service de la protection des renseignements personnels de prendre en charge les délais légaux appropriés.

Veuillez contacter votre gestionnaire de compte (MDP) pour coordonner et fournir un niveau d&#39;effort pour supprimer tout problème d&#39;informations d&#39;identification personnelle ou de données.

## Comment puis-je obtenir des informations sur l&#39;état de ma demande de confidentialité ou de mon travail ?

Vous pouvez récupérer des détails sur une tâche particulière à l’aide de l’API ou de l’interface utilisateur de Privacy Service.

### Utilisation de l’API

Pour récupérer l’état d’une tâche particulière à l’aide de l’API Privacy Service, effectuez une requête au point de terminaison racine (`GET /`), en utilisant l’ID de la tâche dans le chemin de la requête. Pour en savoir plus, consultez la section sur la [vérification de l’état d’un travail](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide du développeur de Privacy Service.

### Utilisation de l’interface utilisateur

Toutes les demandes de travaux actives sont répertoriées dans le widget Demandes **de** travaux du tableau de bord d’interface utilisateur de Privacy Service. L’état de chaque demande de travail s’affiche sous la colonne **État** . Pour plus d’informations sur l’affichage des demandes de travail dans l’interface utilisateur, consultez le guide [d’utilisation de](ui/user-guide.md)Privacy Service.

## Comment télécharger les résultats de mes tâches de confidentialité terminées ?

L’API et l’interface utilisateur de Privacy Service offrent toutes deux des méthodes pour télécharger les résultats des tâches terminées au format ZIP.

### Utilisation de l’API

Faites une requête au point de terminaison racine (`GET /`) de l’API de Privacy Service, en utilisant l’identifiant de la tâche dont vous souhaitez télécharger les résultats dans le chemin d’accès à la requête. Si l’état de la tâche est terminé, l’API inclut un `downloadURL` attribut dans le corps de la réponse. Cet attribut contient une URL que vous pouvez coller dans la barre d’adresse de votre navigateur pour télécharger le fichier ZIP.

Pour plus d’informations, voir la section relative à la [recherche d’un emploi par son identifiant](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide du développeur Privacy Service.

### Utilisation de l’interface utilisateur

Dans le tableau de bord d’interface utilisateur de Privacy Service, recherchez la tâche que vous souhaitez télécharger à partir du widget Demandes de **travaux** . Cliquez sur l’ID de la tâche pour ouvrir la page Détails _de la_ tâche. A partir de là, cliquez sur **Télécharger** dans le coin supérieur droit pour télécharger le fichier ZIP. Consultez le guide [d’utilisation de](ui/user-guide.md) Privacy Service pour obtenir des instructions plus détaillées.