---
keywords: Experience Platform;accueil;rubriques populaires;service de flux;mettre à jour les flux de données de destination
solution: Experience Platform
title: Mettre à jour des flux de données de destination à l’aide de l’API Flow Service
type: Tutorial
description: Ce tutoriel décrit les étapes de mise à jour d’un flux de données de destination. Découvrez comment activer ou désactiver le flux de données, mettre à jour ses informations de base ou ajouter et supprimer des segments et des attributs à l’aide de l’API Flow Service.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 40%

---

# Mettre à jour des flux de données de destination à l’aide de l’API Flow Service

Ce tutoriel décrit les étapes de mise à jour d’un flux de données de destination. Découvrez comment activer ou désactiver le flux de données, mettre à jour ses informations de base ou ajouter et supprimer des segments et des attributs à l’aide du [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Pour plus d’informations sur la modification des flux de données de destination à l’aide de l’interface utilisateur de l’Experience Platform, reportez-vous à la section [Modification des flux d’activation](/help/destinations/ui/edit-activation.md).

## Prise en main {#get-started}

Pour suivre ce tutoriel, vous devez disposer d’un identifiant de flux valide. Si vous ne disposez pas d’un identifiant de flux valide, sélectionnez votre destination de choix dans la [destinations](../catalog/overview.md) et suivez les étapes décrites à la section [se connecter à la destination](../ui/connect-destination.md) et [activer les données](../ui/activation-overview.md) avant de tester ce tutoriel.

>[!NOTE]
>
> Les termes *flow* et *dataflow* sont interchangeables dans ce tutoriel. Dans le contexte de ce tutoriel, ils ont le même sens.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Les destinations sont des intégrations préconfigurées à des plateformes de destination qui permettent dʼactiver facilement des données provenant dʼAdobe Experience Platform. ](../home.md)[!DNL Destinations] Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
* [Sandbox](../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour mettre à jour votre flux de données avec succès à l’aide de la variable [!DNL Flow Service] API.

### Lecture d’exemples d’appels API {#reading-sample-api-calls}

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis {#gather-values-for-required-headers}

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources de l’Experience Platform, y compris celles appartenant à [!DNL Flow Service], sont isolés dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si la variable `x-sandbox-name` n’est pas spécifié, les requêtes sont résolues sous `prod` sandbox.

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Rechercher des détails du flux de données {#look-up-dataflow-details}

La première étape de la mise à jour de votre flux de données de destination consiste à récupérer les détails du flux à l’aide de votre identifiant de flux. Vous pouvez afficher les détails actuels d’un flux de données existant en adressant une requête GET au point d’entrée `/flows`.

**Format d’API**

```http
GET /flows/{FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | L’unique `id` pour le flux de données de destination que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère des informations concernant votre ID de flux.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails actuels de votre flux de données, y compris sa version et son identifiant unique (`id`) et d’autres informations pertinentes.

```json
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## Mise à jour du nom et de la description du flux de données {#update-dataflow}

Pour mettre à jour le nom et la description de votre flux de données, envoyez une requête de PATCH au [!DNL Flow Service] de l’API tout en fournissant votre ID de flux, votre version et les nouvelles valeurs que vous souhaitez utiliser.

>[!IMPORTANT]
>
>L’en-tête `If-Match` est requis lors de l’exécution d’une requête PATCH. La valeur de cet en-tête est la version unique du flux de données que vous souhaitez mettre à jour. La valeur de la balise dʼentité est mise à jour à chaque mise à jour réussie d’un flux de données.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

La requête suivante met à jour le nom et la description de votre flux de données.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Définit la partie du flux à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en y indiquant votre identifiant de flux.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Activation ou désactivation du flux de données {#enable-disable-dataflow}

Lorsqu’il est activé, un flux de données exporte les profils vers la destination. Les flux de données sont activés par défaut, mais peuvent être désactivés pour suspendre les exportations de profils.

Vous pouvez activer ou désactiver un flux de données de destination existant en adressant une requête de POST au [!DNL Flow Service] API et indiquer l’état vers lequel vous souhaitez mettre à jour le flux.

**Format d’API**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**Requête**

La requête suivante met à jour l’état de votre flux de données pour qu’il soit activé.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

La requête suivante met à jour l’état de votre flux de données pour qu’il soit désactivé.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en y indiquant votre identifiant de flux.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Ajout d’un segment à un flux de données {#add-segment}

Pour ajouter un segment au flux de données de destination, effectuez une requête de PATCH au [!DNL Flow Service] API lors de la fourniture de votre ID de flux, de votre version et du segment que vous souhaitez ajouter.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

La requête suivante ajoute un nouveau segment à un flux de données de destination existant.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "triggerType": "AFTER_SEGMENT_EVAL",
               "endDate":"2022-03-10"
            }
         }
      }
   }
]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. Pour ajouter un segment à un flux de données, utilisez l’opération `add`. |
| `path` | Définit la partie du flux à mettre à jour. Lors de l’ajout d’un segment à un flux de données, utilisez le chemin spécifié dans l’exemple. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |
| `id` | Indiquez l’identifiant du segment que vous ajoutez au flux de données de destination. |
| `name` | **(Facultatif)**. Indiquez le nom du segment que vous ajoutez au flux de données de destination. Notez que ce champ n’est pas obligatoire et que vous pouvez ajouter un segment au flux de données de destination sans indiquer son nom. |
| `filenameTemplate` | Pour *destinations par lot* uniquement. Ce champ est obligatoire uniquement lors de l’ajout d’un segment à un flux de données dans des destinations d’exportation de fichiers par lots telles qu’Amazon S3, SFTP ou Azure Blob. <br> Ce champ détermine le format du nom des fichiers exportés vers votre destination. <br>Les options suivantes sont disponibles :<br> <ul><li>`%DESTINATION_NAME%` : obligatoire. Les fichiers exportés contiennent le nom de destination.</li><li>`%SEGMENT_ID%` : obligatoire. Les fichiers exportés contiennent l’identifiant du segment exporté.</li><li>`%SEGMENT_NAME%`: **(Facultatif)**. Les fichiers exportés contiennent le nom du segment exporté.</li><li>`DATETIME(YYYYMMdd_HHmmss)` ou `%TIMESTAMP%`: **(Facultatif)**. Sélectionnez l’une de ces deux options pour que vos fichiers incluent l’heure à laquelle ils sont générés par Experience Platform.</li><li>`custom-text`: **(Facultatif)**. Remplacez cet espace réservé par tout texte personnalisé que vous souhaitez ajouter à la fin de vos noms de fichier.</li></ul> <br> Pour plus d’informations sur la configuration des noms de fichier, reportez-vous à la section [Configurer des noms de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) dans le tutoriel consacré à l’activation des destinations par lot. |
| `exportMode` | Pour *destinations par lot* uniquement. Ce champ est obligatoire uniquement lors de l’ajout d’un segment à un flux de données dans des destinations d’exportation de fichiers par lots telles qu’Amazon S3, SFTP ou Azure Blob. <br> Obligatoire. Sélectionnez `"DAILY_FULL_EXPORT"` ou `"FIRST_FULL_THEN_INCREMENTAL"`. Pour plus d’informations sur les deux options, reportez-vous aux sections [Exporter des fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) et [Exporter des fichiers incrémentiels](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) dans le tutoriel consacré à l’activation des destinations par lot. |
| `startDate` | Sélectionnez la date à laquelle le segment doit commencer à exporter les profils vers votre destination. |
| `frequency` | Pour *destinations par lot* uniquement. Ce champ est obligatoire uniquement lors de l’ajout d’un segment à un flux de données dans des destinations d’exportation de fichiers par lots telles qu’Amazon S3, SFTP ou Azure Blob. <br> Obligatoire. <br> <ul><li>Pour le mode d’exportation `"DAILY_FULL_EXPORT"`, vous pouvez sélectionner `ONCE` ou `DAILY`.</li><li>Pour le mode d’exportation `"FIRST_FULL_THEN_INCREMENTAL"`, vous pouvez sélectionner `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"` ou `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | Pour *destinations par lot* uniquement. Ce champ est obligatoire uniquement lors de la sélection de la variable `"DAILY_FULL_EXPORT"` dans le `frequency` sélecteur. <br> Obligatoire. <br> <ul><li>Sélectionner `"AFTER_SEGMENT_EVAL"` pour que la tâche d’activation s’exécute immédiatement une fois la tâche de segmentation par lots quotidienne de Platform terminée. Ainsi, lorsque la tâche d’activation s’exécute, les profils les plus récents sont exportés vers votre destination.</li><li>Sélectionner `"SCHEDULED"` pour que la tâche d’activation s’exécute à un moment donné. Cela permet de garantir que les données de profil Experience Platform sont exportées simultanément chaque jour, mais les profils que vous exportez peuvent ne pas être les plus à jour, selon que la tâche de segmentation par lots est terminée ou non avant le début de la tâche d’activation. Lorsque vous sélectionnez cette option, vous devez également ajouter une `startTime` pour indiquer à quel moment en UTC les exportations quotidiennes doivent avoir lieu.</li></ul> |
| `endDate` | Pour *destinations par lot* uniquement. Ce champ est obligatoire uniquement lors de l’ajout d’un segment à un flux de données dans des destinations d’exportation de fichiers par lots telles qu’Amazon S3, SFTP ou Azure Blob. <br> Non applicable lors de la sélection de `"exportMode":"DAILY_FULL_EXPORT"` et `"frequency":"ONCE"`. <br> Définit la date à laquelle les membres du segment cessent d’être exportés vers la destination. |
| `startTime` | Pour *destinations par lot* uniquement. Ce champ est obligatoire uniquement lors de l’ajout d’un segment à un flux de données dans des destinations d’exportation de fichiers par lots telles qu’Amazon S3, SFTP ou Azure Blob. <br> Obligatoire. Sélectionnez l’heure à laquelle les fichiers contenant des membres du segment doivent être générés et exportés vers votre destination. |

**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en y indiquant votre identifiant de flux.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Suppression d’un segment d’un flux de données {#remove-segment}

Pour supprimer un segment d’un flux de données de destination existant, effectuez une requête de PATCH à la fonction [!DNL Flow Service] API lors de la fourniture de l’ID de flux, de la version et du sélecteur d’index du segment que vous souhaitez supprimer. L’indexation commence à `0`. Par exemple, l’exemple de requête ci-dessous supprime les premier et deuxième segments du flux de données.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

La requête suivante supprime deux segments d’un flux de données de destination existant.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/0/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/1/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. Pour supprimer un segment d’un flux de données, utilisez la méthode `remove` opération. |
| `path` | Indique quel segment existant doit être supprimé du flux de données de destination, en fonction de l’index du sélecteur de segments. Pour récupérer l’ordre des segments dans un flux de données, effectuez un appel GET à la fonction `/flows` et inspecter le `transformations.segmentSelectors` . Pour supprimer le premier segment dans le flux de données, utilisez `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en y indiquant votre identifiant de flux.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Mise à jour de composants d’un segment dans un flux de données {#update-segment}

Vous pouvez mettre à jour les composants d’un segment dans un flux de données de destination existant. Par exemple, vous pouvez modifier la fréquence d’exportation ou modifier le modèle de nom de fichier. Pour ce faire, envoyez une requête de PATCH au [!DNL Flow Service] API lors de la fourniture de l’ID de flux, de la version et du sélecteur d’index du segment que vous souhaitez mettre à jour. L’indexation commence à `0`. Par exemple, la requête ci-dessous met à jour le neuvième segment dans un flux de données.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

Lors de la mise à jour d’un segment dans un flux de données de destination existant, vous devez d’abord effectuer une opération de GET pour récupérer les détails du segment que vous souhaitez mettre à jour. Indiquez ensuite toutes les informations sur les segments dans la payload, et pas seulement les champs que vous souhaitez mettre à jour. Dans l&#39;exemple ci-dessous, du texte personnalisé est ajouté à la fin du modèle de nom de fichier et la fréquence du planning d&#39;export est mise à jour de 6 heures à 12 heures.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

Pour obtenir des descriptions des propriétés de la payload, reportez-vous à la section . [Ajout d’un segment à un flux de données](#add-segment).


**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en y indiquant votre identifiant de flux.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Consultez les exemples ci-dessous pour plus d’exemples de composants de segment que vous pouvez mettre à jour dans un flux de données.

## Mettre à jour le mode d’exportation d’un segment d’une évaluation planifiée à une évaluation de segment {#update-export-mode}

+++ Cliquez pour voir un exemple dans lequel une exportation de segments est mise à jour : elle n’est plus activée tous les jours à une heure donnée, mais elle est activée tous les jours une fois la tâche de segmentation par lots Platform terminée.

Le segment est exporté tous les jours à 16h00 UTC.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

Le segment est exporté tous les jours à la fin de la tâche de segmentation par lots quotidienne.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "AFTER_SEGMENT_EVAL",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Mettre à jour le modèle de nom de fichier pour inclure des champs supplémentaires dans le nom de fichier {#update-filename-template}

+++ Cliquez pour afficher un exemple de mise à jour du modèle de nom de fichier afin d’inclure des champs supplémentaires dans le nom de fichier.

Les fichiers exportés contiennent le nom de destination et l’identifiant de segment Experience Platform.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

Les fichiers exportés contiennent le nom de destination, l’identifiant du segment Experience Platform, la date et l’heure de génération du fichier par l’Experience Platform et le texte personnalisé ajouté à la fin des fichiers.


```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_%this is custom text%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Ajout d’un attribut de profil à un flux de données {#add-profile-attribute}

Pour ajouter un attribut de profil au flux de données de destination, effectuez une requête de PATCH au [!DNL Flow Service] API lors de la fourniture de votre ID de flux, de votre version et de l’attribut de profil que vous souhaitez ajouter.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

La requête suivante ajoute un nouvel attribut de profil à un flux de données de destination existant.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. Pour ajouter un attribut de profil à un flux de données, utilisez la variable `add` opération. |
| `path` | Définit la partie du flux à mettre à jour. Lors de l’ajout d’un attribut de profil à un flux de données, utilisez le chemin spécifié dans l’exemple. |
| `value.path` | La valeur de l’attribut de profil que vous ajoutez au flux de données. |

**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en y indiquant votre identifiant de flux.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Suppression d’un attribut de profil d’un flux de données {#remove-profile-attribute}

Pour supprimer un attribut de profil d’un flux de données de destination existant, effectuez une requête de PATCH au [!DNL Flow Service] API lors de la fourniture de l’ID de flux, de la version et du sélecteur d’index de l’attribut de profil que vous souhaitez supprimer. L’indexation commence à `0`. Par exemple, l’exemple de requête ci-dessous supprime le cinquième attribut de profil du flux de données.


**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

La requête suivante supprime un attribut de profil d’un flux de données de destination existant.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. Pour supprimer un segment d’un flux de données, utilisez la méthode `remove` opération. |
| `path` | Indique quel attribut de profil existant doit être supprimé du flux de données de destination, en fonction de l’index du sélecteur de segments. Pour récupérer l’ordre des attributs de profil dans un flux de données, effectuez un appel GET à la fonction `/flows` et inspecter le `transformations.profileSelectors` . Pour supprimer le premier segment dans le flux de données, utilisez `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en y indiquant votre identifiant de flux.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Gestion des erreurs d’API {#api-error-handling}

Les points de terminaison d’API de ce tutoriel suivent les principes généraux des messages d’erreur de l’API Experience Platform. Voir [Codes d’état d’API](/help/landing/troubleshooting.md#api-status-codes) et [erreurs d’en-tête de requête](/help/landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform pour plus d’informations sur l’interprétation des réponses d’erreur.

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez appris à mettre à jour différents composants d’un flux de données de destination, comme ajouter ou supprimer des segments ou des attributs de profil à l’aide de [!DNL Flow Service] API. Pour plus d’informations sur les destinations, voir [présentation des destinations](../home.md).
