---
title: API d’hygiène des données (Alpha)
description: Découvrez comment corriger ou supprimer par programmation les données personnelles stockées de vos clients dans Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: dfe9c1ef826bc769a82938223029cd41c066c221
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 19%

---

# API d’hygiène des données (Alpha)

>[!IMPORTANT]
>
>L’API Data Hygiene est actuellement en version alpha et votre entreprise peut ne pas y avoir encore accès. Les fonctionnalités décrites dans ce document peuvent faire l’objet de modifications.

L’API Data Hygiene vous permet de corriger ou de supprimer par programmation les données personnelles stockées de vos clients dans Adobe Experience Platform. Contrairement à l’API du Privacy Service, ces opérations ne doivent pas être associées aux réglementations légales en matière de confidentialité et peuvent être utilisées uniquement à des fins de nettoyage et d’exactitude de vos données.

## Prise en main

Cette section présente les concepts de base que vous devez connaître avant d’effectuer des appels vers l’API Data Hygiene.

### Collecte des valeurs des en-têtes requis

Pour passer des appels à l’API Data Hygiene, vous devez d’abord rassembler vos informations d’authentification. Il s’agit des mêmes informations d’identification que celles utilisées pour accéder à l’API du Privacy Service. Suivez le [guide de prise en main](./api/getting-started.md) de l’API du Privacy Service pour générer des valeurs pour chacun des en-têtes requis pour l’API d’hygiène des données, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

### Lecture d&#39;exemples d&#39;appels API

Ce document fournit un exemple d’appel API pour démontrer comment formater vos requêtes. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section [Comment lire des exemples d’appels API](../landing/api-guide.md#sample-api) dans le guide de prise en main des API Experience Platform.

## Création d’une tâche de suppression

Vous pouvez créer une tâche de suppression en effectuant une requête de POST.

**Format d’API**

```http
POST /jobs
```

**Requête**

La payload de la requête est structurée de la même manière que celle d’une requête [de suppression dans l’API du Privacy Service](./api/privacy-jobs.md#access-delete). Il comprend un tableau `users` dont les objets représentent les utilisateurs dont les données doivent être supprimées.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{IMS_ORG}"
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
| `companyContexts` | Un tableau contenant des informations d’authentification pour votre organisation. Il doit contenir un seul objet avec les propriétés suivantes : <ul><li>`namespace`: Cette propriété doit être définie sur `imsOrgID`.</li><li>`value`: Votre identifiant de l&#39;organisation IMS. Il s’agit de la même valeur que celle fournie dans l’en-tête `x-gw-ims-org-id`.</li></ul> |
| `users` | Tableau contenant une collection d’au moins un utilisateur dont vous souhaitez supprimer les informations. Chaque objet d’utilisateur contient les informations suivantes : <ul><li>`key` : un identifiant pour un utilisateur utilisé pour exécuter les identifiants de tâches distincts dans les données de réponse. Il est recommandé de choisir une chaîne unique facilement identifiable pour cette valeur afin de pouvoir la référencer ou la rechercher ultérieurement.</li><li>`action` : un tableau répertoriant les actions souhaitées pouvant être effectuées sur les données de l’utilisateur. Doit contenir une seule valeur string : `delete`.</li><li>`userIDs` : une collection d’identités pour cet utilisateur. Le nombre d’identités qu’un utilisateur unique peut posséder est limité à neuf. Chaque identité contient les propriétés suivantes : <ul><li>`namespace`: Espace de noms  [d’identité ](../identity-service/namespaces.md) associé à l’identifiant. Il peut s’agir d’un [espace de noms standard](./api/appendix.md#standard-namespaces) reconnu par Platform ou d’un espace de noms personnalisé défini par votre organisation. Le type d’espace de noms utilisé doit être reflété dans la propriété `type` .</li><li>`value`: La valeur d’identité.</li><li>`type`: Doit être défini sur  `standard` si vous utilisez un espace de noms reconnu globalement ou  `custom` si vous utilisez un espace de noms défini par votre organisation.</li></ul></li></ul> |

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
