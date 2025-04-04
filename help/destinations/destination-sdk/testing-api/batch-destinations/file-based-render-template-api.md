---
description: Cette page explique comment utiliser le point d’entrée /authoring/testing/template/render pour visualiser à quoi ressembleraient les champs de données clients modélisés définis dans votre configuration de destination.
title: Validation des champs client générés par le modèle
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 88%

---


# Validation des champs client générés par le modèle

## Vue d’ensemble {#overview}

Le point d’entrée `/authoring/testing/template/render` vous permet de visualiser à quoi les [champs de données client](../../functionality/destination-configuration/customer-data-fields.md) modélisés définis dans votre configuration de destination ressembleraient.

Le point d’entrée génère des valeurs aléatoires pour vos champs de données client et les renvoie dans la réponse. Cela vous permet de valider la structure sémantique des champs de données client, tels que les noms de compartiment ou les chemins d’accès au dossier.

## Prise en main {#getting-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Conditions préalables {#prerequisites}

Avant d’utiliser le point d’entrée `/template/render`, veillez à respecter les conditions suivantes :

* Une destination existante basée sur des fichiers a été créée avec Destination SDK et vous pouvez la voir dans votre [catalogue de destination](../../../ui/destinations-workspace.md).
* Pour réussir la requête API, vous avez besoin de l’identifiant d’instance de destination correspondant à l’instance de destination que vous allez tester. Obtenez l’identifiant d’instance de destination que vous devez utiliser dans l’appel API, à partir de l’URL, lorsque vous parcourez une connexion avec la destination dans l’interface utilisateur d’Experience Platform.

  ![Image de l’interface utilisateur montrant comment obtenir l’identifiant d’instance de destination à partir de l’URL.](../../assets/testing-api/get-destination-instance-id.png)

## Rendu des champs clients modélisés {#render-customer-fields}

**Format d’API**

```http
POST /authoring/testing/template/render/destination
```

Pour illustrer le comportement de ce point d’entrée de l’API, prenons une destination basée sur un fichier avec la configuration des champs de données client suivante :

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**Requête**

La requête ci-dessous appelle le point d’entrée `/authoring/testing/template/render`, qui renvoie une réponse avec des valeurs générées de manière aléatoire pour les deux champs de données client mentionnés ci-dessus.

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| Paramètres | Description |
| -------- | ----------- |
| `destinationId` | Identifiant de la [configuration de destination](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) que vous testez. |
| `templates` | Noms de champs modélisés définis dans votre [configuration de serveur de destination](../../authoring-api/destination-server/create-destination-server.md). |

**Réponse**

Une réponse réussie renvoie un statut `HTTP 200 OK` et le corps comprend des valeurs générées de manière aléatoire pour vos champs modélisés.

Cette réponse peut vous aider à valider la structure sémantique des champs de vos données client, tels que les noms de compartiment ou les chemins d’accès au dossier.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment valider la configuration des champs de données client définie dans votre [serveur de destination](../../authoring-api/destination-server/create-destination-server.md).
