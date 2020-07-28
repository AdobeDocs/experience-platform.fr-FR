---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Consentement
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---


# Consentement

Certaines réglementations exigeaient un consentement explicite de la part du client avant que ses données personnelles puissent être collectées. Le `/consent` point de terminaison de l’ [!DNL Privacy Service] API vous permet de traiter les demandes de consentement des clients et de les intégrer à votre processus de confidentialité.

Avant d&#39;utiliser ce guide, reportez-vous à la section [prise en main](./getting-started.md) pour obtenir des informations sur les en-têtes d&#39;authentification requis présentés dans l&#39;exemple d&#39;appel d&#39;API ci-dessous.

## Traiter une demande de consentement client

Les demandes de consentement sont traitées en adressant une demande de POST au point de `/consent` terminaison.

**Format d’API**

```http
POST /consent
```

**Requête**

La requête suivante crée une nouvelle tâche de consentement pour les ID d&#39;utilisateur fournis dans la `entities` baie de disques.

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
| `optOutOfSale` | Lorsqu’elle est définie sur true, indique que les utilisateurs fournis dans le `entities` cadre de la section souhaitent se désabonner de la vente ou du partage de leurs données personnelles. |
| `entities` | Tableau d’objets indiquant les utilisateurs auxquels s’applique la demande de consentement. Chaque objet contient un tableau `namespace` et un tableau de `values` correspondance entre des utilisateurs individuels et cet espace de nommage. |
| `nameSpace` | Chaque objet du `entities` tableau doit contenir l&#39;un des espaces de nommage [d&#39;identité](./appendix.md#standard-namespaces) standard reconnus par l&#39;API du Privacy Service. |
| `values` | Tableau de valeurs pour chaque utilisateur, correspondant au `nameSpace`fichier fourni. |

>[!NOTE]
>
>Pour plus d&#39;informations sur la manière de déterminer les valeurs d&#39;identité du client à envoyer à [!DNL Privacy Service], consultez le guide sur la [fourniture de données](../identity-data.md)d&#39;identité.

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) sans charge utile, ce qui indique que la demande a été acceptée par [!DNL Privacy Service] et qu’elle est en cours de traitement.