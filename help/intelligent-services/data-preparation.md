---
keywords: Experience Platform ; accueil ; services intelligents ; sujets populaires ; service intelligent ; service intelligent
solution: Experience Platform, Intelligent Services
title: Préparation des données en vue de leur utilisation dans les services intelligents
topic: Intelligent Services
description: 'Pour que les services intelligents puissent découvrir des informations issues de vos données de événement marketing, les données doivent être enrichies et conservées de manière sémantique dans une structure standard. Les services intelligents tirent parti des schémas du modèle de données d’expérience (XDM) pour y parvenir. Plus précisément, tous les jeux de données utilisés dans Intelligent Services] doivent être conformes au schéma XDM Consumer ExperienceEvent (CEE). '
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 2%

---


# Préparer les données à utiliser dans [!DNL Intelligent Services]

Pour que [!DNL Intelligent Services] puisse découvrir des informations issues des données de vos événements marketing, les données doivent être enrichies et conservées sémantiquement dans une structure standard. [!DNL Intelligent Services] exploiter  [!DNL Experience Data Model] (XDM) les schémas pour y parvenir. En particulier, tous les jeux de données utilisés dans [!DNL Intelligent Services] doivent être conformes au schéma XDM de Consumer ExperienceEvent (CEE).

Ce document fournit des conseils généraux sur le mappage des données de vos événements marketing de plusieurs canaux à ce schéma, en décrivant les informations sur les champs importants du schéma afin de vous aider à déterminer comment mapper efficacement vos données à leur structure.

## Résumé du flux de travail

Le processus de préparation varie selon que vos données sont stockées dans Adobe Experience Platform ou en externe. Cette section résume les étapes nécessaires à suivre, selon l&#39;un ou l&#39;autre scénario.

### Préparation de données externes

Si vos données sont stockées en dehors de [!DNL Experience Platform], procédez comme suit :

