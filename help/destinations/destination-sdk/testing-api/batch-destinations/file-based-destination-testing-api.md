---
description: Cette page explique comment utiliser le point d’entrée /testing/destinationInstance de l’API pour tester si la destination basée sur des fichiers est configurée correctement et pour vérifier l’intégrité des flux de données vers la destination configurée.
title: Test de la destination basée sur des fichiers avec des profils types
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: 9ac6b075af3805da4dad0dd6442d026ae96ab5c7
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 100%

---

# Test de la destination basée sur des fichiers avec des profils types

## Vue d’ensemble {#overview}

Cette page explique comment utiliser le point d’entrée `/testing/destinationInstance` de l’API pour tester si la destination basée sur des fichiers est configurée correctement et pour vérifier l’intégrité des flux de données vers la destination configurée.

Vous pouvez envoyer des requêtes au point d’entrée de test avec ou sans ajouter de [profils types](file-based-sample-profile-generation-api.md) à l’appel. Si vous n’envoyez aucun profil à la requête, l’API génère automatiquement un profil type et l’ajoute à la requête.

Les profils types générés automatiquement contiennent des données génériques. Si vous souhaitez tester la destination avec des données de profil personnalisées et plus intuitives, utilisez l’[API de génération de profil type](file-based-sample-profile-generation-api.md) pour générer un profil type, puis personnalisez la réponse et incluez-la dans la requête au point d’entrée `/testing/destinationInstance`.

## Prise en main {#getting-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Conditions préalables {#prerequisites}

Avant d’utiliser le point d’entrée `/testing/destinationInstance`, veillez à respecter les conditions suivantes :

* Une destination existante basée sur des fichiers a été créée avec Destination SDK et vous pouvez la voir dans votre [catalogue de destination](../../../ui/destinations-workspace.md).
* Au moins un flux d’activation pour la destination dans l’interface utilisateur d’Experience Platform a été créé.
* Pour réussir la requête API, vous avez besoin de l’identifiant d’instance de destination correspondant à l’instance de destination que vous allez tester. Obtenez l’identifiant d’instance de destination que vous devez utiliser dans l’appel API, à partir de l’URL, pendant l’exploration d’une connexion avec la destination dans l’interface utilisateur de Platform.

  ![Image de l’interface utilisateur montrant comment obtenir l’identifiant d’instance de destination à partir de l’URL.](../../assets/testing-api/get-destination-instance-id.png)
* *Facultatif* : si vous souhaitez tester la configuration de destination avec un profil type ajouté à l’appel API, utilisez le point d’entrée [/sample-profiles](file-based-sample-profile-generation-api.md) pour générer un profil type en fonction de votre schéma source existant. Si vous ne fournissez pas de profil type, l’API en génère un et le renvoie dans la réponse.

## Test de la configuration de la destination sans ajout de profils à l’appel {#test-without-adding-profiles}

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
| `{DESTINATION_INSTANCE_ID}` | L’identifiant de l’instance de destination pour laquelle vous générez des profils types. Pour en savoir plus sur la manière d’obtenir cet identifiant, consultez la section [Conditions préalables](#prerequisites). |

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec la payload de la réponse.

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
| `activations` | Renvoie l’identifiant de l’audience et l’identifiant de l’exécution du flux pour chaque audience activée. Le nombre d’entrées d’activation (et de fichiers générés associés) est égal au nombre d’audiences mappées sur l’instance de destination. <br><br> Exemple : si vous avez mappé deux audiences sur l’instance de destination, le tableau `activations` contient deux entrées. Chaque audience activée correspond à un fichier exporté. |
| `results` | Renvoie l’identifiant de l’instance de destination et les identifiants d’exécution de flux que vous pouvez utiliser pour appeler l’[API des résultats](file-based-destination-results-api.md) pour tester davantage l’intégration. |
| `inputProfiles` | Renvoie les profils types générés automatiquement par l’API. |

{style="table-layout:auto"}

## Test de la configuration de la destination avec ajout de profils à l’appel {#test-with-added-profiles}

Pour tester la destination avec des données de profil personnalisées et plus intuitives, vous pouvez personnaliser la réponse obtenue à partir du point d’entrée [/sample-profiles](file-based-sample-profile-generation-api.md) avec les valeurs de votre choix et inclure le profil personnalisé dans la requête au point d’entrée `/testing/destinationInstance`.

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
| `{DESTINATION_INSTANCE_ID}` | Identifiant d’instance de destination de la destination que vous testez.  L’identifiant de l’instance de destination pour laquelle vous générez des profils types. Pour en savoir plus sur la manière d’obtenir cet identifiant, consultez la section [Conditions préalables](#prerequisites). |
| `profiles` | Tableau pouvant inclure un ou plusieurs profils. Utilisez le [point d’entrée de l’API de profil type](file-based-sample-profile-generation-api.md) pour générer des profils à utiliser dans cet appel API. |

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec la payload de la réponse.

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
| `activations` | Renvoie l’identifiant de l’audience et l’identifiant de l’exécution du flux pour chaque audience activée. Le nombre d’entrées d’activation (et de fichiers générés associés) est égal au nombre d’audiences mappées sur l’instance de destination. <br><br> Exemple : si vous avez mappé deux audiences sur l’instance de destination, le tableau `activations` contient deux entrées. Chaque audience activée correspond à un fichier exporté. |
| `results` | Renvoie l’identifiant de l’instance de destination et les identifiants d’exécution de flux que vous pouvez utiliser pour appeler l’[API des résultats](file-based-destination-results-api.md) pour tester davantage l’intégration. |
| `inputProfiles` | Renvoie les profils types personnalisés que vous avez transmis dans la requête API. |

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment tester votre configuration de destination basée sur des fichiers.

Si vous avez déjà reçu une réponse API valide, la destination fonctionne correctement. Si vous souhaitez obtenir des informations plus détaillées sur votre flux d’activation, vous pouvez utiliser la `results`propriété de la réponse pour [voir les résultats d’activation détaillés](file-based-destination-results-api.md).

Si vous créez une destination publique, vous pouvez désormais [envoyer votre configuration de destination](../../guides/submit-destination.md) à Adobe pour révision.
