---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Point de terminaison de l’API de consentement
description: Découvrez comment gérer les demandes de consentement des clients pour les applications Experience Cloud à l’aide de l’API Privacy Service.
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 4%

---

# Point de terminaison du consentement

Certaines réglementations exigent un consentement explicite de la part du client avant que leurs données personnelles puissent être collectées. Le point d’entrée `/consent` de l’API [!DNL Privacy Service] vous permet de traiter les demandes de consentement des clients et de les intégrer à votre workflow de confidentialité.

Avant d’utiliser ce guide, reportez-vous au guide de [prise en main](./getting-started.md) pour plus d’informations sur les en-têtes d’authentification requis présentés dans l’exemple d’appel API ci-dessous.

## Traitement d’une demande de consentement du client

Les demandes de consentement sont traitées en envoyant une requête de POST au point de terminaison `/consent`.

**Format d’API**

```http
POST /consent
```

**Requête**

La requête suivante crée une tâche de consentement pour les ID utilisateur fournis dans le tableau `entities`.

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
| `optOutOfSale` | Lorsqu’elle est définie sur true, indique que les utilisateurs fournis sous `entities` souhaitent se désinscrire de la vente ou du partage de leurs données personnelles. |
| `entities` | Tableau d’objets indiquant les utilisateurs auxquels s’applique la demande de consentement. Chaque objet contient un `namespace` et un tableau de `values` pour faire correspondre des utilisateurs individuels à cet espace de noms. |
| `nameSpace` | Chaque objet du tableau `entities` doit contenir l’un des [ espaces de noms d’identité standard](./appendix.md#standard-namespaces) reconnus par l’API du Privacy Service. |
| `values` | Un tableau de valeurs pour chaque utilisateur, correspondant au `nameSpace` fourni. |

{style="table-layout:auto"}

>[!NOTE]
>
>Pour plus d&#39;informations sur la manière de déterminer les valeurs d&#39;identité du client à envoyer à [!DNL Privacy Service], consultez le guide sur la [fourniture de données d&#39;identité](../identity-data.md).

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) sans payload, indiquant que la requête a été acceptée par [!DNL Privacy Service] et qu’elle est en cours de traitement.
