---
description: Cette page explique comment utiliser le point d’entrée de l’API /testing/destinationInstance pour afficher les détails complets de vos résultats de test. Ce point de terminaison API renvoie le même résultat que celui obtenu lors de l’utilisation de l’API Flow Service pour surveiller les flux de données.
title: Affichage des résultats détaillés de l’activation
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 15%

---

# Affichage des résultats détaillés de l’activation {#view-test-results}

## Présentation {#overview}

Cette page explique comment utiliser la variable `/testing/destinationInstance` Point de terminaison d’API pour afficher les détails complets de vos résultats de test de destination basés sur des fichiers.

Si vous avez déjà [a testé votre destination](file-based-destination-testing-api.md) et a reçu une réponse API valide, votre destination fonctionne correctement.

Si vous souhaitez obtenir des informations plus détaillées sur votre flux d’activation, vous pouvez utiliser la variable `results` de la propriété [test de destination](file-based-destination-testing-api.md) réponse du point de terminaison, comme décrit plus loin ci-dessous.

>[!NOTE]
>
>Ce point de terminaison API renvoie le même résultat que vous obtiendriez lors de l’utilisation de la variable [API de service de flux](../api/update-destination-dataflows.md) pour surveiller les flux de données.

## Prise en main {#getting-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Conditions préalables {#prerequisites}

Avant d’utiliser la variable `/testing/destinationInstance` endpoint, assurez-vous de respecter les conditions suivantes :

* Une destination basée sur des fichiers existante est créée via la Destination SDK et vous pouvez la voir dans votre [destinations](../ui/destinations-workspace.md).
* Vous avez créé au moins un flux d’activation pour votre destination dans l’interface utilisateur de l’Experience Platform.
* Pour réussir la requête API, vous avez besoin de l’ID d’instance de destination correspondant à l’instance de destination que vous allez tester. Obtenez l’ID d’instance de destination que vous devez utiliser dans l’appel API, à partir de l’URL, lors de l’exploration d’une connexion avec votre destination dans l’interface utilisateur de Platform.

   ![Image de l’interface utilisateur montrant comment obtenir l’ID d’instance de destination à partir de l’URL.](assets/get-destination-instance-id.png)
* Vous avez précédemment [a testé votre configuration de destination](file-based-destination-testing-api.md)et a reçu une réponse API valide comprenant un `results` . Vous utiliserez ceci : `results` pour tester davantage votre destination.

## Affichage des résultats détaillés du test de destination {#test-activation-results}

Une fois que vous avez [a validé votre configuration de destination](file-based-destination-testing-api.md), vous pouvez afficher les résultats détaillés de l’activation en envoyant une requête de GET au `authoring/testing/destinationInstance/` point de terminaison et en fournissant l’identifiant de l’instance de destination que vous testez, ainsi que les identifiants d’exécution de flux des segments activés.

Vous trouverez l’URL complète d’API que vous devez utiliser dans la variable `results` renvoyée dans la propriété [réponse de l’appel de test de destination](file-based-destination-testing-api.md).

**Format d’API**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| Paramètres de chemin | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L’identifiant de l’instance de destination pour laquelle vous générez des exemples de profils. Voir [conditions préalables](#prerequisites) pour plus d’informations sur la manière d’obtenir cet identifiant. |

| Paramètres de chaîne de requête | Description |
| -------- | ----------- |
| `flowRunIds` | Les identifiants d’exécution de flux correspondant aux segments activés. Vous trouverez les ID d’exécution de flux dans la variable `results` renvoyée dans la propriété [réponse de l’appel de test de destination](file-based-destination-testing-api.md). |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=30d34875-e7ba-4520-ab6e-5705e01dfb16,86c00ad7-443c-459a-855d-0e8cbee43c4f,12305c58-42a9-4230-8fad-1661ee49cb70' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse contient les détails complets du flux d’activation. Vous pouvez obtenir la même réponse en appelant la fonction [API de service de flux](../api/update-destination-dataflows.md) pour surveiller les flux de données.

```json
{
   "items":[
      {
         "id":"18efd5d2-40ae-4f5c-afd1-37a39a45183a",
         "flowId":"a02071ad-f3a4-496c-a2b1-468812301d5d",
         "flowSpec":{
            "id":"25473b67-0801-418a-ab49-ed74ebf88137",
            "version":"1.0"
         },
         "metrics":{
            "durationSummary":{
               "startedAtUTC":1646652235124,
               "completedAtUTC":1646652270439
            },
            "latencySummary":null,
            "sizeSummary":{
               "inputBytes":122,
               "outputBytes":122
            },
            "recordSummary":{
               "inputRecordCount":1,
               "outputRecordCount":1,
               "createdRecordCount":1,
               "skippedRecordCount":0,
               "sourceSummaries":[
                  {
                     "id":"76e4b969-9700-4557-8330-0a8390afbdde",
                     "entitySummaries":[
                        {
                           "inputRecordCount":1,
                           "skippedRecordCount":0,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ],
               "targetSummaries":[
                  {
                     "id":"b43607b6-0dca-43b3-a0bc-ecdea4fa6aa9",
                     "entitySummaries":[
                        {
                           "outputRecordCount":1,
                           "createdRecordCount":1,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ]
            },
            "fileSummary":{
               "inputFileCount":1,
               "outputFileCount":1
            },
            "statusSummary":{
               "status":"success"
            }
         },
         "activities":[
            {
               "id":"c4f238e3-7334-4933-8b56-64d7ea43ea54",
               "name":"Activation Batch XdmProcessor Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652235124,
                  "completedAtUTC":1646652255157
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "inputBytes":122,
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "inputFileCount":1,
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     "incremental.batchId":"",
                     "snapshot.batchId":"",
                     "snapshot.datasetId":"",
                     "incremental.datasetId":""
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            },
            {
               "id":"51d82b36-6b8f-11eb-9439-0242ac130002",
               "name":"Activation Batch Publisher Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652270326,
                  "completedAtUTC":1646652270439
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            }
         ],
         "predecessors":null
      }
   ],
   "_links":{
      
   }
}
```

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment tester votre configuration de destination basée sur des fichiers et voir les détails complets de vos résultats d’activation.

Si vous créez une destination publique, vous pouvez désormais [envoyer votre configuration de destination ;](../destination-sdk/submit-destination.md) à Adobe pour révision.
