---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Préparation des données en vue de les utiliser dans les services intelligents
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 702ac3860e06951574fe48f7d8771a11f68bedc4

---


# Préparation des données en vue de les utiliser dans les services intelligents

Pour que les services intelligents découvrent les informations issues de vos données de marketing, les données doivent être enrichies sémantiquement et conservées dans une structure standard. Les services intelligents tirent parti des  du modèle de données d’expérience (XDM) pour y parvenir. En particulier, tous les jeux de données utilisés dans Intelligent Services doivent être conformes au  XDM **Consumer ExperienceEvent (CEE)** .

Ce fournit des conseils généraux sur le mappage des données de votre marketing de plusieurs à ce. Il présente des informations sur les champs importants duafin de vous aider à déterminer comment mapper efficacement vos données à leur structure.

## Comprendre le CEE 

Le Consumer ExperienceEvent décrit le comportement d’un individu en ce qui concerne les  de marketing numérique (web ou mobile) ainsi que les  de commerce en ligne ou hors ligne. L’utilisation de ce est requise pour les services intelligents en raison de ses champs (colonnes) sémantiquement bien définis, évitant ainsi les noms inconnus qui, autrement, rendraient les données moins claires.

Comme tous les  XDM, le mixin CEE est extensible. En d’autres termes, des champs supplémentaires peuvent être ajoutés au mixin CEE et différentes variantes peuvent être incluses dans plusieurs , si nécessaire.

Un exemple complet du mixin se trouve dans le référentiel [XDM](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)public et doit être utilisé comme référence pour les champs clés décrits dans la section ci-dessous.

## Champs clés

Les sections ci-dessous mettent en évidence les champs clés du mixage CEE qui doivent être utilisés pour que les services intelligents génèrent des informations utiles, y compris des descriptions et des liens vers la documentation de référence pour d’autres exemples.

### xdm:

Ce champ représente le marketing associé à l’événement ExperienceEvent. Le champ contient des informations sur le type de  du, le type de support et le type d’emplacement. **Ce champ _doit_être fourni pour que l’attribut AI fonctionne avec vos données**.

**Exemple de**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:channel`, veuillez vous référer aux [de l&#39;expérience les](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) de. Pour obtenir des exemples de mappages, reportez-vous au [tableau ci-dessous](#example-channels).

#### Exemple de mappage de  de {#example-channels}

Le tableau ci-dessous présente quelques exemples de marketing associés au  `xdm:channel` :

| Canal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Recherche payante | https:/<span>./ns.adobe.com/xdm/-types/search | payé | clicks |
| Social - Marketing | https:/<span>./ns.adobe.com/xdm/-types/social | gagné | clicks |
| Afficher  | https:/<span>./ns.adobe.com/xdm/-types/display | payé | clicks |
| Courriel | https:/<span>./ns.adobe.com/xdm/-types/email | payé | clicks |
|  de interne | https:/<span>./ns.adobe.com/xdm/-types/direct | détenu | clicks |
| Afficher la vue publicitaire | https:/<span>./ns.adobe.com/xdm/-types/display | payé | impressions |
| Redirection du code QR | https:/<span>./ns.adobe.com/xdm/-types/direct | détenu | clicks |
| Mobile | https:/<span>./ns.adobe.com/xdm/-types/mobile | détenu | clicks |

### xdm:productListItems

Ce champ est un tableau d’éléments représentant les produits sélectionnés par un client, y compris le SKU, le nom, le prix et la quantité du produit.

**Exemple de**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:lineItemId": "12345678",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:lineItemId": "48693817",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 80
  }
]
```

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:productListItems`, veuillez consulter les [de détails](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) commerciaux.

### xdm:commerce

Ce champ contient des informations propres au commerce sur ExperienceEvent, notamment le numéro de bon de commande et les informations de paiement.

**Exemple de**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:commerce`, veuillez consulter les [de détails](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) commerciaux.

