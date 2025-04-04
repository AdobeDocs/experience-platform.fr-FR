---
keywords: Experience Platform;accueil;rubriques populaires; notifications
description: En vous abonnant à Adobe I/O Events, vous pouvez utiliser des Webhooks pour recevoir des notifications concernant les statuts d’exécution des flux de vos connexions source. Ces notifications contiennent des informations sur le succès de l’exécution de votre flux ou sur les erreurs qui ont contribué à l’échec d’une exécution.
solution: Experience Platform
title: Notifications d’exécution de flux
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 16%

---

# Notifications d’exécution de flux

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) est utilisé pour collecter et centraliser les données client provenant de diverses sources dans [!DNL Experience Platform]. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge peuvent être connectées.

Avec Adobe I/O Events, vous pouvez vous abonner à des événements et utiliser des Webhooks pour recevoir des notifications concernant le statut de vos exécutions de flux. Ces notifications contiennent des informations sur le succès de l’exécution de votre flux ou sur les erreurs qui ont contribué à l’échec d’une exécution.

Ce document décrit la procédure à suivre pour vous abonner à des événements, enregistrer des Webhooks et recevoir des notifications contenant des informations sur le statut de vos exécutions de flux.

## Commencer

Ce tutoriel suppose que vous avez déjà créé au moins une connexion source dont vous souhaitez surveiller l’exécution du flux. Si vous n’avez pas encore configuré de connexion source, commencez par consulter la [présentation des sources](./home.md) pour configurer la source de votre choix avant de revenir à ce guide.

Ce document nécessite également une compréhension pratique des Webhooks et de la connexion d’un webhook d’une application à une autre. Pour en savoir plus sur les Webhooks, consultez la [[!DNL I/O Events] documentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md).

## Enregistrer un webhook pour les notifications d’exécution de flux

Pour recevoir des notifications d’exécution de flux, vous devez utiliser Adobe Developer Console pour enregistrer un webhook auprès de votre intégration [!DNL Experience Platform].

Suivez le tutoriel sur [l’abonnement aux notifications [!DNL I/O Event]](../observability/alerts/subscribe.md) pour obtenir des instructions détaillées sur la manière d’y parvenir.

>[!IMPORTANT]
>
>Pendant le processus d’abonnement, veillez à sélectionner **[!UICONTROL Notifications Platform]** comme fournisseur d’événements, puis sélectionnez les abonnements aux événements suivants :
>
>* **[!UICONTROL Exécution Du Flux Experience Platform Source Réussie]**
>* **[!UICONTROL Échec De L’Exécution Du Flux Experience Platform Source]**

## Recevoir des notifications d’exécution de flux

Une fois votre webhook connecté et votre abonnement à l’événement terminé, vous pouvez commencer à recevoir des notifications d’exécution de flux via le tableau de bord webhook.

Une notification renvoie des informations telles que le nombre de traitements d’ingestion exécutés, la taille de fichier et les erreurs. Une notification renvoie également une payload associée à votre exécution de flux au format JSON. La payload de réponse peut être classée comme `sources_flow_run_success` ou `sources_flow_run_failure`.

>[!IMPORTANT]
>
>Si l’ingestion partielle est activée pendant le processus de création de flux, un flux qui contient à la fois des ingestions réussies et ayant échoué sera marqué comme `sources_flow_run_success` uniquement si le nombre d’erreurs est inférieur au pourcentage de seuil d’erreur défini pendant le processus de création de flux. Si une exécution de flux réussie contient des erreurs, celles-ci seront toujours incluses dans la payload renvoyée.

### Réussite

Une réponse réussie renvoie un ensemble de `metrics` qui définissent les caractéristiques d’une exécution de flux spécifique et des `activities` qui décrivent la manière dont les données sont transformées.

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{ORG_ID}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| Propriété | Description |
| -------- | ----------- |
| `metrics` | Définit les caractéristiques des données dans l’exécution du flux. |
| `activities` | Définit les différentes étapes et activités exécutées pour transformer les données. |
| `durationSummary` | Définit les heures de début et de fin de l’exécution du flux. |
| `sizeSummary` | Définit le volume des données en octets. |
| `recordSummary` | Définit le nombre d’enregistrements des données. |
| `fileSummary` | Définit le nombre de fichiers des données. |
| `fileInfo` | Une URL qui mène à un aperçu des fichiers ingérés avec succès. |
| `statusSummary` | Définit si l’exécution du flux est une réussite ou un échec. |

### Échec

La réponse suivante est un exemple d’exécution de flux ayant échoué, avec une erreur se produisant lors du traitement des données copiées. Des erreurs peuvent également se produire lors de la copie de données à partir de la source. Une exécution de flux en échec contient des informations sur les erreurs qui ont contribué à l’échec de l’exécution, y compris son erreur et sa description.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{ORG_ID}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{ORG_ID}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| Propriété | Description |
| ---------- | ----------- |
| `fileInfo` | Une URL qui mène à un aperçu des fichiers qui ont été ingérés avec succès et sans succès. |

>[!NOTE]
>
>Voir l’[annexe](#errors) pour plus d’informations sur les messages d’erreur.

## Étapes suivantes

Vous pouvez désormais vous abonner à des événements qui vous permettent de recevoir des notifications en temps réel sur les statuts d’exécution de vos flux. Pour plus d’informations sur les exécutions de flux et les sources, consultez la [ présentation des sources ](./home.md).

## Annexe

Les sections suivantes apportent des informations supplémentaires sur l’utilisation des notifications d’exécution de flux.

### Comprendre les messages d’erreur {#errors}

Des erreurs d’ingestion peuvent se produire lorsque les données sont copiées à partir de la source ou lorsque les données copiées sont en cours de traitement vers [!DNL Experience Platform]. Pour plus d’informations sur des erreurs spécifiques, consultez le tableau ci-dessous .

| Erreur | Description |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Une erreur s’est produite lors de la copie des données à partir d’une source. |
| `CONNECTOR-2001-500` | Une erreur s’est produite lors du traitement des données copiées vers [!DNL Experience Platform]. Cette erreur peut concerner l’analyse, la validation ou la transformation. |
