---
keywords: Experience Platform;accueil;rubriques les plus consultées;flow service;
title: Créer des brouillons de flux de données à l’aide de l’API Flow Service
description: Découvrez comment définir vos flux de données sur le statut de brouillon à l’aide de l’API Flow Service.
badge: label="New Feature" type="Positive"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: ht
source-wordcount: '591'
ht-degree: 100%

---

# Créer des brouillons de flux de données à l’aide de l’API Flow Service

Enregistrez vos flux de données en tant que brouillons lors de l’utilisation de l’API Flow Service en indiquant le paramètre de requête `mode=draft` lors de l’appel de création de flux. Vous pouvez modifier les brouillons à tout moment et les publier quand ils sont prêts. Ce tutoriel décrit les étapes à suivre pour définir vos flux de données sur le statut de brouillon à l’aide de l’API Flow Service.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Conditions préalables

Avant de suivre ce tutoriel, vous devez avoir généré les ressources nécessaires pour créer un flux de données. Il s’agit des éléments suivants :

* une connexion de base authentifiée,
* une connexion source,
* un schéma XDM cible,
* un jeu de données cible,
* une connexion cible,
* un mappage.

Si vous ne disposez pas de ces ressources, sélectionnez une source dans le [catalogue de la présentation des sources](../../home.md). Suivez ensuite les instructions de la source donnée pour générer les ressources nécessaires à la création d’un brouillon de flux de données.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

## Définir un flux de données sur le statut de brouillon

Les sections suivantes décrivent comment définir un flux de données en tant que brouillon, mettre à jour le flux de données, le publier et le supprimer, si nécessaire.

### Créer un brouillon de flux de données

Pour définir un flux de données en tant que brouillon, envoyez une requête POST au point d’entrée `/flows` et indiquez le paramètre de requête `mode=draft`. Vous pouvez ainsi créer un flux de données et l’enregistrer en tant que brouillon.

**Format d’API**

```http
POST /flows?mode=draft
```

| Paramètre | Description |
| --- | --- |
| `mode` | Paramètre de requête fourni par l’utilisateur ou l’utilisatrice qui décide du statut du flux de données. Pour définir un flux de données en tant que brouillon, définissez `mode` sur `draft`. |

**Requête**

La requête suivante permet de créer un brouillon de flux de données.

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**Réponse**

Une réponse réussie renvoie l’`id` et l’`etag` correspondant de votre flux de données.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Mettre à jour un flux de données

Pour mettre à jour le brouillon, envoyez une requête PATCH au point d’entrée `/flows` et indiquez l’identifiant du flux de données à mettre à jour. Au cours de cette étape, vous devez également fournir un paramètre d’en-tête `If-Match`, qui correspond à l’`etag` du flux de données que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

Les requêtes suivantes permettent d’ajouter des transformations de mappage au brouillon de flux de données.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**Réponse**

Une réponse réussie renvoie l’identifiant de flux et l’`etag`. Pour vérifier que la modification a réussi, envoyez une requête GET au point d’entrée `/flows` et indiquez votre identifiant de flux.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Publier un flux de données

Une fois que votre brouillon est prêt à être publié, envoyez une requête POST au point d’entrée `/flows` et indiquez l’identifiant du brouillon de flux de données que vous souhaitez publier, ainsi qu’une opération d’action pour la publication.

**Format d’API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Paramètre | Description |
| --- | --- |
| `op` | Opération d’action qui met à jour le statut du flux de données interrogé. Pour publier un brouillon de flux de données, définissez `op` sur `publish`. |

**Requête**

La requête suivante permet de publier le brouillon de flux de données.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie l’identifiant et l’`etag` correspondant du flux de données.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Supprimer un flux de données

Pour supprimer le flux de données, envoyez une requête DELETE au point d’entrée `/flows` et indiquez l’identifiant du flux de données à supprimer. Pour connaître la procédure de suppression d’un flux de données à l’aide de l’API Flow Service, consultez le guide sur la [suppression d’un flux de données dans l’API](./delete-dataflows.md).