### xdm:web

Ce champ représente les détails Web relatifs à l’événement ExperienceEvent, tels que l’interaction, les détails de la page et les  du.

**Exemple de**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:productListItems`, reportez-vous aux [de détails Web](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) ExperienceEvent.

### xdm:marketing

Ce champ contient des informations relatives aux  de  marketing qui sont actives avec le point de contact.

**Exemple de**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:productListItems`, veuillez consulter la [spécification sechma](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) marketing.

## Mappage et importation de données

Une fois que vous avez déterminé si vos données de marketing peuvent être mises en correspondance avec le  CEE, vous pouvezle processus d’importation de vos données dans Intelligent Services. Contactez les services de conseil d’Adobe pour vous aider à mapper vos données avec l’ du et à les intégrer au service.

Si vous disposez d’une  Adobe Experience Platform et que vous souhaitez mapper et assimiler les données vous-même, suivez les étapes décrites dans la section ci-dessous.

### Utilisation d’Adobe Experience Platform

>[!NOTE] Les étapes ci-dessous nécessitent un  à la plateforme d’expérience. Si vous n’avez pas accès à la plateforme, passez directement à la section [étapes](#next-steps) suivantes.

Cette section décrit le processus de mappage et d’assimilation des données dans Experience Platform en vue de les utiliser dans Intelligent Services, y compris des liens vers des didacticiels pour obtenir des étapes détaillées.

#### Création d’un  et d’un jeu de données CEE

Lorsque vous êtes prêt à la préparation de vos données pour l’ingestion, la première étape consiste à créer un nouveau XDM  qui utilise le mixin CEE. Les didacticiels suivants décrivent le processus de création d’un nouveau dans l’interface utilisateur ou l’API :

* [Création d’un  dans l’interface utilisateur](../xdm/tutorials/create-schema-ui.md)
* [Création d’un  dans l’API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Les didacticiels ci-dessus suivent un processus générique de création d’un  de. Lors du choix d’une classe pour le  de, vous devez utiliser la classe **XDM ExperienceEvent**. Une fois cette classe choisie, vous pouvez ajouter le mixin CEE au .

Après avoir ajouté le mixin CEE au  du, vous pouvez ajouter d’autres mixins selon les besoins pour les champs supplémentaires de vos données.

Une fois que vous avez créé et enregistré le  de, vous pouvez créer un jeu de données basé sur ce  de. Les didacticiels suivants décrivent le processus de création d’un jeu de données dans l’interface utilisateur ou l’API :

* [Création d’un jeu de données dans l’interface utilisateur](../catalog/datasets/user-guide.md#create) (suivez le flux de travail pour utiliser un  existant)
* [Création d’un jeu de données dans l’API](../catalog/datasets/create.md)

#### Mapper et assimiler des données

Après avoir créé un  CEE et un jeu de données, vous pouvez  le mappage de vos tableaux de données avec lejeu de données et assimiler ces données dans la plateforme. Consultez le didacticiel sur le [mappage d’un fichier CSV à un](../ingestion/tutorials/map-a-csv-file.md) XDM pour savoir comment effectuer cette opération dans l’interface utilisateur. Une fois qu’un jeu de données a été renseigné, il est possible d’utiliser le même jeu de données pour importer des fichiers de données supplémentaires.

## Étapes suivantes {#next-steps}

Ce  fournit des conseils généraux sur la préparation de vos données pour une utilisation dans Intelligent Services. Si vous avez besoin de conseils supplémentaires en fonction de votre cas d’utilisation, contactez l’assistance clientèle d’Adobe.

Une fois que vous avez renseigné un jeu de données avec vos données d’expérience client, vous pouvez utiliser les services intelligents pour générer des informations. Pour commencer, reportez-vous au  suivant :

* [Présentation de l’API d’attribution](./attribution-ai/overview.md)
* [Présentation de Customer AI](./customer-ai/overview.md)
