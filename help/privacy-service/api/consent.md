---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Point d’entrée de l’API de consentement
description: Découvrez comment gérer les demandes de consentement des clients pour les applications Experience Cloud à l’aide de l’API Privacy Service.
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
TQID: https://experienceleague.adobe.com/P9SG8xvWJrIX2qo6hZrrK4SrSTTk0dBK8VHBA2WxLJM
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 246
ht-degree: 4%

---

# Point d’entrée de consentement

Certaines réglementations nécessitent le consentement explicite du client avant que ses données personnelles puissent être collectées. Le point d’entrée `/consent` de l’API [!DNL Privacy Service] vous permet de traiter les demandes de consentement des clients et de les intégrer à votre workflow de confidentialité.

Avant d’utiliser ce guide, reportez-vous au guide [prise en main](./getting-started.md) pour plus d’informations sur les en-têtes d’authentification requis présentés dans l’exemple d’appel API ci-dessous.

## Traiter une demande de consentement client

Les demandes de consentement sont traitées en adressant une requête POST au point d’entrée `/consent`.

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
| `optOutOfSale` | Lorsque la valeur est définie sur true, indique que les utilisateurs fournis sous `entities` souhaitent s’exclure de la vente ou du partage de leurs données personnelles. |
| `entities` | Tableau d’objets indiquant les utilisateurs auxquels la demande de consentement s’applique. Chaque objet contient un `namespace` et un tableau de `values` pour faire correspondre des utilisateurs individuels avec cet espace de noms. |
| `nameSpace` | Chaque objet du tableau de `entities` doit contenir l’un des [espaces de noms d’identité standard](./appendix.md#standard-namespaces) reconnus par l’API Privacy Service. |
| `values` | Tableau de valeurs pour chaque utilisateur, correspondant au `nameSpace` fourni. |

{style="table-layout:auto"}

>[!NOTE]
>
>Pour plus d’informations sur la manière de déterminer les valeurs d’identité client à envoyer à [!DNL Privacy Service], consultez le guide sur la [fourniture de données d’identité](../identity-data.md).

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) sans payload, indiquant que la requête a été acceptée par [!DNL Privacy Service] et est en cours de traitement.
