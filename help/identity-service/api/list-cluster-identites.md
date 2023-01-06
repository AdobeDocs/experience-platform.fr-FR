---
keywords: Experience Platform;accueil;rubriques les plus consultées;identités de liste;liste de clusters
solution: Experience Platform
title: Liste de toutes les identités d’un cluster
description: Les identités qui sont liées dans un graphique d’identités, et ce quel que soit l’espace de noms, sont considérées comme faisant partie du même « cluster » dans ce graphique d’identités. Les options ci-dessous permettent d’accéder à tous les membres du cluster.
exl-id: 0fb9eac9-2dc2-4881-8598-02b3053d0b31
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 95%

---

# Répertorier toutes les identités d’un cluster

Les identités qui sont liées dans un graphique d’identités, et ce quel que soit l’espace de noms, sont considérées comme faisant partie du même « cluster » dans ce graphique d’identités. Les options ci-dessous permettent d’accéder à tous les membres du cluster.

## Obtention des identités associées pour une identité unique

Récupérez tous les membres du cluster pour une identité unique.

Vous pouvez utiliser le paramètre `graph-type` facultatif pour indiquer le graphique d’identités duquel doit provenir le cluster. Les options sont les suivantes :

- Aucun - Ne réalisez aucune combinaison d’identités.
- Graphique privé - Effectuez des combinaisons d’identités depuis votre graphique d’identités privé. Il s’agit de la valeur par défaut si aucune valeur `graph-type` n’est renseignée.

**Format d’API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Requête**

Option 1 : fournissez l’identité comme valeur d’espace de noms (`nsId`, par identifiant) et comme valeur d’identifiant (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2 : fournissez l’identité comme valeur d’espace de noms (`ns`, par nom) et comme valeur d’identifiant (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3 : fournissez l’identité comme XID (`xid`). Pour plus d’informations sur l’obtention du XID d’une identité, consultez la section traitant de l’[obtention du XID pour une identité](./list-native-id.md) dans ce document.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obtention des identités associées pour des identités multiples

Utilisez `POST` comme équivalent de lot de la méthode `GET` décrite ci-dessus pour renvoyer les identités dans les clusters d’identités multiples.

>[!NOTE]
>
>La requête ne doit pas indiquer plus de 1 000 identités. Les requêtes dépassant les 1 000 identités se traduiront par un code d’état 400.

**Format d’API**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Requête**

La requête suivante illustre comment fournir une liste de XID pour lesquels récupérer les membres du cluster.

**Requête avec bouchon**

L’utilisation de l’en-tête `x-uis-cst-ctx: stub` renverra une réponse bouchonnée. Il s’agit là d’une solution temporaire qui facilite le développement rapide de l’intégration pendant que les services sont en cours d’achèvement. Cette solution deviendra obsolète lorsqu’elle ne sera plus nécessaire.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**Appel avec des XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Appel avec des UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Réponse « bouchonnée »**

```json
{
   "version": 1,
   "clusters": [{
           "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": ["e8138f65-d3d3-4485-a7e1-6712e047349d", "21312343536983537571245438594"],
           "members": [{
                   "nsid": 0,
                   "id": "27064814400205787570627663430729680462"
               },
               {
                   "nsid": 411,
                   "id": "86826386186182763871263871263876128612"
               }
           ]
       },
       {
           "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [],
           "members": []
       }
   ],
   "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
   "unprocessedNids": [{
       "nsid": 411,
       "id": "WY-RNgAAArI4rGBo"
   }]
}
```

**Réponse complète**

```json
{
   "unprocessedXids": [],
   "unprocessedNids": [],
   "version": "1.0.0",
   "clusters": [{
           "xid": "411|WRbM7AAAAJ_PBZHl",
           "members": [
               "411|WRbM7AAAAJ_PBZHl",
               "0|47713142741924778930324734610798294416"
           ],
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [{
                   "nsid": 411,
                   "id": "WRbM7AAAAJ_PBZHl"
               },
               {
                   "nsid": 0,
                   "id": "47713142741924778930324734610798294416"
               }
           ]
       },
       {
           "xid": "411|WY-RNgAAArI4rGBo",
           "compositeXid": {
               "nsid": 411,
               "id": "WY-RNgAAArI4rGBo"
           },
           "members": [
               "411|WY-RNgAAArI4rGBo",
               "411|WY-RNgAAArI4rGGy"
           ],
           "members": [{
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGBo"
               },
               {
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGGy"
               }
           ]

       }
   ]
}
```

>[!NOTE]
>
>La réponse comportera toujours une entrée pour chaque XID fourni dans la requête, que les XID d’une requête appartiennent au même cluster ou qu’un ou plusieurs clusters y soient associés.

## Étapes suivantes

Passez au tutoriel suivant pour [répertorier l’historique des clusters d’une identité](./list-cluster-history.md)
