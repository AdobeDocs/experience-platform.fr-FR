---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Identités de la grappe '
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


#  toutes les identités dans une grappe

Les identités qui sont liées dans un graphique d’identité, quel que soit  , sont considérées comme faisant partie du même &quot;cluster&quot; dans ce graphique d’identité. Les options ci-dessous fournissent les moyens d’accéder à tous les membres de la grappe.

## Obtenir les identités associées pour une identité unique

Récupérez tous les membres de la grappe pour une identité unique.

Vous pouvez utiliser le `graph-type` paramètre facultatif pour indiquer le graphique d’identité à partir duquel la grappe est issue. Les options sont les suivantes :

- Aucun - Ne faites aucun assemblage d’identité.
- Graphique privé - Effectuez des assemblages d&#39;identité en fonction du graphique de votre identité privée. Si aucune `graph-type` valeur n’est fournie, il s’agit de la valeur par défaut.

**Format API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Requête**

Option 1 : Fournissez l’identité sous la forme   (`nsId`, par ID) et valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2 : Fournissez l’identité sous la forme   (`ns`, par nom) et valeur d’ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3 : Fournissez l’identité sous la forme XID (`xid`). Pour plus d’informations sur la manière d’obtenir le XID d’une identité, consultez la section de ce qui traite de l’ [obtention du XID pour une identité](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obtenir les identités associées pour plusieurs identités

Utilisez `POST` comme équivalent de lot de la `GET` méthode décrite ci-dessus pour renvoyer les identités dans les grappes d’identités multiples.

>[!NOTE] La demande ne doit pas indiquer plus de 1 000 identités au maximum. Les demandes dépassant 1000 identités se traduiront par 400 codes d&#39;état.

**Format API**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Requête**

La requête suivante montre comment fournir un de XID pour lequel récupérer les membres de la grappe.

**Demande de stub**

L’utilisation de `x-uis-cst-ctx: stub` l’en-tête renverra une réponse empilée. Il s&#39;agit là d&#39;une solution temporaire pour faciliter le développement rapide de l&#39;intégration, pendant que les services sont achevés. Cette mesure sera abandonnée lorsqu’elle n’est plus nécessaire.

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

**Réponse &quot;Stubbed&quot;**

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

>[!NOTE] La réponse comporte toujours une entrée pour chaque XID fourni dans la requête, que les XID d’une requête appartiennent à la même grappe ou qu’une ou plusieurs d’entre elles soient associées à une grappe.

## Étapes suivantes

Passez au didacticiel suivant pour [de l’historique de grappe d’une identité](./list-cluster-history.md)