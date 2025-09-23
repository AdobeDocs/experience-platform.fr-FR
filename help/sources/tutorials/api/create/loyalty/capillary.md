---
title: Connecter Capillaire à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter Capillary à Experience Platform à l’aide d’API.
hide: true
hidefromtoc: true
source-git-commit: 7119ca51e0a4db09c8adb68bcde41ab3837439d1
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 8%

---

# Connexion de [!DNL Capillary Streaming Events] à Experience Platform à l’aide de l’API [!DNL Flow Service]

Lisez ce guide pour savoir comment utiliser le [!DNL Capillary Streaming Events] et l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) pour diffuser des données de votre compte [!DNL Capillary] vers Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Collecter les informations d’identification requises

Lisez la [[!DNL Capillary Streaming Events] présentation](../../../../connectors/loyalty/capillary.md) pour plus d’informations sur l’authentification.

### Utilisation des API Experience Platform

Lisez le guide sur [Prise en main des API Experience Platform](../../../../../landing/api-guide.md) pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform.

>[!BEGINSHADEBOX]

## Liste de contrôle du processus du développeur

1. Créez ou choisissez votre cible **schéma de modèle de données d’expérience (XDM)** à l’aide du registre des schémas. Utilisez ce schéma XDM pour **créer un jeu de données** dans Catalog Service.
2. Créez une **connexion de base** pour stocker vos informations d’identification [!DNL Capillary].
3. Créez une **connexion source** pour créer une liaison à votre `baseConnectionId`.
4. Créez une **connexion cible** pour vous assurer que vos données se trouvent dans le lac de données.
5. Utilisez la préparation des données pour créer des mappages qui mappent vos champs source [!DNL Capillary] aux champs XDM corrects.
6. Créer un flux de données à l’aide de vos `sourceConnectionId`, `targetConnectionId` et `mappingID`
7. Effectuez un test électronique avec un seul exemple de profil/événement de transaction pour vérifier votre flux de données.

>[!ENDSHADEBOX]

## Créer une connexion de base {#base-connection}

Une connexion de base conserve les informations d’identification et de connexion. Pour créer une connexion de base pour [!DNL Capillary], envoyez une requête POST au point d’entrée `/connections` de l’API [!DNL Flow Service] et indiquez vos informations d’identification de [!DNL Capillary] dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Capillary] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**Réponse**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Créer une connexion source

Pour créer une connexion source, envoyez une requête POST au point d’entrée `/sourceConnections` et indiquez votre identifiant de connexion de base.

**Format d’API**

```http
POST /flowservice/sourceConnections
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**Réponse**

Une réponse réussie renvoie le statut HTTP 201 avec les détails de la connexion source nouvellement créée, y compris son identifiant unique (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### Configurations de schéma

>[!BEGINTABS]

>[!TAB Ingestion de profil]

Les profils contiennent des attributs d’identité et de fidélité. Affichez la payload suivante pour un exemple basé sur le schéma de profil [!DNL Capillary]. Vous pouvez configurer et mapper ce schéma à un profil individuel XDM.

**Requête**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**Réponse**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB Ingestion des transactions]

Les transactions capturent les activités commerciales. Affichez la payload suivante pour obtenir un exemple en fonction du schéma d’événements [!DNL Capillary]. Vous pouvez configurer et mapper ce schéma à un événement d’expérience XDM.

**Requête**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**Réponse**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

### Événements pris en charge

La source [!DNL Capillary] prend en charge les événements suivants :

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`


### Migration des données historiques

Vous pouvez importer vos données historiques de fidélité et de transaction dans Experience Platform. Il vous suffit d’exporter vos données au format CSV structuré à partir de [!DNL Capillary], de les transférer en toute sécurité à l’aide de [!DNL SFTP] et de les ingérer dans vos jeux de données Experience Platform. Après la migration initiale, vos données restent à jour en temps réel grâce au connecteur piloté par les événements.

### Créer un schéma XDM cible {#target-schema}

Un schéma de modèle de données d’expérience (XDM) offre un moyen normalisé d’organiser et de décrire les données d’expérience client dans Experience Platform. Pour ingérer les données sources dans Experience Platform, vous devez d’abord créer un schéma XDM cible qui définit la structure et les types de données à ingérer. Ce schéma sert de plan directeur pour le jeu de données Experience Platform où se trouveront vos données ingérées.

