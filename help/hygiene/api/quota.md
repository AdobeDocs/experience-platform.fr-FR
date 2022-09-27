---
title: Point de terminaison de l’API Quota
description: Le point de terminaison /quota de l’API Data Hygiene vous permet de surveiller votre utilisation de l’hygiène des données par rapport aux limites mensuelles de quota de votre entreprise pour chaque type d’opération.
source-git-commit: 364ada0c354ddba8a855945f4f806f5600f21416
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Point d&#39;entrée du quota

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données d’Adobe Experience Platform sont uniquement disponibles pour les organisations qui ont acheté Healthcare Shield.

Le `/quota` Le point de terminaison de l’API Data Hygiene vous permet de surveiller votre utilisation de l’hygiène des données par rapport aux limites de quota de votre entreprise pour chaque type d’opération.

Les quotas sont appliqués pour chaque type de tâche d’hygiène des données de la manière suivante :

* Les suppressions par les consommateurs et les mises à jour des champs sont limitées à un certain nombre de demandes par mois.
* Les expirations de jeux de données ont une limite plate pour le nombre de tâches principales simultanées, quelle que soit la date d’exécution des expirations.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de poursuivre, veuillez consulter la section [aperçu](./overview.md) pour obtenir les informations suivantes :

* Liens vers la documentation connexe
* Un guide de lecture des exemples d’appels API dans ce document
* Informations importantes concernant les en-têtes requis pour réussir les appels à une API Experience Platform

## Quotas de liste {#list}

Vous pouvez afficher les informations sur le quota de votre entreprise en adressant une demande de GET à la variable `/quota` point de terminaison .

**Format d’API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Paramètre | Description |
| --- | --- |
| `{QUOTA_TYPE}` | Paramètre de requête facultatif qui spécifie le type de quota à récupérer. Si non `quotaType` est fourni, toutes les valeurs de quota sont renvoyées dans la réponse de l’API. Les valeurs de type acceptées sont les suivantes :<ul><li>`expirationDatasetQuota`: Expirations de jeux de données</li><li>`deleteIdentityWorkOrderDatasetQuota`: Suppressions des consommateurs</li><li>`fieldUpdateWorkOrderDatasetQuota`: Mises à jour des champs</li></ul> |

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

Une réponse réussie renvoie les détails de vos quotas d’hygiène des données.

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Consumer Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `quotas` | Répertorie les informations relatives aux quotas pour chaque type d’emploi en matière d’hygiène des données. Chaque objet Quota contient les propriétés suivantes :<ul><li>`name`: Le type d&#39;opération d&#39;hygiène des données :<ul><li>`expirationDatasetQuota`: Expirations de jeux de données</li><li>`deleteIdentityWorkOrderDatasetQuota`: Suppressions des consommateurs</li></ul></li><li>`description`: Description du type de tâche d’hygiène des données.</li><li>`consumed`: Le nombre de tâches de ce type s’exécutent sur la période mensuelle en cours.</li><li>`quota`: Limite de quota pour ce type de tâche. Pour les suppressions par les consommateurs et les mises à jour de champs, cela représente le nombre de tâches pouvant être exécutées pour chaque période mensuelle. Pour les expirations de jeux de données, cela représente le nombre de tâches pouvant être simultanément principales à un moment donné.</li></ul> |

{style=&quot;table-layout:auto&quot;}
