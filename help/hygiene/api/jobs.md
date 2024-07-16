---
title: Suppression d’enregistrements à l’aide de l’API Data Hygiene
description: Découvrez comment corriger ou supprimer par programmation les données personnelles des clients stockées dans Adobe Experience Platform.
role: Developer
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 96%

---

# Suppression d’enregistrements à l’aide de l’API Data Hygiene

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

L’API Data Hygiene vous permet de corriger ou de supprimer par programmation les données personnelles de vos clients stockées dans Adobe Experience Platform.

Vous pouvez accéder à l’API par le même chemin racine que l’[API Privacy Service](../../privacy-service/api/overview.md) : `https://platform.adobe.io/data/core/privacy/`

## Prise en main

Cette section présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API Data Hygiene.

### Collecte des valeurs des en-têtes requis

Pour effectuer des appels à l’API Data Hygiene, vous devez d’abord rassembler vos informations d’authentification. Ces informations d’identification sont les mêmes que celles utilisées pour accéder à l’API Privacy Service. Consultez la [présentation de l’API](./overview.md#getting-started) afin de générer des valeurs pour chacun des en-têtes obligatoires pour l’API Data Hygiene, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

### Lecture d’exemples d’appels API

Ce document fournit un exemple d’appel API pour illustrer la manière dont vous devez formater vos requêtes. Pour en savoir plus sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section relative à la [lecture d’exemples d’appels API](../../landing/api-guide.md#sample-api) dans le guide de prise en main des API d’Experience Platform.

## Création d’une tâche de suppression

Vous pouvez créer une tâche de suppression en effectuant une requête POST.

**Format d’API**

```http
POST /jobs
```

**Requête**

La structure de la payload de la requête est similaire à celle d’une [requête DELETE dans l’API Privacy Service](../../privacy-service/api/privacy-jobs.md#access-delete). Elle comprend un tableau `users` dans lequel les objets représentent les utilisateurs dont les données doivent être supprimées.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `companyContexts` | Un tableau contenant des informations d’authentification pour votre organisation. Il doit contenir un seul objet avec les propriétés suivantes : <ul><li>`namespace` : Cette propriété doit être définie sur `imsOrgID`.</li><li>`value` : ID d’organisation. Il s’agit de la même valeur que celle fournie dans l’en-tête `x-gw-ims-org-id`.</li></ul> |
| `users` | Un tableau contenant une collection d’au moins un utilisateur dont vous souhaitez supprimer les informations. Chaque objet d’utilisateur contient les informations suivantes : <ul><li>`key` : un identifiant pour un utilisateur utilisé pour exécuter les identifiants de tâches distincts dans les données de réponse. Nous vous recommandons de choisir une chaîne unique et facilement identifiable pour cette valeur afin de pouvoir la référencer ou la rechercher ultérieurement.</li><li>`action` : un tableau répertoriant les actions souhaitées pouvant être effectuées sur les données de l’utilisateur. Doit contenir une seule valeur de chaîne : `delete`.</li><li>`userIDs` : une collection d’identités pour cet utilisateur. Le nombre d’identités qu’un utilisateur unique peut posséder est limité à neuf. Chaque identité contient les propriétés suivantes : <ul><li>`namespace` : l’[espace de noms d’identité](../../identity-service/features/namespaces.md) associé à l’identifiant. Il peut s’agir d’un [espace de noms standard](../../privacy-service/api/appendix.md#standard-namespaces) reconnu par Platform ou d’un espace de noms personnalisé défini par votre organisation. Le type d’espace de noms utilisé doit être reflété dans la propriété `type`.</li><li>`value` : la valeur de l’identité.</li><li>`type` : doit être défini sur `standard` si vous utilisez un espace de noms reconnu globalement ou sur `custom` si vous utilisez un espace de noms défini par votre organisation.</li></ul></li></ul> |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails des tâches créées.

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