Un schéma XDM cible peut être créé en adressant une requête POST à l’[API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, consultez les guides suivants :

* [Créez un schéma à l’aide de l’API](../../../../../xdm/api/schemas.md).
* [Créez un schéma à l’aide de l’interface utilisateur](../../../../../xdm/tutorials/create-schema-ui.md).

Une fois créé, le schéma XDM cible `$id` sera requis ultérieurement pour votre jeu de données cible et votre mappage.

## Créer un jeu de données cible {#target-dataset}

Un jeu de données est une structure de stockage et de gestion pour une collection de données, généralement structurée comme un tableau avec des colonnes (schéma) et des lignes (champs). Les données correctement ingérées par Experience Platform sont stockées dans le lac de données sous forme de jeux de données. Au cours de cette étape, vous pouvez créer un jeu de données ou en utiliser un existant.

Vous pouvez créer un jeu de données cible en adressant une requête POST à l’[API Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/), tout en fournissant l’identifiant du schéma cible dans la payload. Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, consultez le guide [création d’un jeu de données à l’aide de l’API](../../../../../catalog/api/create-dataset.md).


## Créer une connexion cible {#target}

Une connexion cible représente la connexion à la destination où se trouvent les données ingérées. Pour créer une connexion cible, vous devez fournir l’identifiant fixe de spécification de connexion associé au lac de données. Cet identifiant de spécification de connexion est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**Format d’API**

```http
POST /targetConnections
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### Créer un mappage {#mapping}

Mappez ensuite vos données source au schéma cible auquel votre jeu de données cible se conforme. Pour créer un mappage, envoyez une requête POST au point d’entrée `mappingSets` de l’[[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Incluez votre identifiant de schéma XDM cible et les détails des jeux de mappages que vous souhaitez créer.

Mappez les champs capillaires aux champs de schéma XDM correspondants comme suit :

| Schéma source | Schéma cible |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email` |
| `loyalty.points` | `xdm:loyaltyPoints` |
| `loyalty.tier` | `xdm:loyaltyTier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

### Créer un flux de données {#flow}

Après avoir créé la connexion source, le mappage et la connexion cible, vous pouvez configurer un flux de données pour déplacer les données de [!DNL Capillary] vers Experience Platform.

Les flux de données standard incluent :

* **Flux de données de profil** : permet d’ingérer [!DNL Capillary] données de profil dans un jeu de données XDM Individual Profile.
* **Flux de données de transaction** : ingère [!DNL Capillary] données de transaction dans un jeu de données XDM ExperienceEvent.

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime` est en secondes UNIX epoch.

**Réponse**

Une réponse réussie renvoie votre flux de données avec son identifiant de flux de données correspondant.

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## Traitement des erreurs

Le connecteur offre une gestion des erreurs robuste pour les scénarios suivants :

* **Erreurs d’authentification** : actualise automatiquement les informations d’identification Adobe en cas d’échec de l’authentification.
* **Erreurs de limite de débit** : implémente des reprises avec arrêt exponentiel lorsque les limites de débit de l’API sont atteintes.
* **Erreurs réseau** : les journaux et les reprises ont échoué dans les requêtes réseau.
* **Erreurs de validation des données** : consigne les payloads non valides pour une révision et une résolution manuelles.

Toutes les erreurs sont consignées avec des détails tels que le type d’erreur, l’horodatage, la payload de la requête et la réponse de l’API Adobe pour faciliter le dépannage et le débogage.

## Tester votre connexion

Suivez les étapes ci-dessous pour découvrir les étapes à suivre pour tester votre connexion :

* Envoyez une requête GET à `/connections/{BASE_CONNECTION_ID}` et indiquez votre identifiant de connexion de base pour vérifier que votre connexion de base existe. Au cours de cette étape, vous pouvez également vérifier que l’état de votre connexion de base est défini sur `active`.
* Envoyez une requête GET à `/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}` et indiquez votre identifiant de connexion source pour vérifier votre connexion source.
* Utilisez l’URL de point d’entrée de diffusion en continu pour envoyer un exemple de payload de profil (utilisez le fichier JSON d’ingestion de profil).
* Accédez à votre jeu de données dans l’interface utilisateur d’Experience Platform et exécutez une requête sur le jeu de données pour confirmer vos enregistrements.
* Utilisez les journaux de préparation des données pour rechercher des erreurs.
* Si vous devez ouvrir un ticket d’assistance, vérifiez que vous disposez des éléments suivants :
   * Payload de demande
   * Corps de réponse
   * Request-id
   * date et heure
   * ID de ressource.

## Annexe

Consultez la documentation suivante pour obtenir des guides sur les opérations supplémentaires

* [Surveillance des flux de données](../../../../../dataflows/ui/monitor-sources.md)
* [Mettre à jour des flux de données](../../../ui/update-dataflows.md)
* [Supprimer des flux de données](../../../ui/delete.md)
* [Mettre à jour le compte source](../../../ui/update.md)
