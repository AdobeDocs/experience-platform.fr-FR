---
title: Exportation de données vers des environnements ML externes
description: Découvrez comment partager un jeu de données de formation préparé, créé avec Data Distiller, vers un emplacement de stockage dans le cloud que votre environnement ML peut lire pour la formation et la notation de votre modèle.
exl-id: 75022acf-fafd-41d6-8dfa-ff3fd4c4fa7e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 6%

---

# Exportation de données dans des environnements ML externes

Ce document explique comment partager un jeu de données de formation préparé créé avec Data Distiller vers un emplacement de stockage dans le cloud que votre environnement ML peut lire pour la formation et la notation de votre modèle. L’exemple ici exporte le jeu de données d’apprentissage vers la [zone d’entrée de données (DLZ)](../../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md). Vous pouvez modifier la destination de stockage selon les besoins pour travailler avec votre environnement d’apprentissage automatique.

Le [service de flux pour les destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/) est utilisé pour terminer le pipeline de fonctionnalités en déposant un jeu de données de fonctionnalités calculées dans un emplacement de stockage dans le cloud approprié.

## Création de la connexion source {#create-source-connection}

La connexion source est responsable de la configuration de la connexion à votre jeu de données Adobe Experience Platform afin que le flux résultant sache exactement où chercher les données et dans quel format.

```python
from aepp import flowservice
flow_conn = flowservice.FlowService()

training_dataset_id = <YOUR_TRAINING_DATASET_ID>

source_res = flow_conn.createSourceConnectionDataLake(
    name=f"[CMLE] Featurized Dataset source connection created by {username}",
    dataset_ids=[training_dataset_id],
    format="parquet"
)
source_connection_id = source_res["id"]
```

## Création de la connexion cible {#create-target-connection}

La connexion cible est responsable de la connexion au système de fichiers de destination. Cela nécessite d’abord la création d’une connexion de base au compte de stockage dans le cloud (la zone d’entrée des données dans cet exemple), puis une connexion cible à un chemin d’accès de fichier spécifique avec des options de compression et de format spécifiées.

Les destinations de stockage dans le cloud disponibles sont chacune identifiées par un identifiant de spécification de connexion :

| Type de stockage dans le cloud | Identifiant spécifique de la connexion |
|-----------------------|--------------------------------------|
| Amazon S3 | 4fce964d-3f37-408f-9778-e597338a21ee |
| Stockage Azure Blob | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |
| Azure Data Lake | be2c3209-53bc-47e7-ab25-145db8b873e1 |
| Zone d’atterrissage des données | 10440537-2a7b-4583-ac39-ed38d4b848e8 |
| Google Cloud Storage | c5d93acb-ea8b-4b14-8f53-02138444ae99 |
| SFTP | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

```python
connection_spec_id = "10440537-2a7b-4583-ac39-ed38d4b848e8"
base_connection_res = flow_conn.createConnection(data={
    "name": "Base Connection to DLZ created by",
    "auth": None,
    "connectionSpec": {
        "id": connection_spec_id,
        "version": "1.0"
    }
})
base_connection_id = base_connection_res["id"]

target_res = flow_conn.createTargetConnection(
    data={
        "name": "Data Landing Zone target connection",
        "baseConnectionId": base_connection_id,
        "params": {
            "mode": "Server-to-server",
            "compression": config.get("Cloud", "compression_type"),
            "datasetFileType": config.get("Cloud", "data_format"),
            "path": config.get("Cloud", "export_path")
        },
        "connectionSpec": {
            "id": connection_spec_id,
            "version": "1.0"
        }
    }
)
target_connection_id = target_res["id"]
```

## Création du flux de données {#create-data-flow}

La dernière étape consiste à créer un flux de données entre le jeu de données spécifié dans la connexion source et le chemin d’accès au fichier de destination spécifié dans la connexion cible.

Chaque type de stockage dans le cloud disponible est identifié par un identifiant de spécification de flux :

| Type de stockage dans le cloud | Identifiant de spécification de flux |
|-----------------------|--------------------------------------|
| Amazon S3 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Stockage Azure Blob | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Azure Data Lake | 17be2013-2549-41ce-96e7-a70363bec293 |
| Zone d’atterrissage des données | cd2fc47e-e838-4f38-a581-8fff2f99b63a |
| Google Cloud Storage | 585c15c4-6cbf-4126-8f87-e26bff78b657 |
| SFTP | 354d6aad-4754-46e4-a576-1b384561c440 |

Le code suivant crée un flux de données avec une planification qui doit démarrer dans un avenir lointain. Cela vous permet de déclencher des flux ad hoc lors du développement du modèle. Une fois que vous disposez d’un modèle formé, vous pouvez mettre à jour le planning du flux de données pour partager le jeu de données de fonctionnalités selon la planification souhaitée.

```python
import time

on_schedule = False
if on_schedule:
    schedule_params = {
        "interval": 3,
        "timeUnit": "hour",
        "startTime": int(time.time())
    }
else:
    schedule_params = {
        "interval": 1,
        "timeUnit": "day",
        "startTime": int(time.time() + 60*60*24*365) # Start the schedule far in the future
    }

flow_spec_id = "cd2fc47e-e838-4f38-a581-8fff2f99b63a"
flow_obj = {
    "name": "Flow for Feature Dataset to DLZ",
    "flowSpec": {
        "id": flow_spec_id,
        "version": "1.0"
    },
    "sourceConnectionIds": [
        source_connection_id
    ],
    "targetConnectionIds": [
        target_connection_id
    ],
    "transformations": [],
    "scheduleParams": schedule_params
}
flow_res = flow_conn.createFlow(
    obj = flow_obj,
    flow_spec_id = flow_spec_id
)
dataflow_id = flow_res["id"]
```

Une fois le flux de données créé, vous pouvez désormais déclencher une exécution de flux ad hoc pour partager le jeu de données de fonctionnalités à la demande :

```python
from aepp import connector

connector = connector.AdobeRequest(
  config_object=aepp.config.config_object,
  header=aepp.config.header,
  loggingEnabled=False,
  logger=None,
)

endpoint = aepp.config.endpoints["global"] + "/data/core/activation/disflowprovider/adhocrun"

payload = {
    "activationInfo": {
        "destinations": [
            {
                "flowId": dataflow_id, 
                "datasets": [
                    {"id": created_dataset_id}
                ]
            }
        ]
    }
}

connector.header.update({"Accept":"application/vnd.adobe.adhoc.dataset.activation+json; version=1"})
activation_res = connector.postData(endpoint=endpoint, data=payload)
activation_res
```

## Partage rationalisé vers la zone d’entrée des données

Pour partager plus facilement un jeu de données dans la zone d’entrée des données, la bibliothèque `aepp` fournit une fonction `exportDatasetToDataLandingZone` qui exécute les étapes ci-dessus dans un seul appel de fonction :

```python
from aepp import exportDatasetToDataLandingZone

export = exportDatasetToDataLandingZone.ExportDatasetToDataLandingZone()

dataflow_id = export.createDataFlowRunIfNotExists(
    dataset_id = created_dataset_id,
    data_format = data_format, 
    export_path= export_path, 
    compression_type = compression_type, 
    on_schedule = False, 
    config_path = config_path, 
    entity_name = "Flow for Featurized Dataset to DLZ"
)
```

Ce code crée la connexion source, la connexion cible et le flux de données en fonction des paramètres fournis et exécute une exécution ad hoc du flux de données en une seule étape.
