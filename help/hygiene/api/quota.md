---
title: Point d’entrée de l’API Quota
description: Le point d’entrée /quota de l’API Data Hygiene vous permet de surveiller l’utilisation de la gestion avancée du cycle de vie des données par rapport aux limites mensuelles de quota de votre entreprise pour chaque type de tâche.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 4d34ae1885f8c4b05c7bb4ff9de9c0c0e26154bd
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 22%

---

# Point d’entrée du quota

Le point d’entrée `/quota` de l’API Data Hygiene vous permet de surveiller l’utilisation de la gestion avancée du cycle de vie des données par rapport aux limites de quota de votre entreprise pour chaque type de tâche.

L’utilisation du quota est suivie pour chaque type de tâche du cycle de vie des données. Vos limites de quota réelles dépendent des droits de votre organisation et peuvent être révisées périodiquement. L’expiration des jeux de données est soumise à une limite stricte du nombre de tâches actives simultanées.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de poursuivre, veuillez consulter la section [Présentation](./overview.md) pour obtenir les informations suivantes :

* Liens vers la documentation connexe
* Un guide de lecture des exemples d’appels API dans ce document
* Informations importantes concernant les en-têtes requis pour effectuer des appels vers n’importe quelle API Experience Platform

## Quotas et délais de traitement {#quotas}

Les demandes de suppression d’enregistrements sont soumises à des quotas et à des attentes de niveau de service en fonction de vos droits de licence. Ces limites s’appliquent à la fois aux requêtes de suppression basées sur l’interface utilisateur et les API.

>[!TIP]
> 
>Ce document vous explique comment interroger votre utilisation par rapport aux limites basées sur les droits. Pour une description complète des niveaux de quota, des droits de suppression d’enregistrements et du comportement de SLA, consultez les documents [Suppression d’enregistrements basée sur l’interface utilisateur](../ui/record-delete.md#quotas) ou [Suppression d’enregistrements basée sur l’API](./workorder.md#quotas).

## Quotas de liste {#list}

Vous pouvez afficher les informations sur le quota de votre entreprise en adressant une requête GET au point d’entrée `/quota`.

**Format d’API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Paramètre | Description |
| --- | --- |
| `{QUOTA_TYPE}` | Paramètre de requête facultatif qui spécifie le type de quota à récupérer. Si aucun paramètre `quotaType` n’est fourni, toutes les valeurs de quota sont renvoyées dans la réponse de l’API. Les valeurs de type acceptées sont les suivantes :<ul><li>`datasetExpirationQuota` : cet objet affiche le nombre d’expirations de jeux de données actifs simultanément pour votre organisation et votre tolérance totale d’expirations. </li><li>`dailyConsumerDeleteIdentitiesQuota` : Cet objet affiche le nombre total de demandes de suppression d&#39;enregistrements effectuées par votre organisation aujourd&#39;hui et votre allocation quotidienne totale.<br>Remarque : seules les demandes acceptées sont comptabilisées. Si un ordre de travail est rejeté car sa validation échoue, ces suppressions d’identité ne sont pas prises en compte dans votre quota.</li><li>`monthlyConsumerDeleteIdentitiesQuota` : cet objet affiche le nombre total de demandes de suppression d&#39;enregistrements effectuées par votre organisation ce mois-ci et votre allocation mensuelle totale.</li><li>`monthlyUpdatedFieldIdentitiesQuota` : Cet objet affiche le nombre total de demandes de mises à jour d&#39;enregistrements effectuées par votre organisation ce mois-ci et votre allocation mensuelle totale.</li></ul> |

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
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 1000000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 2000000
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
| -------- | ------- |
| `quotas` | Répertorie les informations sur le quota pour chaque type de traitement du cycle de vie des données. Chaque objet Quota contient les propriétés suivantes :<ul><li>`name` : type de traitement du cycle de vie des données :<ul><li>`expirationDatasetQuota` : expirations de jeux de données</li><li>`deleteIdentityWorkOrderDatasetQuota` : suppressions d’enregistrements</li></ul></li><li>`description` : description du type de traitement du cycle de vie des données.</li><li>`consumed` : nombre de traitements de ce type exécutés au cours de la période en cours. Le nom de l’objet indique la période de quota.</li><li>`quota` : allocation pour ce type de traitement pour votre organisation. Pour les suppressions et mises à jour d&#39;enregistrements, le quota représente le nombre de traitements pouvant être exécutés pour chaque période mensuelle. Pour les expirations de jeux de données, le quota représente le nombre de traitements pouvant être simultanément actifs à un moment donné.</li></ul> |
