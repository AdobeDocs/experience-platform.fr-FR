---
title: Point d’entrée de l’API Quota
description: Le point d’entrée /quota de l’API Data Hygiene vous permet de surveiller l’utilisation de l’hygiène des données par rapport aux limites mensuelles de quota de votre entreprise pour chaque type de traitement.
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 1c6a5df6473e572cae88a5980fe0db9dfcf9944e
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 88%

---

# Point d’entrée du quota

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données d’Adobe Experience Platform sont uniquement disponibles pour les organisations qui ont acheté **Adobe Healthcare Shield** ou **Adobe Privacy &amp; Security Shield**.

Le point d’entrée `/quota` de l’API Data Hygiene vous permet de surveiller votre utilisation de l’hygiène des données par rapport aux limites de quota de votre entreprise pour chaque type de tâche.

Les quotas sont appliqués pour chaque type de tâche d’hygiène des données de la manière suivante :

* Les suppressions d’enregistrements et les mises à jour sont limitées à un certain nombre de demandes par mois.
* Les expirations de jeux de données ont une limite plate pour le nombre de traitements principaux simultanés, quelle que soit la date d’exécution des expirations.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de poursuivre, veuillez consulter la section [Présentation](./overview.md) pour obtenir les informations suivantes :

* Liens vers la documentation connexe
* Un guide de lecture des exemples d’appels API dans ce document
* Informations importantes concernant les en-têtes requis pour réussir les appels à une API Experience Platform

## Quotas de liste {#list}

Vous pouvez afficher les informations sur le quota de votre entreprise en adressant une requête GET au point d’entrée `/quota`.

**Format d’API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Paramètre | Description |
| --- | --- |
| `{QUOTA_TYPE}` | Paramètre de requête facultatif qui spécifie le type de quota à récupérer. Si aucun paramètre `quotaType` n’est fourni, toutes les valeurs de quota sont renvoyées dans la réponse de l’API. Les valeurs de type acceptées sont les suivantes :<ul><li>`expirationDatasetQuota` : expirations de jeux de données</li><li>`deleteIdentityWorkOrderDatasetQuota`: Suppressions d’enregistrements</li><li>`fieldUpdateWorkOrderDatasetQuota`: Enregistrer les mises à jour</li></ul> |

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
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `quotas` | Répertorie les informations relatives aux quotas pour chaque type de traitement en matière d’hygiène des données. Chaque objet Quota contient les propriétés suivantes :<ul><li>`name` : le type de traitement d’hygiène des données :<ul><li>`expirationDatasetQuota` : expirations de jeux de données</li><li>`deleteIdentityWorkOrderDatasetQuota`: Suppressions d’enregistrements</li></ul></li><li>`description` : description du type de traitement d’hygiène des données.</li><li>`consumed` : le nombre de traitements de ce type s’exécutent sur la période mensuelle en cours.</li><li>`quota` : limite de quota pour ce type de traitement. Pour les suppressions et mises à jour d’enregistrement, cela représente le nombre de tâches pouvant être exécutées pour chaque période mensuelle. Pour les expirations de jeux de données, cela représente le nombre de traitements pouvant être simultanément actifs à un moment donné.</li></ul> |

{style=&quot;table-layout:auto&quot;}
