---
description: Cette page explique comment utiliser le point de terminaison /authoring/testing/template/render pour visualiser à quoi ressembleraient les champs de données clients modélisés définis dans votre configuration de destination.
title: Validation des champs de client modélisés
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 20%

---

# Validation des champs de client modélisés

## Présentation {#overview}

Le `/authoring/testing/template/render` endpoint vous aide à visualiser la manière dont le modèle est [Champs de données client](file-based-destination-configuration.md#customer-data-fields) défini dans votre configuration de destination ressemblerait à ce qui suit.

Le point de terminaison génère des valeurs aléatoires pour vos champs de données client et les renvoie dans la réponse. Vous pouvez ainsi valider la structure sémantique des champs de données client, tels que les noms de compartiment ou les chemins d’accès aux dossiers.

## Prise en main {#getting-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Conditions préalables {#prerequisites}

Avant d’utiliser la variable `/template/render` endpoint, assurez-vous de respecter les conditions suivantes :

* Une destination basée sur des fichiers existante est créée via la Destination SDK et vous pouvez la voir dans votre [destinations](../ui/destinations-workspace.md).
* Pour réussir la requête API, vous avez besoin de l’ID d’instance de destination correspondant à l’instance de destination que vous allez tester. Obtenez l’ID d’instance de destination que vous devez utiliser dans l’appel API, à partir de l’URL, lors de l’exploration d’une connexion avec votre destination dans l’interface utilisateur de Platform.

   ![Image de l’interface utilisateur montrant comment obtenir l’ID d’instance de destination à partir de l’URL.](assets/get-destination-instance-id.png)

## Rendu des champs client modélisés {#render-customer-fields}

**Format d’API**

```http
POST /authoring/testing/template/render/destination
```

Pour illustrer le comportement de ce point de terminaison API, considérons une destination basée sur un fichier avec la configuration des champs de données client suivante :

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

La requête ci-dessous appelle le `/authoring/testing/template/render` point de terminaison , qui renvoie une réponse avec des valeurs générées de manière aléatoire pour les deux champs de données client mentionnés ci-dessus.

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
| `destinationId` | L’identifiant de la variable [configuration de destination](file-based-destination-configuration.md) que vous testez. |
| `templates` | Les noms de champ sous forme de modèles définis dans votre [configuration du serveur de destination](server-and-file-configuration.md). |

**Réponse**

Une réponse réussie renvoie une `HTTP 200 OK` et le corps comprend des valeurs générées de manière aléatoire pour vos champs modélisés.

Cette réponse peut vous aider à valider la structure correcte des champs de données du client, tels que les noms des compartiments ou les chemins d’accès aux dossiers.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment valider la configuration des champs de données client définie dans votre [serveur de destination](server-and-file-configuration.md).
