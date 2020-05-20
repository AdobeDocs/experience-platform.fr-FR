---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Obtenir l'historique de cluster d'une identité
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 1%

---


# Obtenir l&#39;historique de cluster d&#39;une identité

Les identités peuvent déplacer des grappes au cours de diverses exécutions de graphiques de périphériques. Avec le temps, Identity Service permet d&#39;identifier les associations de cluster d&#39;une identité donnée.

Utilisez un paramètre facultatif `graph-type` pour indiquer le type de sortie à partir duquel la grappe doit être récupérée. Les options sont les suivantes :

- `None` - Ne pas procéder à l&#39;assemblage d&#39;identité.
- `Private Graph` - Effectuez des assemblages d&#39;identité basés sur votre graphique d&#39;identité privée. Si aucun `graph-type` paramètre n’est fourni, il s’agit de la valeur par défaut.

## Obtenir l&#39;historique de cluster d&#39;une identité unique

**Format d’API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Requête**

Option 1 : Fournissez l’identité sous forme d’espace de nommage (`nsId`, par ID) et de valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2 : Fournissez l’identité sous forme d’espace de nommage (`ns`, par nom) et de valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3 : Fournissez l’identité sous la forme XID (`xid`). Pour plus d&#39;informations sur la façon d&#39;obtenir le XID d&#39;une identité, consultez la section de ce document qui traite de l&#39; [obtention du XID pour une identité](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obtenir l’historique de cluster d’une multitude d’identités

Utilisez la `POST` méthode en tant qu’équivalent par lot de la `GET` méthode décrite ci-dessus pour renvoyer les historiques de cluster de plusieurs identités.

>[!NOTE] La demande ne doit pas comporter plus de 1 000 identités. Les demandes dépassant 1000 identités se traduiront par un code d&#39;état de 400.

**Format d’API**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Corps de requête**

Option 1 : Fournissez une liste de XID pour lesquels récupérer les membres de la grappe.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Option 2 : Fournissez une liste d’identités sous la forme d’identifiants composites, où chacun nomme la valeur d’identification et l’espace de nommage par code d’espace de nommage.

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

**Demande de stub**

L&#39;utilisation de l&#39; `x-uis-cst-ctx: stub` en-tête renvoie une réponse empilée. Il s&#39;agit d&#39;une solution temporaire qui facilitera les progrès rapides du développement de l&#39;intégration, alors que les services sont en cours d&#39;achèvement. Cette mesure sera abandonnée lorsqu&#39;elle n&#39;est plus nécessaire.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**Utilisation de XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Utilisation d’UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

>[!NOTE] La réponse comporte toujours une entrée pour chaque XID fourni dans la requête, que les XID d’une requête appartiennent à la même grappe ou qu’une ou plusieurs d’entre elles soient associées ou non.

## Étapes suivantes

Passez au didacticiel suivant pour découvrir les mappages d&#39;identité des [listes](./list-identity-mappings.md)