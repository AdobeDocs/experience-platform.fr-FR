---
keywords: Experience Platform;accueil;rubriques les plus consultées;identités;historique des clusters
solution: Experience Platform
title: Obtention de l’historique des clusters d’une identité
description: Les identités peuvent déplacer des clusters au cours de différentes opérations de graphiques d’appareil. Le service d’identités offre une visibilité sur les associations de cluster d’une identité donnée au fil du temps.
role: Developer
exl-id: e52edb15-e3d6-4085-83d5-212bbd952632
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 78%

---

# Obtention de l’historique des clusters d’une identité

Les identités peuvent déplacer des clusters au cours de différentes opérations de graphiques d’appareil. [!DNL Identity Service] offre une visibilité sur les associations de cluster d’une identité donnée au fil du temps.

Utilisez le paramètre `graph-type` facultatif pour indiquer le type de sortie à partir duquel obtenir le cluster. Les options sont les suivantes :

- `None` : ne réalise aucune combinaison d’identités.
- `Private Graph` : réalise des combinaisons d’identités en se basant sur votre graphique d’identités privé. Il s’agit de la valeur par défaut si aucune valeur `graph-type` n’est renseignée.

## Obtention de l’historique des clusters d’une seule identité

**Format d’API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Requête**

Option 1 : fournissez l’identité comme valeur d’espace de noms (`nsId`, par identifiant) et comme valeur d’identifiant (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2 : fournissez l’identité comme valeur d’espace de noms (`ns`, par nom) et comme valeur d’identifiant (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3 : fournissez l’identité comme XID (`xid`). Pour plus d’informations sur l’obtention du XID d’une identité, consultez la section traitant de l’[obtention du XID pour une identité](./list-native-id.md) dans ce document.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obtention de l’historique des clusters de plusieurs identités

Afin de renvoyer les historiques de clusters pour plusieurs identités, utilisez la méthode `POST` comme équivalent par lots de la méthode `GET` décrite ci-dessus.

>[!NOTE]
>
>La requête ne doit pas indiquer plus de 1 000 identités. Les requêtes dépassant les 1 000 identités se traduiront par un code d’état 400.

**Format d’API**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Corps de la requête**

Option 1 : fournissez la liste des XID pour lesquels vous voulez récupérer les membres du cluster.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Option 2 : fournissez une liste d’identités sous forme d’identifiants composites où la valeur d’identifiant et l’espace de noms sont spécifiés par le code d’espace de noms.

```shell
{
    "compositeXids": [{
            "ns": "AdCloud",
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "ns": "AddCloud",
            "id": "WY-RNgAAArI4rGBo"
        }
    ]
}
```

**Requête**

**Requête avec bouchon**

L’utilisation de l’en-tête `x-uis-cst-ctx: stub` renverra une réponse bouchonnée. Il s’agit là d’une solution temporaire qui facilite le développement rapide de l’intégration pendant que les services sont en cours d’achèvement. Cette solution deviendra obsolète lorsqu’elle ne sera plus nécessaire.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**Utilisation des XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Utilisation des UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "compositeXids": [{
                "nsid": 411,
                "id": "WRbM7AAAAJ_PBZHl"
            },
            {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            }
        ],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Réponse**

```json
{
    "version": 1,
    "xidsClusterHistory": [{
            "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                    "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                    "cRecordedTS": "1504741401382"
                },
                {
                    "clusterId": "29bf066c-971a-11e7-abc4-cec278b6b50a",
                    "cRecordedTS": "1502063001629"
                },
                {
                    "clusterId": "aeb2f60c-b0f1-446a-91dd-d28ab6a44ff9",
                    "cRecordedTS": "1499384601763"
                }
            ]
        },
        {
            "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                "cRecordedTS": "1504741401937"
            }]
        }
    ],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]

}
```

>[!NOTE]
>
>La réponse comportera toujours une entrée pour chaque XID fourni dans la requête, que les XID d’une requête appartiennent au même cluster ou qu’un ou plusieurs clusters y soient associés.

## Étapes suivantes

Passez au tutoriel suivant pour [répertorier les mappages d’une identité](./list-identity-mappings.md)
