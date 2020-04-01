---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Obtention de l’historique de cluster d’une identité
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Obtention de l’historique de cluster d’une identité

Les identités peuvent déplacer des grappes au cours de différentes exécutions de graphiques de périphériques. Identity Service offre une visibilité sur les associations de cluster d’une identité donnée au fil du temps.

Utilisez un `graph-type` paramètre facultatif pour indiquer le type de sortie à partir duquel obtenir la grappe. Les options sont les suivantes :

- `None` - Ne pas procéder à l&#39;assemblage d&#39;identité.
- `Private Graph` - Effectuez des assemblages d&#39;identité sur la base du graphique de votre identité privée. Si aucune `graph-type` valeur n’est fournie, il s’agit de la valeur par défaut.

## Obtention de l’historique de cluster d’une identité unique

**Format API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Requête**

Option 1 : Fournissez l’identité sous la forme   (`nsId`, par ID) et valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2 : Fournissez l’identité sous la forme   (`ns`, par nom) et valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3 : Fournissez l’identité sous la forme XID (`xid`). Pour plus d’informations sur la manière d’obtenir le XID d’une identité, consultez la section de ce qui traite de l’ [obtention du XID pour une identité](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obtention de l’historique de cluster d’une multitude d’identités

Utilisez la `POST` méthode comme équivalent par lot de la `GET` méthode décrite ci-dessus pour renvoyer les historiques de cluster de plusieurs identités.

>[!NOTE] La demande ne doit pas indiquer plus de 1 000 identités au maximum. Les demandes dépassant 1000 identités se traduiront par 400 codes d&#39;état.

**Format API**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Corps de requête**

Option 1 : Fournissez un de XID pour lesquels récupérer les membres de la grappe.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Option 2 : Fournissez un d’identités sous la forme d’identifiants composites, où chacun nomme la valeur d’ID et  l’par le code de.

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

L’utilisation de `x-uis-cst-ctx: stub` l’en-tête renverra une réponse empilée. Il s&#39;agit là d&#39;une solution temporaire pour faciliter le développement rapide de l&#39;intégration, pendant que les services sont achevés. Cette mesure sera abandonnée lorsqu’elle n’est plus nécessaire.

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

>[!NOTE] La réponse comporte toujours une entrée pour chaque XID fourni dans la requête, que les XID d’une requête appartiennent à la même grappe ou qu’une ou plusieurs d’entre elles soient associées à une grappe.

## Étapes suivantes

Passez au didacticiel suivant pour [et mappages d’identité](./list-identity-mappings.md)