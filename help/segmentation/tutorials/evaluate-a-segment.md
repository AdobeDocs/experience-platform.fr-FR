---
keywords: Experience Platform;home;popular topics;segment evaluation;Segmentation Service;segmentation;Segmentation;evaluate a segment;access segment results;evaluate and access segment;
solution: Experience Platform
title: Évaluation d’un segment
topic: tutorial
description: Ce document fournit un tutoriel sur l’évaluation des segments et l’accès aux résultats de segmentation à l’aide de l’API Segmentation.
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 64%

---


# Évaluation et accès aux résultats de segmentation

This document provides a tutorial for evaluating segments and accessing segment results using the [[!DNL Segmentation API]](../api/getting-started.md).

## Prise en main

This tutorial requires a working understanding of the various [!DNL Adobe Experience Platform] services involved in creating audience segments. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [[ !Service de segmentation Adobe Experience Platform DNL]](../home.md): Permet de créer des segments d’audience à partir de [!DNL Real-time Customer Profile] données.
- [[ ! Modèle de données d’expérience DNL (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

### En-têtes requis

Ce tutoriel exige aussi que vous ayez terminé le [tutoriel sur l’authentification](../../tutorials/authentication.md) pour passer des appels à des API [!DNL Platform] Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. Requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes POST, PUT et PATCH requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Évaluation d’un segment

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez ensuite évaluer le segment soit par une évaluation planifiée soit par l’évaluation sur demande.

[L’évaluation planifiée](#scheduled-evaluation) (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent pour exécuter une tâche d’exportation à un moment précis, tandis que l’[évaluation sur demande](#on-demand-evaluation) implique la création d’une tâche de segmentation pour créer immédiatement l’audience. Les étapes à suivre pour chaque type d’évaluation sont décrites ci-dessous.

If you have not yet completed the [create a segment using the Segmentation API](./create-a-segment.md) tutorial or created a segment definition using [Segment Builder](../ui/overview.md), please do so before proceeding with this tutorial.

## Évaluation planifiée {#scheduled-evaluation}

L’évaluation planifiée permet à votre organisation IMS de créer un planning récurrent pour exécuter automatiquement les tâches d’exportation.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les environnements de test avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. If your organization has more than five merge policies for [!DNL XDM Individual Profile] within a single sandbox environment, you will not be able to use scheduled evaluation.

### Création d’un planning

En effectuant une requête POST sur le point de terminaison `/config/schedules`, vous pouvez créer un planning et inclure l’heure spécifique à laquelle le planning doit être déclenché.

Vous trouverez des informations plus détaillées sur l&#39;utilisation de ce point de terminaison dans le guide des points de terminaison [planifiés.](../api/schedules.md#create)

### Activation d’un planning

Par défaut, un planning est inactif lors de la création, sauf si la propriété `state` est définie sur `active` dans le corps de la requête de création (POST). Vous pouvez activer un planning (définissez `state` sur `active`) en effectuant une requête PATCH sur le point de terminaison `/config/schedules` et en incluant l’identifiant du planning dans le chemin.

Vous trouverez des informations plus détaillées sur l&#39;utilisation de ce point de terminaison dans le guide des points de terminaison [planifiés.](../api/schedules.md#update-state)

### Mise à jour de l’heure du planning

Vous pouvez mettre à jour l’heure du planning en effectuant une requête PATCH sur le point de terminaison `/config/schedules` et en incluant l’identifiant du planning dans le chemin.

Vous trouverez des informations plus détaillées sur l&#39;utilisation de ce point de terminaison dans le guide des points de terminaison [planifiés.](../api/schedules.md#update-schedule)

## Évaluation sur demande

L’évaluation sur demande vous permet de créer une tâche de segmentation afin de générer un segment ciblé chaque fois que vous en avez besoin. Contrairement à l’évaluation planifiée, celle-ci n’a lieu que sur demande et n’est pas récurrente.

### Création d’une tâche de segmentation

Une tâche de segmentation est un processus asynchrone qui crée un nouveau segment ciblé. It references a segment definition, as well as any merge policies controlling how [!DNL Real-time Customer Profile] merges overlapping attributes across your profile fragments. Lorsqu’une tâche de segmentation se termine avec succès, vous pouvez collecter diverses informations sur le segment, telles que les erreurs qui se sont produites au cours du traitement et la taille finale de votre audience.

Vous pouvez créer une tâche de segmentation en exécutant une requête POST sur le point de terminaison `/segment/jobs` dans l’API [!DNL Real-time Customer Profile]

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le guide des points de terminaison des tâches de [segment.](../api/segment-jobs.md#create)


### Recherche de l’état de la tâche de segmentation

Vous pouvez utiliser l’`id` pour une tâche de segmentation spécifique afin d’effectuer une requête de recherche (GET) pour afficher l’état actuel de la tâche.

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le guide des points de terminaison des tâches de [segment.](../api/segment-jobs.md#get)

## Interprétation des résultats de segmentation

Lorsque les tâches de segmentation sont exécutées avec succès, le mappage `segmentMembership` est mis à jour pour chaque profil inclus dans le segment. `segmentMembership` stocke également tous les segments d’audience préévalués qui sont assimilés [!DNL Platform], ce qui permet l’intégration à d’autres solutions, telles que [!DNL Adobe Audience Manager]les solutions.

L’exemple suivant illustre l’attribut `segmentMembership` pour chaque enregistrement de profil individuel :

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Propriété | Description |
| -------- | ----------- |
| `lastQualificationTime` | La date et l’heure auxquelles l’appartenance au segment a été affirmée et le profil est entré dans le segment ou en est sorti. |
| `status` | L’état de la participation au segment dans le cadre de la requête actuelle. Doit être égal à l’une des valeurs connues suivantes : <ul><li>`existing` : l’entité reste dans le segment.</li><li>`realized` : l’entité entre dans le segment.</li><li>`exited` : l’entité quitte le segment.</li></ul> |

## Accès aux résultats de segmentation

Vous pouvez accéder aux résultats d’une tâche de segmentation de deux manières : en accédant aux profils individuels ou en exportant une audience entière vers un jeu de données.

Les sections suivantes décrivent ces options de manière plus détaillée.

## Recherche d’un profil

If you know the specific profile that you would like to access, you can do so using the [!DNL Real-time Customer Profile] API. Toutes les étapes pour accéder aux profils individuels sont disponibles dans le tutoriel sur l’[accès aux données de Real-time Customer Profile à l’aide de l’API Profile](../../profile/api/entities.md).

## Exportation d’un segment {#export}

Une fois la tâche de segmentation terminée (la valeur de l’attribut `status` correspond à &quot;SUCCEEDED&quot;), vous pouvez exporter votre audience vers un jeu de données permettant son accès et son utilisation.

Les étapes suivantes sont requises pour exporter votre audience :

- [Création d’un jeu de données cible](#create-a-target-dataset) : créez le jeu de données permettant de contenir les membres de l’audience.
- [Génération de profils d’audience dans le jeu de données](#generate-profiles-for-audience-members) : renseignez le jeu de données avec des profils individuels XDM en fonction des résultats d’une tâche de segmentation.
- [Contrôle de la progression de l’exportation](#monitor-export-progress) : vérifiez la progression actuelle du processus d’exportation.
- [Lecture des données d’audience](#next-steps) : récupérez les profils individuels XDM obtenus représentant les membres de votre audience.

### Création d’un jeu de données cible

Lors de l’exportation d’une audience, un jeu de données cible doit d’abord être créé. Il est important que le jeu de données soit correctement configuré pour garantir la réussite de l’exportation.

Le schéma sur lequel repose le jeu de données est l’une des principales considérations (`schemaRef.id` dans l’exemple de requête API ci-dessous). Pour exporter un segment, le jeu de données doit être basé sur le [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Un schéma d’union est un schéma en lecture seule généré par le système regroupant les champs des schémas qui partagent la même classe, dans ce cas précis, la classe XDM Individual Profile. Pour plus d’informations sur la vue d’union des schémas, consultez la [section Real-time Customer Profile du guide de développement du registre des schémas](../../xdm/api/getting-started.md).

Il existe deux manières de créer le jeu de données nécessaire :

- **Utilisation des API :** Les étapes suivantes de ce didacticiel expliquent comment créer un jeu de données qui référence le [!DNL XDM Individual Profile Union Schema] système à l’aide de l’ [!DNL Catalog] API.
- **Utilisation de l’interface utilisateur :** Pour utiliser l’interface [!DNL Adobe Experience Platform] utilisateur pour créer un jeu de données faisant référence au schéma d’union, suivez les étapes du didacticiel [](../ui/overview.md) IU, puis revenez à ce didacticiel pour passer à la procédure de [génération de profils](#generate-xdm-profiles-for-audience-members)d’audience.

Si vous disposez déjà d’un jeu de données compatible et que vous connaissez son identifiant, vous pouvez passer directement à l’étape de [génération de profils](#generate-xdm-profiles-for-audience-members).

**Format d’API**

```http
POST /dataSets
```

**Requête**

La requête suivante crée un jeu de données et fournit des paramètres de configuration dans le payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Un nom explicite pour le jeu de données. |
| `schemaRef.id` | L’identifiant de la vue d’union (schéma) à laquelle le jeu de données sera associé. |
| `fileDescription.persisted` | Une valeur booléenne qui, lorsqu’elle est définie sur `true`, permet de conserver le jeu de données dans la vue d’union. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l’identifiant unique et en lecture seule généré par le système du jeu de données que vous venez de créer. Un identifiant de jeu de données correctement configuré est nécessaire pour exporter les membres de l’audience.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Génération de profils pour les membres de l’audience {#generate-profiles}

Une fois que vous disposez d’un jeu de données d’union persistant, vous pouvez créer une tâche d’exportation afin de conserver les membres de l’audience dans le jeu de données, en effectuant une requête POST sur le point de terminaison `/export/jobs` dans l’API et en fournissant l’identifiant du jeu de données et les informations sur les segments que vous souhaitez exporter.[!DNL Real-time Customer Profile]

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le guide des points de terminaison des tâches [d’exportation.](../api/export-jobs.md#create)

### Contrôle de la progression de l’exportation

Lorsqu’une tâche d’exportation est en cours de traitement, vous pouvez contrôler son état en effectuant une requête GET sur le point de terminaison `/export/jobs` et en incluant l’`id` de la tâche d’exportation dans le chemin. La tâche d’exportation est terminée lorsque le champ `status` renvoie la valeur &quot;SUCCEEDED&quot;.

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le guide des points de terminaison des tâches [d’exportation.](../api/export-jobs.md#get)

## Étapes suivantes

Once the export has completed successfully, your data is available within the [!DNL Data Lake] in [!DNL Experience Platform]. You can then use the [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) to access the data using the `batchId` associated with the export. Selon la taille du segment, les données peuvent se présenter sous forme de blocs et le lot peut être constitué de plusieurs fichiers.

For step-by-step instructions on how to use the [!DNL Data Access] API to access and download batch files, follow the [Data Access tutorial](../../data-access/tutorials/dataset-data.md).

Vous pouvez également accéder aux données de segment exportées avec succès à l’aide de [!DNL Adobe Experience Platform Query Service]. Using the UI or RESTful API, [!DNL Query Service] allows you to write, validate, and run queries on data within the [!DNL Data Lake].

For more information on how to query audience data, please review the documentation on [[!DNL Query Service]](../../query-service/home.md).
