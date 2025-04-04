---
description: Cette page explique comment utiliser le point d’entrée /testing/destinationInstance de l’API pour afficher les détails complets de vos résultats de test. Ce point d’entrée de l’API renvoie le même résultat que celui obtenu pendant l’utilisation de l’API Flow Service pour surveiller les flux de données.
title: Consulter les résultats détaillés de l’activation
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 92%

---

# Consulter les résultats détaillés de l’activation {#view-test-results}

## Vue d’ensemble {#overview}

Cette page explique comment utiliser le point d’entrée `/testing/destinationInstance` de l’API pour afficher les détails complets de vos résultats de tests des destinations basés sur des fichiers.

Si vous avez déjà [testé la destination](file-based-destination-testing-api.md) et reçu une réponse API valide, la destination fonctionne correctement.

Si vous souhaitez obtenir des informations plus détaillées sur votre flux d’activation, vous pouvez utiliser la propriété `results` de la réponse de point d’entrée du [test de destination](file-based-destination-testing-api.md), comme décrit plus en détail ci-après.

>[!NOTE]
>
>Ce point d’entrée de l’API renvoie le même résultat que celui obtenu lors de l’utilisation de l’[API Flow Service](../../../api/update-destination-dataflows.md) pour surveiller les flux de données.

## Prise en main {#getting-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Conditions préalables {#prerequisites}

Avant d’utiliser le point d’entrée `/testing/destinationInstance`, veillez à respecter les conditions suivantes :

* Une destination existante basée sur des fichiers a été créée avec Destination SDK et vous pouvez la voir dans votre [catalogue de destination](../../../ui/destinations-workspace.md).
* Au moins un flux d’activation pour la destination dans l’interface utilisateur d’Experience Platform a été créé.
* Pour réussir la requête API, vous avez besoin de l’identifiant d’instance de destination correspondant à l’instance de destination que vous allez tester. Obtenez l’identifiant d’instance de destination que vous devez utiliser dans l’appel API, à partir de l’URL, lorsque vous parcourez une connexion avec la destination dans l’interface utilisateur d’Experience Platform.

  ![Image de l’interface utilisateur montrant comment obtenir l’identifiant d’instance de destination à partir de l’URL.](../../assets/testing-api/get-destination-instance-id.png)
* Vous avez précédemment [testé votre configuration de destination](file-based-destination-testing-api.md) et reçu une réponse API valide comprenant une propriété `results`. Vous utiliserez cette valeur `results` pour tester davantage la destination.

## Affichage des résultats détaillés du test de destination {#test-activation-results}

Une fois que vous avez [validé votre configuration de destination](file-based-destination-testing-api.md), vous pouvez afficher les résultats détaillés de l’activation en envoyant une requête GET au point d’entrée `authoring/testing/destinationInstance/` et en fournissant l’identifiant de l’instance de destination que vous testez, ainsi que les identifiants d’exécution de flux des audiences activées.

Vous trouverez l’URL complète d’API que vous devez utiliser dans la propriété `results` renvoyée dans la [réponse de l’appel de test de destination](file-based-destination-testing-api.md).

**Format d’API**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| Paramètres de chemin | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L’identifiant de l’instance de destination pour laquelle vous générez des profils types. Pour en savoir plus sur la manière d’obtenir cet identifiant, consultez la section [Conditions préalables](#prerequisites). |

| Paramètres de chaîne de requête | Description |
| -------- | ----------- |
| `flowRunIds` | Les identifiants d’exécution de flux correspondant aux audiences activées. Vous trouverez les identifiants d’exécution de flux dans la propriété `results` renvoyée dans la [réponse de l’appel de test de destination](file-based-destination-testing-api.md). |

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

La réponse contient les détails complets du flux d’activation. Vous pouvez obtenir la même réponse en appelant la fonction [API Flow Service](../../../api/update-destination-dataflows.md) pour surveiller les flux de données.

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

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment tester votre configuration de destination basée sur des fichiers et voir les détails complets de vos résultats d’activation.

Si vous créez une destination publique, vous pouvez désormais [envoyer votre configuration de destination](../../guides/submit-destination.md) à Adobe pour révision.
