---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Point de terminaison de l’API de consentement
topic-legacy: developer guide
description: Découvrez comment gérer les demandes de consentement client pour les applications Experience Cloud à l’aide de l’API Privacy Service.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 5%

---

# Point de terminaison du consentement

Certains règlements exigent un consentement explicite de la part des clients avant que leurs données personnelles puissent être collectées. Le `/consent` point de terminaison dans le noeud [!DNL Privacy Service] L’API vous permet de traiter les demandes de consentement client et de les intégrer à votre flux de travaux de confidentialité.

Avant d’utiliser ce guide, veuillez vous référer au [prise en main](./getting-started.md) pour plus d’informations sur les en-têtes d’authentification requis présentés dans l’exemple d’appel d’API ci-dessous.

## Traitement d’une demande de consentement client

Les demandes de consentement sont traitées en adressant une demande de POST à la `/consent` point de terminaison.

**Format d’API**

```http
POST /consent
```

**Requête**

La demande suivante crée une nouvelle tâche de consentement pour les ID d’utilisateur fournis dans le fichier `entities` tableau.

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
| `optOutOfSale` | Lorsqu’elle est définie sur true, indique que les utilisateurs fournis sous `entities` souhaite renoncer à la vente ou au partage de leurs données personnelles. |
| `entities` | Tableau d’objets indiquant les utilisateurs auxquels la demande de consentement s’applique. Chaque objet contient un `namespace` et un tableau de `values` pour associer des utilisateurs individuels à cet espace de noms. |
| `nameSpace` | Chaque objet dans le noeud `entities` doit contenir l&#39;un des éléments suivants : [espaces de noms d’identité standard](./appendix.md#standard-namespaces) reconnu par l’API du Privacy Service. |
| `values` | Un tableau de valeurs pour chaque utilisateur, correspondant à la `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Pour plus d’informations sur la manière de déterminer les valeurs d’identité client à envoyer à [!DNL Privacy Service], consultez le guide sur [fourniture de données d’identité](../identity-data.md).

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) sans charge utile, indiquant que la demande a été acceptée par [!DNL Privacy Service] et est en cours de traitement.
