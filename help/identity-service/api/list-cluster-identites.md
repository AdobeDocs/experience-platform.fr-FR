---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identités des grappes de Listes
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 1%

---


# Liste de toutes les identités dans une grappe

Les identités liées dans un graphique d&#39;identité, quel que soit l&#39;espace de nommage, sont considérées comme faisant partie du même &quot;cluster&quot; dans ce graphique d&#39;identité. Les options ci-dessous permettent d’accéder à tous les membres de la grappe.

## Obtenir les identités associées pour une seule identité

Récupérez tous les membres de la grappe pour une seule identité.

Vous pouvez utiliser le `graph-type` paramètre facultatif pour indiquer le graphique d’identité à partir duquel la grappe doit être créée. Les options sont les suivantes :

- Aucun - N’effectuez aucune assemblage d’identité.
- Graphique privé - Effectuez un assemblage d&#39;identité en fonction de votre graphique d&#39;identité privée. Si aucun `graph-type` paramètre n’est fourni, il s’agit de la valeur par défaut.

**Format d’API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Requête**

Option 1 : Fournissez l’identité sous forme d’espace de nommage (`nsId`, par ID) et de valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2 : Fournissez l’identité sous forme d’espace de nommage (`ns`, par nom) et de valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3 : Fournissez l’identité sous la forme XID (`xid`). Pour plus d&#39;informations sur la façon d&#39;obtenir le XID d&#39;une identité, consultez la section de ce document qui traite de l&#39; [obtention du XID pour une identité](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obtenir les identités associées pour plusieurs identités

Utilisez `POST` comme équivalent par lot de la `GET` méthode décrite ci-dessus pour renvoyer les identités dans les grappes de plusieurs identités.

>[!NOTE] La demande ne doit pas comporter plus de 1 000 identités. Les demandes dépassant 1000 identités se traduiront par un code d&#39;état de 400.

**Format d’API**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Requête**

La requête suivante montre comment fournir une liste de XID pour laquelle récupérer les membres de la grappe.

**Demande de stub**

L&#39;utilisation de l&#39; `x-uis-cst-ctx: stub` en-tête renvoie une réponse empilée. Il s&#39;agit d&#39;une solution temporaire qui facilitera les progrès rapides du développement de l&#39;intégration, alors que les services sont en cours d&#39;achèvement. Cette mesure sera abandonnée lorsqu&#39;elle n&#39;est plus nécessaire.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**Appel à l’aide de XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Appel à l’aide d’UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Réponse &quot;coincée&quot;**

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

>[!NOTE] La réponse comporte toujours une entrée pour chaque XID fourni dans la requête, que les XID d’une requête appartiennent à la même grappe ou qu’une ou plusieurs d’entre elles soient associées ou non.

## Étapes suivantes

Passez au didacticiel suivant pour [liste de l&#39;historique de cluster d&#39;une identité](./list-cluster-history.md)