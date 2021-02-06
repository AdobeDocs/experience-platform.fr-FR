---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Point de terminaison de l’API de consentement
topic: developer guide
description: Découvrez comment gérer les demandes de consentement des clients pour les applications Experience Cloud à l’aide de l’API Privacy Service.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%

---


# Point de terminaison du consentement

Certains règlements exigent un consentement explicite de la part du client avant que ses données personnelles puissent être collectées. Le point de terminaison `/consent` de l&#39;API [!DNL Privacy Service] vous permet de traiter les demandes de consentement des clients et de les intégrer à votre processus de confidentialité.

Avant d&#39;utiliser ce guide, consultez la section [prise en main](./getting-started.md) pour plus d&#39;informations sur les en-têtes d&#39;authentification requis présentés dans l&#39;exemple d&#39;appel d&#39;API ci-dessous.

## Traiter une demande de consentement client

Les demandes de consentement sont traitées en adressant une demande de POST au point de terminaison `/consent`.

**Format d’API**

```http
POST /consent
```

**Requête**

La requête suivante crée une nouvelle tâche de consentement pour les ID utilisateur fournis dans le tableau `entities`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `optOutOfSale` | Lorsqu’elle est définie sur true, indique que les utilisateurs fournis en vertu de `entities` souhaitent s’exclure de la vente ou du partage de leurs données personnelles. |
| `entities` | Tableau d’objets indiquant les utilisateurs auxquels s’applique la demande de consentement. Chaque objet contient un `namespace` et un tableau de `values` pour faire correspondre des utilisateurs individuels à cet espace de nommage. |
| `nameSpace` | Chaque objet du tableau `entities` doit contenir l&#39;un des espaces de nommage d&#39;identité [standard ](./appendix.md#standard-namespaces) reconnus par l&#39;API du Privacy Service. |
| `values` | Tableau de valeurs pour chaque utilisateur, correspondant au `nameSpace` fourni. |

>[!NOTE]
>
>Pour plus d&#39;informations sur la manière de déterminer les valeurs d&#39;identité du client à envoyer à [!DNL Privacy Service], consultez le guide [fournissant des données d&#39;identité](../identity-data.md).

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) sans charge utile, ce qui indique que la demande a été acceptée par [!DNL Privacy Service] et qu’elle est en cours de traitement.