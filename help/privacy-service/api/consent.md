---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Consentement
topic: developer guide
translation-type: tm+mt
source-git-commit: a3178ab54a7ab5eacd6c5f605b8bd894779f9e85
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%

---


# Consentement

Certaines réglementations exigeaient un consentement explicite de la part du client avant que ses données personnelles puissent être collectées. Le `/consent` point de terminaison de l’API Privacy Service vous permet de traiter les demandes de consentement des clients et de les intégrer à votre processus de confidentialité.

Avant d&#39;utiliser ce guide, reportez-vous à la section [prise en main](./getting-started.md) pour obtenir des informations sur les en-têtes d&#39;authentification requis présentés dans l&#39;exemple d&#39;appel d&#39;API ci-dessous.

## Traiter une demande de consentement client

Les demandes de consentement sont traitées en envoyant une demande POST au point de `/consent` terminaison.

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
| `nameSpace` | Chaque objet de la `entities` baie doit contenir l&#39;un des espaces de nommage [d&#39;identité](./appendix.md#standard-namespaces) standard reconnus par l&#39;API Privacy Service. |
| `values` | Tableau de valeurs pour chaque utilisateur, correspondant au `nameSpace`fichier fourni. |

>[!NOTE] Pour plus d’informations sur la façon de déterminer les valeurs d’identité du client à envoyer à Privacy Service, consultez le guide sur la [fourniture de données](../identity-data.md)d’identité.

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) sans charge utile, ce qui indique que la demande a été acceptée par Privacy Service et qu’elle est en cours de traitement.