---
keywords: Experience Platform;home;popular topics; notifications
description: Avec les Événements d'E/S Adobe, vous pouvez vous abonner à des événements et utiliser des hameçons Web pour recevoir des notifications concernant l'état de vos exécutions de flux. Ces notifications contiennent des informations sur la réussite de l'exécution de flux ou les erreurs qui ont contribué à l'échec de l'exécution.
solution: Experience Platform
title: Notifications d’exécution de flux
topic: overview
translation-type: tm+mt
source-git-commit: b5b785d8415c15e3acb9e1155811a66c51477717
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 4%

---


# Notifications d’exécution de flux

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[Le service de flux Adobe Experience Platform [ ! DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) est utilisé pour collecter et centraliser les données client à partir de diverses sources disparates au sein [!DNL Platform]. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Avec les Événements d&#39;E/S d&#39;Adobe, vous pouvez vous abonner à des événements et utiliser des hameçons Web pour recevoir des notifications concernant l&#39;état de vos exécutions de flux. Ces notifications contiennent des informations sur la réussite de l&#39;exécution de flux ou les erreurs qui ont contribué à l&#39;échec de l&#39;exécution.

Ce document décrit la procédure à suivre pour s’abonner à des événements, enregistrer des hameçons Web et recevoir des notifications contenant des informations sur l’état de vos exécutions de flux.

## Prise en main

Ce document exige une compréhension pratique des composantes suivantes de Adobe Experience Platform :

* [[ ! Système de modèle de données d’expérience (XDM) DNL]](../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
* [[ !Profil client en temps réel DNL]](../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[ ! Extraction de données Adobe Experience Platform DNL]](../ingestion/home.md): [!DNL Data Ingestion] représente les méthodes multiples par lesquelles [!DNL Platform] ingère des données provenant de ces sources, ainsi que la manière dont ces données sont conservées au sein de l’ [!DNL Data Lake] entreprise pour être utilisées par [!DNL Platform] les services en aval.

Ce document nécessite également une bonne compréhension des hameçons Web et de la façon de connecter un hameçon Web d&#39;une application à une autre. Consultez la [documentation](https://requestbin.com/blog/working-with-webhooks/) suivante pour plus d’informations sur les hameçons Web.

## Enregistrement de votre webhook

Pour recevoir des notifications sur l&#39;état de votre flux d&#39;exécution, vous devez enregistrer un webhook en spécifiant une URL webhook unique dans les détails d&#39;enregistrement de votre événement. Pour connecter un webhook à votre [!DNL I/O Events] abonnement, visitez le service [](https://webhook.site/) webhook et copiez l’URL unique fournie.

![webhook](./images/notifications/webhook-url.png)

## S&#39;abonner aux événements

Une fois que vous avez acquis une URL webhook unique, accédez aux Événements [d&#39;E/S d&#39;](https://www.adobe.io/apis/experienceplatform/events.html) Adobe et suivez les étapes décrites dans le document de notifications [d&#39;assimilation des](../ingestion/quality/subscribe-events.md) données au début s&#39;abonnant aux événements.

>[!IMPORTANT]
>Au cours du processus d’abonnement, veillez à sélectionner [!DNL Platform] les notifications en tant que fournisseur de événements et à sélectionner les abonnements de événement suivants :
>
>* **[!UICONTROL L&#39;exécution de flux de la source Experience Platform a réussi]**
>* **[!UICONTROL Échec de l&#39;exécution du flux de la source Experience Platform]**

>
>
Lorsque vous êtes invité à fournir une adresse webhook, utilisez l’URL webhook que vous avez acquise précédemment.

## Recevoir des notifications d&#39;exécution de flux

Une fois votre webhook connecté et votre abonnement d’événement terminé, vous pouvez début recevoir des notifications d’exécution de flux via le tableau de bord webhook.

Une notification renvoie des informations telles que le nombre de tâches d’assimilation exécutées, la taille du fichier et les erreurs. Une notification renvoie également une charge utile associée à votre flux exécuté au format JSON. La charge utile de réponse peut être classée en tant que `sources_flow_run_success` ou `sources_flow_run_failure`.

>[!IMPORTANT]
>Si l’assimilation partielle est activée pendant le processus de création de flux, un flux qui contient à la fois des intégrations réussies et en échec est marqué comme `sources_flow_run_success` uniquement si le nombre d’erreurs est inférieur au pourcentage de seuil d’erreur défini pendant le processus de création de flux. Si une exécution de flux réussie contient des erreurs, ces erreurs seront toujours incluses dans la charge utile de retour.

### Réussite

Une réponse réussie renvoie un ensemble de `metrics` caractéristiques d’une exécution de flux spécifique et `activities` qui décrit comment les données sont transformées.

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
    "imsOrgId": "{IMS_ORG}",
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
              "fileInfo": "https://platform-int.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
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
        "imsOrgId": "{IMS_ORG}",
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
| `metrics` | Définit les caractéristiques des données dans l’exécution de flux. |
| `activities` | Définit les différentes étapes et activités de transformation des données. |
| `durationSummary` | Définit le début et l’heure de fin de l’exécution du flux. |
| `sizeSummary` | Définit le volume des données en octets. |
| `recordSummary` | Définit le nombre d’enregistrements des données. |
| `fileSummary` | Définit le nombre de fichiers des données. |
| `fileInfo` | URL qui conduit à un aperçu des fichiers correctement assimilés. |
| `statusSummary` | Définit si l’exécution du flux est une réussite ou un échec. |

### Échec

La réponse suivante est un exemple d’échec de l’exécution du flux, avec une erreur survenant lors du traitement des données copiées. Des erreurs peuvent également se produire lorsque des données sont copiées à partir de la source. Une exécution de flux ayant échoué comprend des informations sur les erreurs qui ont contribué à l’échec de l’exécution, y compris son erreur et sa description.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{IMS_ORG}",
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
          "imsOrgId": "{IMS_ORG}",
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
| `fileInfo` | URL qui conduit à un aperçu des fichiers qui ont été correctement et non correctement ingérés. |

>[!NOTE]
>Consultez l&#39; [annexe](#errors) pour plus d&#39;informations sur les messages d&#39;erreur.

## Étapes suivantes

Vous pouvez désormais vous abonner à des événements qui vous permettent de recevoir des notifications en temps réel sur vos états d’exécution de flux. Pour plus d’informations sur les exécutions de flux et les sources, voir l’aperçu [des](./home.md)sources.

## Annexe

Les sections suivantes contiennent des informations supplémentaires sur l’utilisation des notifications d’exécution de flux.

### Présentation des messages d&#39;erreur {#errors}

Des erreurs d&#39;embouteillage peuvent se produire lorsque des données sont copiées à partir de la source ou lorsque les données copiées sont traitées vers [!DNL Platform]la source. Consultez le tableau ci-dessous pour en savoir plus sur les erreurs spécifiques.

| Erreur | Description |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Une erreur s&#39;est produite lors de la copie des données à partir d&#39;une source. |
| `CONNECTOR-2001-500` | Une erreur s&#39;est produite lors du traitement des données copiées vers [!DNL Platform]. Cette erreur peut concerner l’analyse, la validation ou la transformation. |
