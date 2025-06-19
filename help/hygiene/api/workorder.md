---
title: Demandes De Suppression D’Enregistrements (Point D’Entrée De L’Ordre De Travail)
description: Le point d’entrée /workorder de l’API Data Hygiene vous permet de gérer par programmation les tâches de suppression des identités.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: d569b1d04fa76e0a0e48364a586e8a1a773b9bf2
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 48%

---

# Demandes de suppression d’enregistrements (point d’entrée de l’ordre de travail) {#work-order-endpoint}

Le point d’entrée `/workorder` de l’API Data Hygiene vous permet de gérer par programmation les demandes de suppression d’enregistrements dans Adobe Experience Platform.

>[!IMPORTANT]
> 
>Les suppressions d’enregistrements sont destinées au nettoyage des données, à la suppression des données anonymes ou à la minimisation des données. Elles ne sont **pas** destinées aux demandes de droits des titulaires de données (conformité) en ce qui concerne les réglementations de confidentialité comme le Règlement général sur la protection des données (RGPD). Pour tous les cas d’utilisation de conformité, utilisez plutôt [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de continuer, consultez la [présentation](./overview.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Quotas et délais de traitement {#quotas}

Les demandes de suppression d’enregistrements sont soumises à des limites d’envoi d’identifiants quotidiennes et mensuelles, déterminées par les droits de licence de votre entreprise. Ces limites s’appliquent à la fois aux requêtes de suppression basées sur l’interface utilisateur et les API.

>[!NOTE]
>
>Vous pouvez envoyer jusqu’à 1 000 000 **d’identifiants par jour** mais uniquement si votre quota mensuel restant le permet. Si votre limite mensuelle est inférieure à 1 million, vos soumissions quotidiennes ne peuvent pas dépasser cette limite.

### Droit d’envoi mensuel par produit {#quota-limits}

Le tableau ci-dessous présente les limites d’envoi des identifiants par produit et niveau de droit. Pour chaque produit, la limite mensuelle est la moins élevée des deux valeurs suivantes : un plafond d’identifiant fixe ou un seuil basé sur un pourcentage lié à votre volume de données sous licence.

| Produit | Description du droit | Plafond mensuel (le moins élevé) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP ou Adobe Journey Optimizer | Sans Privacy and Security Shield ni module complémentaire Healthcare Shield | 2 000 000 d’identifiants ou 5 % de l’audience adressable |
| Real-Time CDP ou Adobe Journey Optimizer | Avec le module complémentaire Privacy and Security Shield ou Healthcare Shield | 15 000 000 d’identifiants ou 10 % de l’audience adressable |
| Customer Journey Analytics | Sans Privacy and Security Shield ni module complémentaire Healthcare Shield | 2 000 000 d’identifiants ou 100 d’identifiants par million de lignes CJA de droits |
| Customer Journey Analytics | Avec le module complémentaire Privacy and Security Shield ou Healthcare Shield | 15 000 000 d’identifiants ou 200 d’identifiants par million de lignes CJA de droits |

>[!NOTE]
>
> La plupart des entreprises ont des limites mensuelles inférieures en fonction de leur audience adressable réelle ou de leurs droits de ligne CJA.

Les quotas sont réinitialisés le premier jour de chaque mois civil. Le quota inutilisé n **est pas reporté**

>[!NOTE]
>
>Les quotas sont basés sur les droits mensuels sous licence de votre entreprise pour les **identifiants envoyés**. Elles ne sont pas appliquées par les mécanismes de sécurisation du système, mais peuvent être surveillées et examinées.
>
>La suppression d’enregistrements est un **service partagé**. Votre limite mensuelle reflète les droits les plus élevés pour Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics et tous les modules complémentaires Shield applicables.

### Chronologies de traitement des envois d’identifiants {#sla-processing-timelines}

Après l’envoi, les demandes de suppression d’enregistrements sont mises en file d’attente et traitées en fonction de votre niveau de droits.

| Description du produit et des droits | Durée de la file d’attente | Durée Maximale De Traitement (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Sans Privacy and Security Shield ni module complémentaire Healthcare Shield | Jusqu’à 15 jours | 30 jours |
| Avec le module complémentaire Privacy and Security Shield ou Healthcare Shield | Généralement 24 heures | 15 jours |

Si votre organisation requiert des limites plus élevées, contactez votre représentant Adobe pour une révision des droits.

>[!TIP]
>
>Pour vérifier votre niveau d’utilisation ou de droit de quota actuel, consultez le [Guide de référence des quotas](../api/quota.md).

## Créer une requête de suppression d’enregistrement {#create}

Vous pouvez supprimer une ou plusieurs identités d’un seul jeu de données ou de tous les jeux de données en effectuant une requête POST au point d’entrée `/workorder`.

>[!TIP]
>
>Chaque demande de suppression d’enregistrement envoyée via l’API peut inclure jusqu’à 100 000 **d’identités**. Pour optimiser l’efficacité, envoyez autant d’identités par requête que possible et évitez les envois en faible volume, tels que les ordres de travail à ID unique.

**Format d’API**

```http
POST /workorder
```

>[!NOTE]
>
>Les requêtes de cycle de vie des données peuvent uniquement modifier les jeux de données en fonction d’identités principales ou d’un mappage d’identités. Une requête doit spécifier l’identité principale ou fournir un mappage d’identités.

**Requête**

En fonction de la valeur de la `datasetId` fournie dans le payload de requête, l’appel API supprime les identités de tous les jeux de données ou d’un seul jeu de données que vous spécifiez. La requête suivante supprime trois identités d’un jeu de données spécifique.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "displayName": "Example Record Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `action` | L’action à effectuer. La valeur doit être définie sur `delete_identity` pour les suppressions d’enregistrements. |
| `datasetId` | Si vous effectuez une suppression dans un seul jeu de données, cette valeur doit correspondre à l’identifiant du jeu de données en question. Si vous effectuez une suppression dans tous les jeux de données, définissez la valeur sur `ALL`.<br><br>Si vous spécifiez un seul jeu de données, une identité principale doit être définie pour le schéma de modèle de données d’expérience (XDM) associé au jeu de données. Si le jeu de données ne dispose pas d’une identité principale, il doit disposer d’un mappage d’identités pour être modifié par une requête relative au cycle de vie des données.<br>S’il existe un mappage d’identités, il est présent sous la forme d’un champ de niveau supérieur nommé `identityMap`.<br>Notez qu’une ligne de jeu de données peut avoir plusieurs identités dans son mappage d’identités, mais une seule peut être marquée comme principale. `"primary": true` doit être inclus pour forcer le `id` à correspondre à une identité principale. |
| `displayName` | Nom d’affichage de la requête de suppression d’enregistrement. |
| `description` | Description de la requête de suppression d’enregistrement. |
| `identities` | Un tableau contenant les identités d’au moins un utilisateur dont vous souhaitez supprimer les informations. Chaque identité se compose d’un [espace de noms d’identité](../../identity-service/features/namespaces.md) et d’une valeur :<ul><li>`namespace` : contient une seule propriété de chaîne, `code`, qui représente l’espace de noms d’identité. </li><li>`id` : la valeur de l’identité.</ul>Si `datasetId` spécifie un seul jeu de données, chaque entité sous `identities` doit utiliser le même espace de noms d’identité que l’identité principale du schéma.<br><br>Si `datasetId` est défini sur `ALL`, le tableau `identities` n’est limité à aucun espace de noms unique, car chaque jeu de données peut être différent. Toutefois, les requêtes sont toujours limitées aux espaces de noms disponibles pour l’organisation, comme indiqué par le [service d’identités](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la suppression de l’enregistrement.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Propriété | Description |
| --- | --- |
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher le statut de la suppression ultérieurement. |
| `orgId` | Votre identifiant d’organisation. |
| `bundleId` | L’identifiant de l’offre groupée à laquelle cet ordre de suppression est associé, utilisé à des fins de débogage. Plusieurs ordres de suppression sont regroupés pour être traités par les services en aval. |
| `action` | L’action effectuée par l’ordre de travail. Pour les suppressions d’enregistrements, la valeur est `identity-delete`. |
| `createdAt` | La date et l’heure de création de l’ordre de suppression. |
| `updatedAt` | La date et l’heure de la dernière mise à jour de l’ordre de suppression. |
| `status` | Le statut actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |
| `datasetId` | L’identifiant du jeu de données sujet à la requête. Si la requête porte sur tous les jeux de données, la valeur est définie sur `ALL`. |

{style="table-layout:auto"}

## Récupération du statut d’une suppression d’enregistrement {#lookup}

Après avoir [créé une demande de suppression d’enregistrement](#create), vous pouvez vérifier son statut à l’aide d’une demande GET.

**Format d’API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Paramètre | Description |
| --- | --- |
| `{WORK_ORDER_ID}` | `workorderId` de la suppression d’enregistrement que vous recherchez. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’opération de suppression, y compris son statut actuel.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher le statut de la suppression ultérieurement. |
| `orgId` | Votre identifiant d’organisation. |
| `bundleId` | L’identifiant de l’offre groupée à laquelle cet ordre de suppression est associé, utilisé à des fins de débogage. Plusieurs ordres de suppression sont regroupés pour être traités par les services en aval. |
| `action` | L’action effectuée par l’ordre de travail. Pour les suppressions d’enregistrements, la valeur est `identity-delete`. |
| `createdAt` | La date et l’heure de création de l’ordre de suppression. |
| `updatedAt` | La date et l’heure de la dernière mise à jour de l’ordre de suppression. |
| `status` | Le statut actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |
| `datasetId` | L’identifiant du jeu de données sujet à la requête. Si la requête porte sur tous les jeux de données, la valeur est définie sur `ALL`. |
| `productStatusDetails` | Un tableau qui répertorie le statut actuel des processus en aval liés à la requête. Chaque objet Tableau contient les propriétés suivantes :<ul><li>`productName` : le nom du service en aval.</li><li>`productStatus` : le statut actuel du traitement de la requête du service en aval.</li><li>`createdAt` : la date et l’heure auxquelles le statut le plus récent a été publié par le service.</li></ul> |

## Mettre à jour une requête de suppression d’enregistrement

Vous pouvez mettre à jour les `displayName` et les `description` d’une suppression d’enregistrement en effectuant une requête PUT.

**Format d’API**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Paramètre | Description |
| --- | --- |
| `{WORK_ORDER_ID}` | `workorderId` de la suppression d’enregistrement que vous recherchez. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| Propriété | Description |
| --- | --- |
| `displayName` | Nom d’affichage mis à jour pour la requête de suppression d’enregistrement. |
| `description` | Description mise à jour de la requête de suppression d’enregistrement. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la suppression de l’enregistrement.

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
    "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher le statut de la suppression ultérieurement. |
| `orgId` | Votre identifiant d’organisation. |
| `bundleId` | L’identifiant de l’offre groupée à laquelle cet ordre de suppression est associé, utilisé à des fins de débogage. Plusieurs ordres de suppression sont regroupés pour être traités par les services en aval. |
| `action` | L’action effectuée par l’ordre de travail. Pour les suppressions d’enregistrements, la valeur est `identity-delete`. |
| `createdAt` | La date et l’heure de création de l’ordre de suppression. |
| `updatedAt` | La date et l’heure de la dernière mise à jour de l’ordre de suppression. |
| `status` | Le statut actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |
| `datasetId` | L’identifiant du jeu de données sujet à la requête. Si la requête porte sur tous les jeux de données, la valeur est définie sur `ALL`. |
| `productStatusDetails` | Un tableau qui répertorie le statut actuel des processus en aval liés à la requête. Chaque objet Tableau contient les propriétés suivantes :<ul><li>`productName` : le nom du service en aval.</li><li>`productStatus` : le statut actuel du traitement de la requête du service en aval.</li><li>`createdAt` : la date et l’heure auxquelles le statut le plus récent a été publié par le service.</li></ul> |

{style="table-layout:auto"}
