---
keywords: Experience Platform;accueil;rubriques les plus consultées;identité;identité
solution: Experience Platform
title: Mappages d’identités de liste
topic-legacy: API guide
description: Un mappage est un ensemble regroupant toutes les identités d’un cluster pour un espace de noms spécifié.
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 96%

---

# Répertorier les mappages d’une identité

Un mappage est un ensemble regroupant toutes les identités d’un cluster pour un espace de noms spécifié.

## Obtention d’un mappage d’identité pour une seule identité

Si une identité est définie, récupérez toutes les identités associées issues de l’espace de noms représenté par l’identité dans la requête.

**Format d’API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Requête**

Option 1 : fournissez l’identité comme valeur d’espace de noms (`nsId`, par identifiant) et comme valeur d’identifiant (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2 : fournissez l’identité comme valeur d’espace de noms (`ns`, par nom) et comme valeur d’identifiant (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3 : fournissez l’identité comme XID (`xid`). Pour plus d’informations sur l’obtention du XID d’une identité, consultez la section traitant de l’[obtention du XID pour une identité](./list-native-id.md) dans ce document.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Obtention des mappages d’identité pour plusieurs identités

Afin de récupérer les mappages pour plusieurs identités, utilisez la méthode `POST` comme équivalent par lots de la méthode `GET` décrite ci-dessus.

>[!NOTE]
>
>La requête ne doit pas indiquer plus de 1 000 identités. Les requêtes dépassant les 1 000 identités se traduiront par un code d’état 400.

**Format d’API**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Corps de la requête**

Option 1 : fournissez la liste des XID pour lesquels vous voulez récupérer les mappages.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Option 2 : fournissez une liste d’identités sous forme d’identifiants composites où la valeur d’identifiant et l’espace de noms sont spécifiés par l’identifiant d’espace de noms. Cet exemple illustre l’utilisation de cette méthode lors du remplacement de la valeur par défaut de `graph-type` pour « Private Graph ».

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

**Utilisation des XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids": ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**Utilisation des UID**

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

Si aucune identité associée n’est trouvée pour l’entrée fournie, un code de réponse `HTTP 204` est renvoyé sans contenu.

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

- `lastAssociationTime` : horodatage de la dernière association de l’identité d’entrée à cette identité.
- `regions` : fournit les `regionId` et `lastAssociationTime` pour l’endroit où l’identité a été vue.

## Étapes suivantes

Passez au tutoriel suivant pour [répertorier les espaces de noms disponibles](./list-namespaces.md).
