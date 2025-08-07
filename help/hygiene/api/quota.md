---
title: Point d’entrée de l’API Quota
description: Le point d’entrée /quota de l’API Data Hygiene vous permet de surveiller l’utilisation de la gestion avancée du cycle de vie des données par rapport aux limites mensuelles de quota de votre entreprise pour chaque type de tâche.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 23%

---

# Point d’entrée du quota

Utilisez le point d’entrée `/quota` dans l’API Data Hygiene pour vérifier l’utilisation et les limites actuelles de votre organisation. Les quotas varient en fonction des droits, tels que Privacy and Security Shield ou Healthcare Shield.

Surveillez votre consommation actuelle de quota pour vous assurer de la conformité aux limites organisationnelles pour chaque type de tâche.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de poursuivre, veuillez consulter la section [Présentation](./overview.md) pour obtenir les informations suivantes :

* Liens vers la documentation connexe
* Comment lire des exemples d’appels API
* En-têtes requis pour les appels API Experience Platform

## Quotas et délais de traitement {#quotas}

Les demandes de suppression d’enregistrements sont soumises à des quotas et à des attentes de niveau de service en fonction de vos droits de licence. Ces limites s’appliquent à la fois aux requêtes de suppression basées sur l’interface utilisateur et les API.

>[!TIP]
>
>Ce document vous explique comment interroger votre utilisation par rapport aux limites basées sur les droits. Pour une description complète des niveaux de quota, des droits de suppression d’enregistrements et du comportement de SLA, consultez les documents [suppression d’enregistrements basée sur l’interface utilisateur](../ui/record-delete.md#quotas) ou [suppression d’enregistrements basée sur l’API](./workorder.md#quotas).

## Quotas de liste {#list}

Vous pouvez afficher les informations sur le quota de votre entreprise en adressant une requête GET au point d’entrée `/quota`.

**Format d’API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

>[!NOTE]
>
>La consommation des quotas se réinitialise tous les jours et tous les mois le 1er de chaque mois à 00:00 GMT.
>
>Seules les requêtes acceptées sont prises en compte dans votre quota. Les ordres de travail rejetés ne réduisent pas votre quota.

| Paramètre | Description |
| --- | --- |
| `{QUOTA_TYPE}` | Paramètre de requête facultatif qui spécifie le type de quota à récupérer. Si aucun paramètre `quotaType` n’est fourni, toutes les valeurs de quota sont renvoyées dans la réponse de l’API. Les valeurs acceptées sont les suivantes :<ul><li>`datasetExpirationQuota` : nombre d’expirations de jeux de données actifs et votre tolérance totale.</li><li>`dailyConsumerDeleteIdentitiesQuota` : nombre d’enregistrements supprimés aujourd’hui et votre quota quotidien.</li><li>`monthlyConsumerDeleteIdentitiesQuota` : nombre d’enregistrements supprimés ce mois-ci et votre quota mensuel.</li></ul> |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**Réponse**

Une réponse réussie renvoie les détails de vos quotas de cycle de vie des données.

```json
{
  "quotas": [
    {
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| Propriété | Description |
| -------- | ------- |
| `quotas` | Répertorie les informations sur le quota pour chaque type de traitement du cycle de vie des données. Chaque objet Quota contient les propriétés suivantes :<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | Identifiant du type de quota. |
| `description` | Description des limites de ce quota. |
| `consumed` | Quantité de quota actuellement consommée. La quantité consommée se réinitialise le 1er du mois à 00:00 GMT et 00:00 GMT pour le quota quotidien. |
| `quota` | Allocation maximale de ce type de quota pour votre organisation. |
