---
description: Cette page explique comment utiliser le point d’entrée de l’API /testing/destinationInstance pour tester si votre destination basée sur des fichiers est configurée correctement et pour vérifier l’intégrité des flux de données vers votre destination configurée.
title: Testez votre destination basée sur des fichiers avec des exemples de profils
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 12%

---

# Testez votre destination basée sur des fichiers avec des exemples de profils

## Présentation {#overview}

Cette page explique comment utiliser la variable `/testing/destinationInstance` Point de terminaison d’API pour tester si votre destination basée sur des fichiers est configurée correctement et pour vérifier l’intégrité des flux de données vers votre destination configurée.

Vous pouvez envoyer des requêtes au point de terminaison de test avec ou sans ajouter [exemples de profils](file-based-sample-profile-generation-api.md) à l’appel . Si vous n’envoyez aucun profil à la requête, l’API génère automatiquement un exemple de profil et l’ajoute à la requête.

Les exemples de profils générés automatiquement contiennent des données génériques. Si vous souhaitez tester votre destination avec des données de profil personnalisées et plus intuitives, utilisez la variable [exemple d’API de génération de profil](file-based-sample-profile-generation-api.md) pour générer un exemple de profil, personnalisez sa réponse et incluez-la dans la requête au `/testing/destinationInstance` point de terminaison .

## Prise en main {#getting-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Conditions préalables {#prerequisites}

Avant d’utiliser la variable `/testing/destinationInstance` endpoint, assurez-vous de respecter les conditions suivantes :

* Une destination basée sur des fichiers existante est créée via la Destination SDK et vous pouvez la voir dans votre [destinations](../../../ui/destinations-workspace.md).
* Vous avez créé au moins un flux d’activation pour votre destination dans l’interface utilisateur de l’Experience Platform.
* Pour réussir la requête API, vous avez besoin de l’ID d’instance de destination correspondant à l’instance de destination que vous allez tester. Obtenez l’ID d’instance de destination que vous devez utiliser dans l’appel API, à partir de l’URL, lors de l’exploration d’une connexion avec votre destination dans l’interface utilisateur de Platform.

   ![Image de l’interface utilisateur montrant comment obtenir l’ID d’instance de destination à partir de l’URL.](../../assets/testing-api/get-destination-instance-id.png)
* *Facultatif*: Si vous souhaitez tester votre configuration de destination avec un exemple de profil ajouté à l’appel API, utilisez la variable [/sample-profiles](file-based-sample-profile-generation-api.md) point d’entrée pour générer un exemple de profil en fonction de votre schéma source existant. Si vous ne fournissez pas d’exemple de profil, l’API en génère un et le renvoie dans la réponse.

## Tester la configuration de votre destination sans ajouter de profils à l’appel {#test-without-adding-profiles}

**Format d’API**

```http
POST /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Requête**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Paramètres de chemin | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L’identifiant de l’instance de destination pour laquelle vous générez des exemples de profils. Voir [conditions préalables](#prerequisites) pour plus d’informations sur la manière d’obtenir cet identifiant. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec la charge utile de la réponse.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"crmid-P1A7l"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string",
               "lastName":"string"
            }
         }
      }
   ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `activations` | Renvoie l’identifiant du segment et l’identifiant de l’exécution du flux pour chaque segment activé. Le nombre d’entrées d’activation (et de fichiers générés associés) est égal au nombre de segments mappés sur l’instance de destination. <br><br> Exemple : Si vous avez mappé deux segments à l’instance de destination, la variable `activations` contient deux entrées. Chaque segment activé correspond à un fichier exporté. |
| `results` | Renvoie l’identifiant de l’instance de destination et les identifiants d’exécution de flux que vous pouvez utiliser pour appeler la variable [API des résultats](file-based-destination-results-api.md), pour tester davantage l’intégration. |
| `inputProfiles` | Renvoie les exemples de profils générés automatiquement par l’API. |

{style="table-layout:auto"}

## Tester la configuration de votre destination avec les profils ajoutés à l’appel {#test-with-added-profiles}

Pour tester votre destination avec des données de profil personnalisées et plus intuitives, vous pouvez personnaliser la réponse obtenue à partir de la variable [/sample-profiles](file-based-sample-profile-generation-api.md) point de terminaison avec les valeurs de votre choix et incluez le profil personnalisé dans la requête au `/testing/destinationInstance` point de terminaison .

**Format d’API**

```http
POST  /testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Requête**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' 
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}'
```

| Paramètre | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L’ID d’instance de destination de la destination que vous testez.  L’identifiant de l’instance de destination pour laquelle vous générez des exemples de profils. Voir [conditions préalables](#prerequisites) pour plus d’informations sur la manière d’obtenir cet identifiant. |
| `profiles` | Tableau pouvant inclure un ou plusieurs profils. Utilisez la variable [exemple de point d’entrée de l’API de profil](file-based-sample-profile-generation-api.md) pour générer des profils à utiliser dans cet appel API. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec la charge utile de la réponse.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `activations` | Renvoie l’identifiant du segment et l’identifiant de l’exécution du flux pour chaque segment activé. Le nombre d’entrées d’activation (et de fichiers générés associés) est égal au nombre de segments mappés sur l’instance de destination. <br><br> Exemple : Si vous avez mappé deux segments à l’instance de destination, la variable `activations` contient deux entrées. Chaque segment activé correspond à un fichier exporté. |
| `results` | Renvoie l’identifiant de l’instance de destination et les identifiants d’exécution de flux que vous pouvez utiliser pour appeler la variable [API des résultats](file-based-destination-results-api.md), pour tester davantage l’intégration. |
| `inputProfiles` | Renvoie les exemples de profils personnalisés que vous avez transmis dans la requête API. |

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment tester votre configuration de destination basée sur des fichiers.

Si vous avez reçu une réponse API valide, votre destination fonctionne correctement. Si vous souhaitez obtenir des informations plus détaillées sur votre flux d’activation, vous pouvez utiliser la variable `results` de la réponse à [afficher les résultats détaillés de l’activation](file-based-destination-results-api.md).

Si vous créez une destination publique, vous pouvez désormais [envoyer votre configuration de destination ;](../../guides/submit-destination.md) à Adobe pour révision.
