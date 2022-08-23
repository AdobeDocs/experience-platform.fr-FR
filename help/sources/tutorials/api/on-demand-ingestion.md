---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux ;
title: (Version bêta) Création d’une exécution de flux pour l’ingestion à la demande à l’aide de l’API Flow Service
description: Ce tutoriel décrit les étapes à suivre pour créer une exécution de flux pour l’ingestion à la demande à l’aide de l’API Flow Service.
source-git-commit: ab496c7a32c20487f47850c2c571976dff57704f
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 10%

---

# (Version bêta) Créez une exécution de flux pour l’ingestion à la demande à l’aide du [!DNL Flow Service] API

>[!IMPORTANT]
>
>L’ingestion à la demande est actuellement en version bêta et votre entreprise n’y a peut-être pas encore accès. Les fonctionnalités décrites dans cette documentation peuvent changer.

Les exécutions de flux représentent une instance d’exécution de flux. Par exemple, si un flux est planifié pour s’exécuter toutes les heures à 9 h, 10 h et 11 h, il y a trois instances d’une exécution de flux. Les exécutions de flux sont spécifiques à votre organisation particulière.

L’ingestion à la demande vous permet de créer une exécution de flux par rapport à un flux de données donné. Cela permet aux utilisateurs de créer une exécution de flux, en fonction de paramètres donnés, et de créer un cycle d’ingestion, sans jetons de service.

