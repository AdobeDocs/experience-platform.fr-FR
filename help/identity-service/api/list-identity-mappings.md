---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mappages d'identité des Listes
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 3%

---


# Mappages d&#39;identité des Listes

Un mappage est un ensemble de toutes les identités d’une grappe, pour un espace de nommage spécifié.

## Obtenir un mappage d&#39;identité pour une seule identité

Si une identité est définie, récupérez toutes les identités associées du même espace de nommage que celles représentées par l’identité dans la demande.

**Format d’API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Requête**

Option 1 : Fournissez l’identité sous forme d’espace de nommage (`nsId`, par ID) et de valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2 : Fournissez l’identité sous forme d’espace de nommage (`ns`, par nom) et de valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3 : Fournissez l’identité sous la forme XID (`xid`). Pour plus d&#39;informations sur la façon d&#39;obtenir le XID d&#39;une identité, consultez la section de ce document qui traite de l&#39; [obtention du XID pour une identité](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Obtenir des mappages d’identité pour plusieurs identités

Utilisez la `POST` méthode en tant qu’équivalent par lot de la `GET` méthode décrite ci-dessus pour récupérer les mappages pour plusieurs identités.

>[!NOTE]
>
>La demande ne doit pas comporter plus de 1 000 identités. Les demandes dépassant 1000 identités se traduiront par un code d&#39;état de 400.

**Format d’API**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Corps de requête**

Option 1 : Fournissez une liste de XID pour lesquels récupérer les mappages.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Option 2 : Fournissez une liste d’identités sous la forme d’identifiants composites, où chacun nomme la valeur d’identification et l’espace de nommage par identifiant d’espace de nommage. Cet exemple illustre l&#39;utilisation de cette méthode lors du remplacement de la valeur par défaut `graph-type` de &quot;Graphique privé&quot;.

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**Requête**

**Utilisation de XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids" : ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**Utilisation d’UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
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
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

Si aucune identité associée n’a été trouvée avec l’entrée fournie, un code de `HTTP 204` réponse est renvoyé sans contenu.

**Réponse**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`: Horodatage de la dernière association de l&#39;identité d&#39;entrée à cette identité.
- `regions`: Fournit les informations `regionId` et `lastAssociationTime` pour l&#39;endroit où l&#39;identité a été vue.

## Étapes suivantes

Passez au didacticiel suivant pour [liste des espaces de nommage](./list-namespaces.md)disponibles.
