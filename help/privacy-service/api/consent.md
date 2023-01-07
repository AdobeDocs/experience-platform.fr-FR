---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Point de terminaison de l’API de consentement
description: Découvrez comment gérer les demandes de consentement des clients pour les applications Experience Cloud à l’aide de l’API Privacy Service.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 5%

---

# Point de terminaison du consentement

Certaines réglementations exigent un consentement explicite de la part du client avant que leurs données personnelles puissent être collectées. Le `/consent` du point de terminaison [!DNL Privacy Service] L’API vous permet de traiter les demandes de consentement des clients et de les intégrer à votre workflow de confidentialité.

Avant d’utiliser ce guide, reportez-vous à la section [prise en main](./getting-started.md) guide pour plus d’informations sur les en-têtes d’authentification requis présentés dans l’exemple d’appel API ci-dessous.

## Traitement d’une demande de consentement du client

Les demandes de consentement sont traitées en adressant une requête de POST à la fonction `/consent` point de terminaison .

**Format d’API**

```http
POST /consent
```

**Requête**

La requête suivante crée une tâche de consentement pour les ID utilisateur fournis dans la variable `entities` tableau.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `optOutOfSale` | Lorsqu’elle est définie sur true, indique que les utilisateurs ont fourni `entities` vous souhaitez vous exclure de la vente ou du partage de leurs données personnelles. |
| `entities` | Tableau d’objets indiquant les utilisateurs auxquels s’applique la demande de consentement. Chaque objet contient une `namespace` et un tableau de `values` pour associer des utilisateurs individuels à cet espace de noms. |
| `nameSpace` | Chaque objet de la variable `entities` Le tableau doit contenir l’un des [espaces de noms d’identité standard](./appendix.md#standard-namespaces) reconnu par l’API du Privacy Service. |
| `values` | Tableau de valeurs pour chaque utilisateur, correspondant au `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Pour plus d’informations sur la manière de déterminer les valeurs d’identité du client à envoyer à [!DNL Privacy Service], reportez-vous au guide sur la [fournir des données d’identité](../identity-data.md).

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) sans payload, indiquant que la requête a été acceptée par [!DNL Privacy Service] et est en cours de traitement.