1. Contactez les services de conseil en Adobe pour demander des informations d&#39;identification d&#39;accès pour un conteneur d&#39;Enregistrement Azure Blob dédié.
1. A l’aide de vos informations d’identification d’accès, téléchargez vos données vers le conteneur Blob.
1. Travaillez avec les services de conseil en Adobe pour faire correspondre vos données au [schéma Consumer ExperienceEvent](#cee-schema) et les assimiler à [!DNL Intelligent Services].

### [!DNL Experience Platform] préparation des données

Si vos données sont déjà stockées dans [!DNL Platform], procédez comme suit :

1. Examinez la structure du [schéma Consumer ExperienceEvent](#cee-schema) et déterminez si vos données peuvent être mises en correspondance avec ses champs.
1. Contactez les Services de conseil en Adobe pour vous aider à mapper vos données au schéma et à les intégrer dans [!DNL Intelligent Services], ou [suivez les étapes décrites dans ce guide](#mapping) si vous souhaitez mapper les données vous-même.

## Comprendre le schéma CEE {#cee-schema}

Le schéma Consumer ExperienceEvent décrit le comportement d’une personne en ce qui concerne les événements de marketing numérique (Web ou mobile) ainsi que l’activité de commerce en ligne ou hors ligne. L&#39;utilisation de ce schéma est requise pour [!DNL Intelligent Services] en raison de ses champs (colonnes) sémantiquement bien définis, en évitant les noms inconnus qui autrement rendraient les données moins claires.

Le schéma CEE, comme tous les schémas XDM ExperienceEvent, capture l’état du système basé sur les séries chronologiques lorsqu’un événement (ou un ensemble de événements) s’est produit, y compris le moment et l’identité du sujet concerné. Les Événements d&#39;expérience sont des données factuelles de ce qui s&#39;est passé, et ils sont donc immuables et représentent ce qui s&#39;est passé sans agrégation ni interprétation.

[!DNL Intelligent Services] utilisez plusieurs champs clés de ce schéma pour générer des informations à partir des données de vos événements marketing, qui se trouvent tous au niveau racine et sont développés pour afficher leurs sous-champs requis.

![](./images/data-preparation/schema-expansion.gif)

Comme tous les schémas XDM, le mixin CEE est extensible. En d’autres termes, des champs supplémentaires peuvent être ajoutés au mixin CEE et différentes variantes peuvent être incluses dans plusieurs schémas si nécessaire.

Vous trouverez un exemple complet du mixin dans le [référentiel XDM public](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). En outre, vous pouvez vue et copier le [fichier JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) suivant pour obtenir un exemple de la manière dont les données peuvent être structurées pour se conformer au schéma CEE. Reportez-vous à ces deux exemples au fur et à mesure que vous découvrirez les champs clés décrits dans la section ci-dessous, afin de déterminer comment mapper vos propres données au schéma.

## Champs clés

Il existe plusieurs champs clés dans le mixin CEE qui doivent être utilisés pour que [!DNL Intelligent Services] puisse générer des informations utiles. Cette section décrit le cas d’utilisation et les données attendues pour ces champs et fournit des liens vers la documentation de référence pour d’autres exemples.

### Champs obligatoires

Bien que l&#39;utilisation de tous les champs clés soit fortement recommandée, il existe deux champs **requis** pour que [!DNL Intelligent Services] fonctionne :

* [Un champ d&#39;identité Principal](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:canal](#channel)  (obligatoire uniquement pour l’Attribution AI)

#### Identité Principal {#identity}

L&#39;un des champs de votre schéma doit être défini en tant que champ d&#39;identité Principal, ce qui permet à [!DNL Intelligent Services] de lier chaque instance de données de séries chronologiques à une personne.

Vous devez déterminer le meilleur champ à utiliser comme identité Principale en fonction de la source et de la nature de vos données. Un champ d&#39;identité doit inclure un **espace de nommage d&#39;identité** qui indique le type de données d&#39;identité que le champ attend comme valeur. Certaines valeurs d’espace de nommage valides sont les suivantes :

* &quot;e-mail&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (pour les Adobe Audience Manager ID)
* &quot;aid&quot; (pour les identifiants Adobe Analytics)

Si vous ne savez pas quel champ vous devez utiliser comme Principale identité, contactez les Services de conseil en Adobe pour déterminer la meilleure solution.

#### xdm:timestamp {#timestamp}

Ce champ représente la date et l&#39;heure auxquelles le événement s&#39;est produit. Cette valeur doit être fournie sous forme de chaîne, conformément à la norme ISO 8601.

#### xdm:channel {#channel}

>[!NOTE]
>
>Ce champ n’est obligatoire que lorsque vous utilisez Attribution AI.

Ce champ représente le canal marketing associé à ExperienceEvent. Ce champ contient des informations sur le type de canal, le type de support et le type d’emplacement.

![](./images/data-preparation/channel.png)

**Exemple de schéma**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:channel`, consultez la section [schéma du canal d’expérience](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md). Pour obtenir des exemples de mappages, voir le [tableau ci-dessous](#example-channels).

##### Exemple de mappages de canal {#example-channels}

Le tableau suivant fournit quelques exemples de canaux marketing mappés au schéma `xdm:channel` :

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Recherche payante | https:/<span>/ns.adobe.com/xdm/canal-types/search | payé | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/canal-types/social | gagné | clics |
| Afficher | https:/<span>/ns.adobe.com/xdm/canal-types/display | payé | clics |
| E-mail | https:/<span>/ns.adobe.com/xdm/canal-types/email | payé | clics |
| Parrain interne | https:/<span>/ns.adobe.com/xdm/canal-types/direct | détenu | clics |
| Afficher la vue publicitaire | https:/<span>/ns.adobe.com/xdm/canal-types/display | payé | impressions |
| Redirection du code QR | https:/<span>/ns.adobe.com/xdm/canal-types/direct | détenu | clics |
| Mobile | https:/<span>/ns.adobe.com/xdm/canal-types/mobile | détenu | clics |

### Champs recommandés

Les autres champs clés sont décrits dans cette section. Bien que ces champs ne soient pas nécessairement nécessaires pour que [!DNL Intelligent Services] fonctionne, il est fortement recommandé d’en utiliser autant que possible pour obtenir des informations plus précises.

#### xdm:productListItems

Ce champ est un tableau d&#39;articles qui représentent les produits sélectionnés par un client, y compris le SKU, le nom, le prix et la quantité du produit.

![](./images/data-preparation/productListItems.png)

**Exemple de schéma**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:productListItems`, consultez la section [schéma des détails commerciaux](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:commerce

Ce champ contient des informations propres au commerce sur ExperienceEvent, notamment le numéro de bon de commande et les informations de paiement.

![](./images/data-preparation/commerce.png)

**Exemple de schéma**

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

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:commerce`, consultez la section [schéma des détails commerciaux](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:web

Ce champ représente les détails Web relatifs à ExperienceEvent, tels que l’interaction, les détails de la page et le parrain.

![](./images/data-preparation/web.png)

**Exemple de schéma**

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

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:productListItems`, consultez la section [Détails Web d’ExperienceEvent ](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) du schéma .

#### xdm:marketing

Ce champ contient des informations relatives aux activités marketing qui sont principales avec le point de contact.

![](./images/data-preparation/marketing.png)

**Exemple de schéma**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:productListItems`, consultez la section [sechma marketing](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md).

## Mappage et assimilation de données {#mapping}

Une fois que vous avez déterminé si les données de vos événements marketing peuvent être mises en correspondance avec le schéma CEE, l’étape suivante consiste à déterminer les données à importer dans [!DNL Intelligent Services]. Toutes les données historiques utilisées dans [!DNL Intelligent Services] doivent se situer dans la période minimale de quatre mois de données, plus le nombre de jours prévus comme période de consultation.

Après avoir décidé de la plage de données à envoyer, contactez les services de conseil en Adobe pour aider à faire correspondre vos données au schéma et à les intégrer au service.

Si vous disposez d&#39;un abonnement [!DNL Adobe Experience Platform] et souhaitez mapper et assimiler les données vous-même, suivez les étapes décrites dans la section ci-dessous.

### Utilisation de Adobe Experience Platform

>[!NOTE]
>
>Les étapes ci-dessous nécessitent un abonnement à l&#39;Experience Platform. Si vous n&#39;avez pas accès à la plate-forme, passez directement à la section [étapes suivantes](#next-steps).

Cette section décrit le processus de mappage et d&#39;assimilation de données dans l&#39;Experience Platform en vue de leur utilisation dans [!DNL Intelligent Services], y compris les liens vers des didacticiels pour obtenir des étapes détaillées.

#### Créer un schéma et un jeu de données CEE

Lorsque vous êtes prêt à début pour préparer vos données pour l&#39;assimilation, la première étape consiste à créer un nouveau schéma XDM qui utilise le mixin CEE. Les didacticiels suivants décrivent le processus de création d’un schéma dans l’interface utilisateur ou l’API :

* [Création d’un schéma dans l’interface utilisateur](../xdm/tutorials/create-schema-ui.md)
* [Création d’un schéma dans l’API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Les didacticiels ci-dessus suivent un processus générique de création d’un schéma. Lorsque vous choisissez une classe pour le schéma, vous devez utiliser la **classe XDM ExperienceEvent**. Une fois cette classe choisie, vous pouvez ajouter le mixin CEE au schéma.

Après avoir ajouté le mixin CEE au schéma, vous pouvez ajouter d’autres mixins en fonction des champs supplémentaires de vos données.

Une fois le schéma créé et enregistré, vous pouvez créer un jeu de données basé sur ce schéma. Les didacticiels suivants décrivent le processus de création d’un nouveau jeu de données dans l’interface utilisateur ou l’API :

* [Créer un jeu de données dans l’interface utilisateur](../catalog/datasets/user-guide.md#create)  (Suivez le processus pour utiliser un schéma existant)
* [Création d’un jeu de données dans l’API](../catalog/datasets/create.md)

Une fois le jeu de données créé, vous pouvez le trouver dans l&#39;interface utilisateur de la plate-forme dans l&#39;espace de travail **[!UICONTROL Datasets]**.

![](images/data-preparation/dataset-location.png)

#### Ajouter les champs d&#39;identité au jeu de données

Si vous importez des données de [!DNL Adobe Audience Manager], [!DNL Adobe Analytics] ou d&#39;une autre source externe, vous avez la possibilité de définir un champ de schéma comme champ d&#39;identité. Pour définir un champ de schéma en tant que champ d’identité, vue la section relative à la définition des champs d’identité dans le [didacticiel d’interface utilisateur](../xdm/tutorials/create-schema-ui.md#identity-field) ou le [didacticiel d’API](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) pour la création d’un schéma.

Si vous importez des données à partir d’un fichier CSV local, vous pouvez passer à la section suivante sur [le mappage et l’assimilation des données](#ingest).

#### Mapper et assimiler des données {#ingest}

Après avoir créé un schéma CEE et un jeu de données, vous pouvez début de mappage de vos tables de données sur le schéma et d’assimiler ces données dans la plate-forme. Consultez le didacticiel sur le [mappage d’un fichier CSV à un schéma XDM](../ingestion/tutorials/map-a-csv-file.md) pour connaître les étapes à suivre dans l’interface utilisateur. Vous pouvez utiliser le [fichier JSON exemple](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) suivant pour tester le processus d’assimilation avant d’utiliser vos propres données.

Une fois qu&#39;un jeu de données a été renseigné, il est possible d&#39;utiliser le même jeu de données pour importer des fichiers de données supplémentaires.

Si vos données sont stockées dans une application tierce prise en charge, vous pouvez également choisir de créer un [connecteur source](../sources/home.md) pour importer en temps réel les données de vos événements marketing dans [!DNL Platform].

## Étapes suivantes {#next-steps}

Ce document fournit des conseils généraux sur la préparation de vos données en vue de leur utilisation dans [!DNL Intelligent Services]. Si vous avez besoin de services de conseil supplémentaires en fonction de votre cas d&#39;utilisation, veuillez contacter le service d&#39;assistance-Adobe.

Une fois que vous avez renseigné un jeu de données avec vos données d’expérience client, vous pouvez utiliser [!DNL Intelligent Services] pour générer des informations. Pour commencer, reportez-vous aux documents suivants :

* [Présentation d’Attribution AI](./attribution-ai/overview.md)
* [Présentation de Customer AI](./customer-ai/overview.md)
