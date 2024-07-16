---
title: Point d’entrée de l’API Quota
description: Le point d’entrée /quota de l’API Data Hygiene vous permet de surveiller l’utilisation de la gestion avancée du cycle de vie des données par rapport aux limites mensuelles de quota de votre entreprise pour chaque type de tâche.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 48a83e2b615fc9116a93611a5e6a8e7f78cb4dee
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 29%

---

# Point d’entrée du quota

Le point d’entrée `/quota` de l’API Data Hygiene vous permet de surveiller l’utilisation de la gestion avancée du cycle de vie des données par rapport aux limites de quota de votre entreprise pour chaque type de tâche.

Les quotas sont appliqués pour chaque type de tâche Data Lifecycle de la manière suivante :

* Les suppressions d’enregistrements et les mises à jour sont limitées à un certain nombre de demandes par mois.
* Les expirations de jeux de données ont une limite plate pour le nombre de traitements principaux simultanés, quelle que soit la date d’exécution des expirations.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de poursuivre, veuillez consulter la section [Présentation](./overview.md) pour obtenir les informations suivantes :

* Liens vers la documentation connexe
* Un guide de lecture des exemples d’appels API dans ce document
* Informations importantes concernant les en-têtes requis pour effectuer des appels vers une API Experience Platform

## Quotas de liste {#list}

Vous pouvez afficher les informations sur le quota de votre entreprise en adressant une requête GET au point d’entrée `/quota`.

**Format d’API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Paramètre | Description |
| --- | --- |
| `{QUOTA_TYPE}` | Paramètre de requête facultatif qui spécifie le type de quota à récupérer. Si aucun paramètre `quotaType` n’est fourni, toutes les valeurs de quota sont renvoyées dans la réponse de l’API. Les valeurs de type acceptées sont les suivantes :<ul><li>`datasetExpirationQuota` : cet objet indique le nombre d’expirations de jeux de données actives simultanées pour votre organisation, ainsi que votre limite totale d’expirations. </li><li>`dailyConsumerDeleteIdentitiesQuota` : cet objet indique le nombre total de demandes de suppression d’enregistrements effectuées par votre organisation aujourd’hui et votre allocation quotidienne totale.<br>Remarque : Seules les demandes acceptées sont comptabilisées. Si une commande de travail est rejetée parce qu’elle ne parvient pas à être validée, ces suppressions d’identité ne sont pas prises en compte par rapport à votre quota.</li><li>`monthlyConsumerDeleteIdentitiesQuota` : cet objet indique le nombre total de demandes de suppression d’enregistrements effectuées par votre organisation ce mois-ci et votre allocation mensuelle totale.</li><li>`monthlyUpdatedFieldIdentitiesQuota` : cet objet indique le nombre total de demandes de mise à jour des enregistrements effectuées par votre organisation ce mois-ci et votre allocation mensuelle totale.</li></ul> |

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

Une réponse réussie renvoie les détails des quotas de cycle de vie des données.

```json
{
  "quotas": [
    {
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 600000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 600000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `quotas` | Répertorie les informations de quota pour chaque type de tâche de cycle de vie des données. Chaque objet Quota contient les propriétés suivantes :<ul><li>`name` : type de tâche du cycle de vie des données :<ul><li>`expirationDatasetQuota` : expirations de jeux de données</li><li>`deleteIdentityWorkOrderDatasetQuota` : Suppressions d’enregistrements</li></ul></li><li>`description` : description du type de tâche du cycle de vie des données.</li><li>`consumed` : nombre de tâches de ce type exécutées au cours de la période en cours. Le nom de l’objet indique la période du quota.</li><li>`quota` : allocation de ce type de tâche pour votre organisation. Pour les suppressions et mises à jour d’enregistrements, le quota représente le nombre de tâches pouvant être exécutées pour chaque période mensuelle. Pour les expirations de jeux de données, le quota représente le nombre de tâches pouvant être actives simultanément à un moment donné.</li></ul> |

{style="table-layout:auto"}