Ce tutoriel décrit les étapes à suivre pour utiliser l’ingestion à la demande et créer une exécution de flux à l’aide de la fonction [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

>[!NOTE]
>
>Pour créer une exécution de flux, vous devez d’abord disposer de l’identifiant de flux d’un flux de données planifié pour une ingestion unique.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

## Création d’une exécution de flux pour une source basée sur un tableau

Pour créer un flux pour une source basée sur un tableau, envoyez une requête de POST au [!DNL Flow Service] API tout en fournissant l’identifiant du flux sur lequel vous souhaitez créer l’exécution, ainsi que les valeurs des colonnes heure de début, heure de fin et delta.

>[!TIP]
>
>Les sources basées sur un tableau incluent les catégories de sources suivantes : publicités, analyses, consentement et préférences, CRM, succès client, base de données, automatisation du marketing, paiements et protocoles.

**Format d’API**

```http
POST /runs/
```

**Requête**

La requête suivante crée une exécution de flux pour l’ID de flux. `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Vous devez uniquement fournir la variable `deltaColumn` lors de la création de votre première exécution de flux. Après cela, `deltaColumn` sera corrigée dans le cadre de `copy` la transformation du flux et seront traités comme la source de la vérité. Toute tentative de modification de la variable `deltaColumn` dans les paramètres d’exécution de flux, entraîne une erreur.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| Paramètre | Description |
| --- | --- |
| `flowId` | L’identifiant du flux sur lequel votre exécution de flux sera créée. |
| `params.windowStartTime` | Entier qui définit l’heure de début de la fenêtre pendant laquelle les données doivent être extraites. La valeur est représentée en heure unix. |
| `params.windowEndTime` | Entier qui définit l’heure de fin de la fenêtre pendant laquelle les données doivent être extraites. La valeur est représentée en heure unix. |
| `params.deltaColumn` | La colonne delta est nécessaire pour partitionner les données et séparer les données nouvellement ingérées des données historiques. |
| `params.deltaColumn.name` | Nom de la colonne delta. |

**Réponse**

Une réponse réussie renvoie les détails de l’exécution de flux nouvellement créée, y compris son exécution unique. `id`.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567",
        "deltaColumn": {
            "name": "DOB"
        }
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Propriété | Description |
| --- | --- |
| `id` | L’identifiant de l’exécution de flux nouvellement créée. Consultez le guide sur la [récupération des spécifications de flux](../api/collect/database-nosql.md#specs) pour plus d’informations sur les spécifications d’exécution basées sur un tableau. |
| `createdAt` | Horodatage unix désignant le moment où l’exécution du flux a été créée. |
| `updatedAt` | Horodatage unix désignant le moment où l’exécution du flux a été mise à jour pour la dernière fois. |
| `createdBy` | ID d’organisation de l’utilisateur qui a créé l’exécution du flux. |
| `updatedBy` | ID d’organisation de l’utilisateur qui a mis à jour l’exécution du flux pour la dernière fois. |
| `createdClient` | Client de l’application qui a créé l’exécution du flux. |
| `updatedClient` | Client de l’application qui a mis à jour la dernière exécution du flux. |
| `sandboxId` | L’identifiant de l’environnement de test qui contient l’exécution du flux. |
| `sandboxName` | Nom de l’environnement de test qui contient l’exécution de flux. |
| `imsOrgId` | ID d’organisation. |
| `flowId` | Identifiant du flux par lequel l’exécution du flux est créée. |
| `params.windowStartTime` | Entier qui définit l’heure de début de la fenêtre pendant laquelle les données doivent être extraites. La valeur est représentée en heure unix. |
| `params.windowEndTime` | Entier qui définit l’heure de fin de la fenêtre pendant laquelle les données doivent être extraites. La valeur est représentée en heure unix. |
| `params.deltaColumn` | La colonne delta est nécessaire pour partitionner les données et séparer les données nouvellement ingérées des données historiques. **Remarque**: Le `deltaColumn` n’est nécessaire que lors de la création de votre première exécution de flux. |
| `params.deltaColumn.name` | Nom de la colonne delta. |
| `etag` | Version de ressource de l’exécution de flux. |
| `metrics` | Cette propriété affiche un résumé de l’état de l’exécution du flux. |

## Création d’une exécution de flux pour une source basée sur des fichiers

Pour créer un flux pour une source basée sur un fichier, envoyez une requête de POST au [!DNL Flow Service] API tout en fournissant l’identifiant du flux sur lequel vous souhaitez créer l’exécution et les valeurs pour l’heure de début et l’heure de fin.

>[!TIP]
>
>Les sources basées sur des fichiers comprennent toutes les sources de stockage dans le cloud.

**Format d’API**

```http
POST /runs/
```

**Requête**

La requête suivante crée une exécution de flux pour l’ID de flux. `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Paramètre | Description |
| --- | --- |
| `flowId` | L’identifiant du flux sur lequel votre exécution de flux sera créée. |
| `params.windowStartTime` | Entier qui définit l’heure de début de la fenêtre pendant laquelle les données doivent être extraites. La valeur est représentée en heure unix. |
| `params.windowEndTime` | Entier qui définit l’heure de fin de la fenêtre pendant laquelle les données doivent être extraites. La valeur est représentée en heure unix. |

**Réponse**

Une réponse réussie renvoie les détails de l’exécution de flux nouvellement créée, y compris son exécution unique. `id`.


```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567"
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Propriété | Description |
| --- | --- |
| `id` | L’identifiant de l’exécution de flux nouvellement créée. Consultez le guide sur la [récupération des spécifications de flux](../api/collect/cloud-storage.md#specs) pour plus d’informations sur les spécifications d’exécution basées sur les fichiers. |
| `createdAt` | Horodatage unix désignant le moment où l’exécution du flux a été créée. |
| `updatedAt` | Horodatage unix désignant le moment où l’exécution du flux a été mise à jour pour la dernière fois. |
| `createdBy` | ID d’organisation de l’utilisateur qui a créé l’exécution du flux. |
| `updatedBy` | ID d’organisation de l’utilisateur qui a mis à jour l’exécution du flux pour la dernière fois. |
| `createdClient` | Client de l’application qui a créé l’exécution du flux. |
| `updatedClient` | Client de l’application qui a mis à jour la dernière exécution du flux. |
| `sandboxId` | L’identifiant de l’environnement de test qui contient l’exécution du flux. |
| `sandboxName` | Nom de l’environnement de test qui contient l’exécution de flux. |
| `imsOrgId` | ID d’organisation. |
| `flowId` | Identifiant du flux par lequel l’exécution du flux est créée. |
| `params.windowStartTime` | Entier qui définit l’heure de début de la fenêtre pendant laquelle les données doivent être extraites. La valeur est représentée en heure unix. |
| `params.windowEndTime` | Entier qui définit l’heure de fin de la fenêtre pendant laquelle les données doivent être extraites. La valeur est représentée en heure unix. |
| `etag` | Version de ressource de l’exécution de flux. |
| `metrics` | Cette propriété affiche un résumé de l’état de l’exécution du flux. |


## Surveillance des exécutions de flux

Une fois l’exécution de flux créée, vous pouvez surveiller les données qui sont ingérées par celle-ci pour afficher des informations sur les exécutions de flux, l’état d’achèvement et les erreurs. Pour surveiller les exécutions de flux à l’aide de l’API, consultez le tutoriel sur [surveillance des flux de données dans l’API ](./monitor.md). Pour surveiller les exécutions de flux à l’aide de l’interface utilisateur de Platform, consultez le guide sur [surveillance des flux de données des sources à l’aide du tableau de bord de surveillance](../../../dataflows/ui/monitor-sources.md).
