---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux ;
title: Brouillons De Flux À L’Aide De L’API Flow Service
description: Découvrez comment définir vos flux de données dans un état de brouillon à l’aide de l’API Flow Service.
badge: label="Nouvelle fonctionnalité" type="Positive"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 18%

---

# Brouillons de flux de données à l’aide de l’API Flow Service

Enregistrez vos flux de données en tant que brouillons lors de l’utilisation de l’API Flow Service en fournissant la variable `mode=draft` paramètre de requête lors de l’appel de création de flux. Les versions préliminaires peuvent être mises à jour ultérieurement avec de nouvelles informations, puis publiées une fois qu’elles sont prêtes. Ce tutoriel décrit les étapes à suivre pour définir vos flux de données dans un état de brouillon à l’aide de l’API Flow Service.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Conditions préalables

Ce tutoriel nécessite que vous ayez déjà généré les ressources nécessaires pour créer un flux de données. Cela inclut les éléments suivants :

* Une connexion de base authentifiée
* Une connexion source
* Un schéma XDM cible
* Un jeu de données cible
* Une connexion cible
* Mappage

Si vous ne disposez pas encore de ces valeurs, sélectionnez une source parmi [catalogue dans la présentation des sources](../../home.md). Suivez ensuite les instructions de cette source donnée pour générer les ressources requises pour créer un flux de données de brouillon.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

## Définition du flux de données à l’état de brouillon

Les sections suivantes décrivent le processus de définition d’un flux de données en tant que brouillon, de mise à jour du flux de données, de publication du flux de données, puis de suppression finale du flux de données.

### Création d’un flux de données

Pour définir un flux de données en tant que brouillon, envoyez une requête de POST à la variable `/flows` point d’entrée lors de l’ajout de la variable `mode=draft` comme paramètre de requête. Vous pouvez ainsi créer un flux de données et l’enregistrer en tant que brouillon.

**Format d’API**

```http
POST /flows?mode=draft
```

| Paramètre | Description |
| --- | --- |
| `mode` | Paramètre de requête fourni par l’utilisateur qui décide de l’état du flux de données. Pour définir un flux de données en tant que brouillon, définissez `mode` to `draft`. |

**Requête**

La requête suivante crée un flux de données de brouillon.

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

Une réponse réussie renvoie la variable `id` et le `etag` de votre flux de données.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Mise à jour d’un flux de données

Pour mettre à jour votre brouillon, envoyez une requête de PATCH à l’ `/flows` point d’entrée tout en fournissant l’identifiant du flux de données que vous souhaitez mettre à jour. Au cours de cette étape, vous devez également fournir un `If-Match` paramètre d’en-tête , qui correspond à `etag` du flux de données que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

Les requêtes suivantes ajoutent des transformations de mappage au flux de données brouillé.

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

Une réponse réussie renvoie votre identifiant de flux et `etag`. Pour vérifier la modification, vous pouvez envoyer une demande de GET à la variable `/flows` point de terminaison tout en fournissant votre identifiant de flux.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Publication d’un flux de données

Une fois que votre brouillon est prêt à être publié, envoyez une requête de POST au `/flows` point de terminaison tout en fournissant l’identifiant du flux de données de brouillon que vous souhaitez publier, ainsi qu’une opération d’action pour la publication.

**Format d’API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Paramètre | Description |
| --- | --- |
| `op` | Opération d’action qui met à jour l’état du flux de données interrogé. Pour publier un brouillon de flux de données, définissez `op` to `publish`. |

**Requête**

La requête suivante publie votre flux de données de brouillon.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie l’identifiant et le `etag` de votre flux de données.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Supprimer un flux de données

Pour supprimer votre flux de données, envoyez une requête de DELETE au `/flows` point d’entrée tout en fournissant l’identifiant du flux de données que vous souhaitez supprimer. Pour obtenir des instructions détaillées sur la suppression d’un flux de données à l’aide de l’API Flow Service, consultez le guide sur [suppression d’un flux de données dans l’API](./delete-dataflows.md).