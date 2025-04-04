---
keywords: Experience Platform;accueil;Services intelligents;rubriques populaires;service intelligent;Service intelligent
solution: Experience Platform
title: Préparation des données en vue de leur utilisation dans les services intelligents
description: Pour qu’Intelligent Services puisse découvrir des informations à partir de vos données d’événements marketing, les données doivent être enrichies sémantiquement et conservées dans une structure standard. Pour ce faire, les services intelligents utilisent des schémas de modèle de données d’expérience (XDM).
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2827'
ht-degree: 2%

---

# Préparation des données en vue de leur utilisation dans [!DNL Intelligent Services]

Pour que [!DNL Intelligent Services] puissiez découvrir des informations à partir de vos données d’événements marketing, les données doivent être enrichies sémantiquement et conservées dans une structure standard. [!DNL Intelligent Services] tirer parti des schémas [!DNL Experience Data Model] (XDM) pour y parvenir. Plus précisément, tous les jeux de données utilisés dans [!DNL Intelligent Services] doivent être conformes au schéma XDM Consumer ExperienceEvent (CEE) ou utiliser le connecteur Adobe Analytics. En outre, l’IA dédiée aux clients prend en charge le connecteur Adobe Audience Manager.

Ce document fournit des instructions générales sur le mappage de vos données d’événements marketing de plusieurs canaux au schéma CEE, en fournissant des informations sur les champs importants du schéma afin de vous aider à déterminer comment mapper efficacement vos données à leur structure. Si vous prévoyez d’utiliser les données Adobe Analytics, consultez la section relative à la [préparation des données Adobe Analytics](#analytics-data). Si vous envisagez d’utiliser les données de Adobe Audience Manager (IA dédiée aux clients uniquement), consultez la section relative à la [préparation des données d’Adobe Audience Manager](#AAM-data).

## Exigences en matière de données

[!DNL Intelligent Services] nécessitent différentes quantités de données historiques en fonction de l’objectif que vous créez. Quoi qu’il en soit, les données que vous préparez pour **tous** [!DNL Intelligent Services] doivent inclure des parcours/événements clients positifs et négatifs. Les événements négatifs et positifs améliorent la précision et la précision du modèle.

Par exemple, si vous utilisez l’IA dédiée aux clients pour prédire la propension à acheter un produit, le modèle pour l’IA dédiée aux clients a besoin d’exemples de chemins d’achat réussis et d’exemples de chemins d’achat infructueux. En effet, lors de la formation aux modèles, l’IA dédiée aux clients cherche à comprendre quels événements et parcours conduisent à un achat. Cela inclut également les actions entreprises par les clients qui n’ont pas effectué d’achat, comme une personne qui a arrêté son parcours pour ajouter un article au panier. Ces clients peuvent présenter des comportements similaires. Cependant, l’IA dédiée aux clients peut fournir des insights et analyser en profondeur les différences et facteurs majeurs qui conduisent à un score de propension plus élevé. De même, l’IA dédiée à l’attribution nécessite à la fois des types d’événements et de parcours afin d’afficher des mesures telles que l’efficacité des points de contact, les principaux chemins de conversion et les répartitions par position de point de contact.

Pour plus d’exemples et d’informations sur les exigences en matière de données historiques, consultez la section [IA dédiée aux clients](./customer-ai/data-requirements.md#data-requirements) ou [IA dédiée à l’attribution](./attribution-ai/input-output.md#data-requirements) exigences en matière de données historiques dans la documentation sur les entrées/sorties.

### Instructions pour l’assemblage de données

Il est recommandé de regrouper les événements d’un utilisateur sur un identifiant commun lorsque cela est possible. Par exemple, vous pouvez avoir des données utilisateur avec « id1 » sur 10 événements. Par la suite, le même utilisateur a supprimé l’ID de cookie et est enregistré comme « id2 » sur les 20 événements suivants. Si vous savez que id1 et id2 correspondent au même utilisateur, la bonne pratique consiste à assembler les 30 événements avec un id commun.

Si cela s’avère impossible, vous devez traiter chaque ensemble d’événements comme un utilisateur différent lors de la création des données d’entrée de votre modèle. Vous obtiendrez ainsi les meilleurs résultats lors de la formation et de la notation des modèles.

## Résumé du workflow

Le processus de préparation varie selon que vos données sont stockées dans Adobe Experience Platform ou en externe. Cette section résume les étapes nécessaires à suivre, selon les scénarios.

### Préparation des données externes

Si vos données sont stockées en dehors d’Experience Platform, vous devez les mapper aux champs obligatoires et pertinents d’un [schéma Consumer ExperienceEvent](#cee-schema). Ce schéma peut être complété par des groupes de champs personnalisés pour mieux capturer vos données client. Une fois mappé, vous pouvez créer un jeu de données à l’aide de votre schéma ExperienceEvent client et [ ingérer vos données dans Experience Platform](../ingestion/home.md). Le jeu de données CEE peut ensuite être sélectionné lors de la configuration d&#39;un [!DNL Intelligent Service].

Selon le [!DNL Intelligent Service] que vous souhaitez utiliser, différents champs peuvent être requis. Notez qu’il est recommandé d’ajouter des données à un champ si vous disposez des données. Pour en savoir plus sur les champs obligatoires, consultez le guide [IA dédiée à l’attribution](./attribution-ai/input-output.md) ou [IA dédiée aux clients](./customer-ai/data-requirements.md) sur les exigences en matière de données.

### Préparation des données Adobe Analytics {#analytics-data}

L’IA dédiée aux clients et l’IA dédiée à l’attribution prennent en charge les données Adobe Analytics de manière native. Pour utiliser les données Adobe Analytics, suivez les étapes décrites dans la documentation pour configurer un connecteur source [Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).

Une fois que le connecteur source diffuse vos données dans Experience Platform, vous pouvez sélectionner Adobe Analytics en tant que source de données suivie d’un jeu de données pendant la configuration de votre instance. Tous les groupes de champs de schéma requis et les champs individuels sont automatiquement créés lors de la configuration de la connexion. Vous n’avez pas besoin d’ETL (Extraction, transformation, chargement) pour les jeux de données au format CEE.

Si vous comparez les données transmises par le biais du connecteur source Adobe Analytics sur Adobe Experience Platform avec les données Adobe Analytics, vous remarquerez peut-être quelques incohérences. Le connecteur Source Analytics peut ignorer des lignes lors de la transformation en schéma de modèle de données d’expérience (XDM). Il peut y avoir plusieurs raisons pour lesquelles la ligne entière ne peut pas être transformée, notamment des horodatages manquants, des ID de personne manquants, des ID de personne volumineux ou non valides, des valeurs d’analyse non valides, etc.

Pour plus d’informations et d’exemples, consultez la documentation pour [comparer des données Adobe Analytics et Customer Journey Analytics](https://www.adobe.com/go/compare-aa-data-to-cja-data). Cet article est conçu pour vous aider à diagnostiquer et à résoudre ces différences afin que vous et votre équipe puissiez utiliser les données Adobe Experience Platform pour les services intelligents sans être gênés par des préoccupations relatives à l’intégrité des données.

Dans Adobe Experience Platform Query Services, exécutez les enregistrements totaux suivants entre l’horodatage de début et de fin par canal.typeAtSource pour rechercher le nombre par canaux marketing.

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>Le connecteur Adobe Analytics prend jusqu’à quatre semaines pour renvoyer les données. Si vous avez récemment configuré une connexion, vous devez vérifier que le jeu de données contient la longueur minimale de données requise pour Customer ou Attribution AI. Consultez les sections sur les données historiques dans [IA dédiée aux clients](./customer-ai/data-requirements.md#data-requirements) ou [IA dédiée à l’attribution](./attribution-ai/input-output.md#data-requirements), et vérifiez que vous disposez de suffisamment de données pour votre objectif de prédiction.

### Préparation des données Adobe Audience Manager (IA dédiée aux clients uniquement) {#AAM-data}

L’IA dédiée aux clients prend en charge les données Adobe Audience Manager en mode natif. Pour utiliser les données d’Audience Manager, suivez les étapes décrites dans la documentation pour configurer un [connecteur source Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

Une fois que le connecteur source diffuse vos données dans Experience Platform, vous pouvez sélectionner Adobe Audience Manager en tant que source de données suivie d’un jeu de données lors de la configuration de l’IA dédiée aux clients. Tous les groupes de champs de schéma et les champs individuels sont automatiquement créés lors de la configuration de la connexion. Vous n’avez pas besoin d’ETL (Extraction, transformation, chargement) pour les jeux de données au format CEE.

>[!IMPORTANT]
>
>Si vous avez récemment configuré un connecteur, vous devez vérifier que le jeu de données contient la longueur minimale de données requise. Veuillez consulter la section données historiques dans la [documentation sur les entrées/sorties](./customer-ai/data-requirements.md) de l’IA dédiée aux clients, et vérifier que vous disposez de suffisamment de données pour votre objectif de prédiction.

### préparation des données [!DNL Experience Platform]

Si vos données sont déjà stockées dans [!DNL Experience Platform] et ne sont pas diffusées en continu via les connecteurs source Adobe Analytics ou Adobe Audience Manager (IA dédiée aux clients uniquement), procédez comme suit. Il est toujours recommandé de comprendre le schéma CEE.

1. Examinez la structure du schéma [Consumer ExperienceEvent](#cee-schema) et déterminez si vos données peuvent être mappées à ses champs.
2. Contactez les services Adobe Consulting pour mapper vos données au schéma et les ingérer dans [!DNL Intelligent Services], ou [suivez les étapes de ce guide](#mapping) si vous souhaitez mapper les données vous-même.

## Présentation du schéma CEE {#cee-schema}

Le schéma ExperienceEvent du client décrit le comportement d’un individu par rapport aux événements de marketing numérique (web ou mobile), ainsi qu’à l’activité commerciale en ligne ou hors ligne. L’utilisation de ce schéma est requise pour [!DNL Intelligent Services] en raison de ses champs (colonnes) sémantiquement bien définis, qui évitent les noms inconnus qui rendraient autrement les données moins claires.

Le schéma CEE, comme tous les schémas XDM ExperienceEvent, capture l’état temporel du système lorsqu’un événement (ou un ensemble d’événements) se produit, y compris le moment et l’identité du titulaire concerné. Les événements d’expérience sont des enregistrements de faits de ce qui s’est produit. Ils sont donc immuables et représentent ce qui s’est produit sans agrégation ni interprétation.

[!DNL Intelligent Services] utiliser plusieurs champs clés dans ce schéma pour générer des informations à partir de vos données d’événements marketing, qui se trouvent tous au niveau racine et sont développés pour afficher les sous-champs requis.

![](./images/data-preparation/schema-expansion.gif)

Comme tous les schémas XDM, le groupe de champs de schéma CEE est extensible. En d’autres termes, des champs supplémentaires peuvent être ajoutés au groupe de champs CEE et différentes variations peuvent être incluses dans plusieurs schémas si nécessaire.

Vous trouverez un exemple complet du groupe de champs dans le [référentiel XDM public](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). En outre, vous pouvez afficher et copier le fichier [JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) suivant pour un exemple de la manière dont les données peuvent être structurées pour se conformer au schéma CEE. Reportez-vous à ces deux exemples au fur et à mesure que vous en apprendrez plus sur les champs clés décrits dans la section ci-dessous, afin de déterminer comment vous pouvez mapper vos propres données au schéma.

## Champs clés

Plusieurs champs clés du groupe de champs CEE doivent être utilisés afin que les [!DNL Intelligent Services] puissent générer des informations utiles. Cette section décrit le cas d’utilisation et les données attendues pour ces champs, et fournit des liens vers la documentation de référence pour d’autres exemples.

### Champs obligatoires

Bien que l’utilisation de tous les champs clés soit vivement recommandée, deux champs sont **obligatoires** pour que le [!DNL Intelligent Services] fonctionne :

* [Un champ d’identité principal](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (obligatoire uniquement pour l’IA dédiée à l’attribution)

#### Identité principale {#identity}

L’un des champs de votre schéma doit être défini comme champ d’identité principal, ce qui [!DNL Intelligent Services] permet de lier chaque instance de données de série temporelle à une personne individuelle.

Vous devez déterminer le meilleur champ à utiliser comme identité principale en fonction de la source et de la nature de vos données. Un champ d’identité doit inclure un **espace de noms d’identité** qui indique le type de données d’identité attendu par le champ en tant que valeur. Voici quelques valeurs d’espace de noms valides :

>[!NOTE]
>
>L’Experience Cloud ID (ECID) est également appelé MCID et continue à être utilisé dans les espaces de noms.

* « e-mail »
* « téléphone »
* « mcid » (pour les identifiants Adobe Audience Manager)
* « aaid » (pour les Adobe Analytics ID)

Si vous ne savez pas quel champ vous devez utiliser comme identité principale, contactez les services Adobe Consulting pour déterminer la meilleure solution. Si aucune identité principale n’est définie, l’application Intelligent Service utilise le comportement par défaut suivant :

| Par défaut | IA dédiée à l’attribution | IA dédiée aux clients |
| --- | --- | --- |
| Colonne Identité | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Espace de noms | AAID | ECID |

Pour définir une identité principale, accédez à votre schéma à partir de l’onglet **[!UICONTROL Schémas]** et sélectionnez le lien hypertexte du nom du schéma pour ouvrir le **[!DNL Schema Editor]**.

![Accéder au schéma](./images/data-preparation/navigate_schema.png)

Ensuite, accédez au champ que vous souhaitez utiliser comme identité principale et sélectionnez-le. Le menu **[!UICONTROL Propriétés du champ]** s’ouvre pour ce champ.

![Sélectionnez le champ](./images/data-preparation/find_field.png)

Dans le menu **[!UICONTROL Propriétés du champ]**, faites défiler l’écran vers le bas jusqu’à trouver la case à cocher **[!UICONTROL Identité]**. Après avoir coché la case, l’option permettant de définir l’identité sélectionnée comme **[!UICONTROL identité de Principal]** s’affiche. Cochez également cette case.

![Cocher la case](./images/data-preparation/set_primary_identity.png)

Ensuite, vous devez fournir un **[!UICONTROL Espace de noms d’identité]** à partir des espaces de noms prédéfinis dans la liste déroulante. Dans cet exemple, l’espace de noms ECID est sélectionné, car un `mcid.id` d’ID Adobe Audience Manager est utilisé. Sélectionnez **[!UICONTROL Appliquer]** pour confirmer les mises à jour, puis sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit pour enregistrer les modifications apportées à votre schéma.

![Enregistrez les modifications](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Ce champ représente la date et l’heure auxquelles l’événement s’est produit. Cette valeur doit être fournie sous la forme d’une chaîne, conformément à la norme ISO 8601.

#### xdm:channel {#channel}

>[!NOTE]
>
>Ce champ n’est obligatoire que lors de l’utilisation de l’IA dédiée à l’attribution.

Ce champ représente le canal marketing associé à l’ExperienceEvent. Le champ contient des informations sur le type de canal, le type de média et le type d’emplacement.

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

Pour obtenir des informations complètes sur chacun des sous-champs obligatoires pour `xdm:channel`, reportez-vous à la spécification [schéma du canal d’expérience](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md). Pour obtenir des exemples de mappages, consultez le [tableau ci-dessous](#example-channels).

#### Exemples de mappages de canal {#example-channels}

Le tableau suivant fournit quelques exemples de canaux marketing mappés au schéma `xdm:channel` :

| Canal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Recherche payante | https:/<span>/ns.adobe.com/xdm/channel-types/search | payé | clics |
| Réseau social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | mérité | clics |
| Affichage | https:/<span>/ns.adobe.com/xdm/channel-types/display | payé | clics |
| E-mail | https:/<span>/ns.adobe.com/xdm/channel-types/email | payé | clics |
| Référent interne | https:/<span>/ns.adobe.com/xdm/channel-types/direct | possédée | clics |
| Afficher la vue d&#39;ensemble | https:/<span>/ns.adobe.com/xdm/channel-types/display | payé | impressions |
| Redirection du code QR | https:/<span>/ns.adobe.com/xdm/channel-types/direct | possédée | clics |
| Mobile | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | possédée | clics |

### Champs recommandés

Le reste des champs clés est décrit dans cette section. Bien que ces champs ne soient pas nécessairement obligatoires pour que [!DNL Intelligent Services] fonctionne, il est vivement recommandé d’en utiliser le plus grand nombre possible afin d’obtenir des informations plus riches.

#### xdm:productListItems

Ce champ est un tableau d’éléments qui représentent les produits sélectionnés par un client, y compris le SKU, le nom, le prix et la quantité du produit.

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

Pour obtenir des informations complètes sur chacun des sous-champs obligatoires pour `xdm:productListItems`, reportez-vous à la spécification [schéma des détails commerciaux](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:commerce

Ce champ contient des informations spécifiques à Commerce sur l’ExperienceEvent, y compris le numéro de commande fournisseur et les informations de paiement.

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

Pour obtenir des informations complètes sur chacun des sous-champs obligatoires pour `xdm:commerce`, reportez-vous à la spécification [schéma des détails commerciaux](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:web

Ce champ représente les détails web relatifs à l’ExperienceEvent, tels que l’interaction, les détails de la page et le référent.

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

Pour obtenir des informations complètes sur chacun des sous-champs obligatoires pour `xdm:productListItems`, reportez-vous à la spécification du schéma [Détails web ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md).

#### xdm:marketing

Ce champ contient des informations relatives aux activités marketing qui sont actives avec le point de contact.

![](./images/data-preparation/marketing.png)

**Exemple de schéma**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Pour obtenir des informations complètes sur chacun des sous-champs obligatoires pour `xdm:productListItems`, reportez-vous à la spécification [du schéma marketing](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md).

## Mappage et ingestion de données {#mapping}

Une fois que vous avez déterminé si vos données d’événements marketing peuvent être mappées au schéma CEE, l’étape suivante consiste à déterminer les données à importer en [!DNL Intelligent Services]. Toutes les données historiques utilisées dans [!DNL Intelligent Services] doivent se situer dans la fenêtre temporelle minimale de quatre mois de données, plus le nombre de jours prévus comme période de recherche en amont.

Après avoir choisi la plage de données à envoyer, contactez les services Adobe Consulting pour mapper vos données au schéma et les ingérer dans le service.

Si vous disposez d’un abonnement [!DNL Adobe Experience Platform] et que vous souhaitez mapper et ingérer les données vous-même, suivez les étapes décrites dans la section ci-dessous.

### Utilisation de Adobe Experience Platform

>[!NOTE]
>
>Les étapes ci-dessous nécessitent un abonnement à Experience Platform. Si vous n’avez pas accès à Experience Platform, passez directement à la section [étapes suivantes](#next-steps).

Cette section décrit le processus de mappage et d’ingestion de données dans Experience Platform en vue d’une utilisation dans [!DNL Intelligent Services], y compris des liens vers des tutoriels détaillant les étapes.

#### Créer un schéma et un jeu de données CEE

Lorsque vous êtes prêt(e) à commencer à préparer vos données pour l’ingestion, la première étape consiste à créer un schéma XDM qui utilise le groupe de champs CEE. Les tutoriels suivants décrivent le processus de création d’un schéma dans l’interface utilisateur ou l’API :

* [Créer un schéma dans l’interface utilisateur](../xdm/tutorials/create-schema-ui.md)
* [Créer un schéma dans l’API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Les tutoriels ci-dessus suivent un workflow générique pour créer un schéma. Lors du choix d’une classe pour le schéma, vous devez utiliser la classe **XDM ExperienceEvent**. Une fois cette classe choisie, vous pouvez ensuite ajouter le groupe de champs CEE au schéma.

Après avoir ajouté le groupe de champs CEE au schéma, vous pouvez ajouter d’autres groupes de champs selon vos besoins pour des champs supplémentaires dans vos données.

Une fois que vous avez créé et enregistré le schéma, vous pouvez créer un jeu de données basé sur ce schéma. Les tutoriels suivants décrivent le processus de création d’un jeu de données dans l’interface utilisateur ou l’API :

* [Créer un jeu de données dans l’interface utilisateur](../catalog/datasets/user-guide.md#create) (suivez le workflow pour utiliser un schéma existant)
* [Créer un jeu de données dans l’API](../catalog/datasets/create.md)

Une fois le jeu de données créé, vous pouvez le retrouver dans l’interface utilisateur d’Experience Platform dans l’espace de travail **[!UICONTROL Jeux de données]**.

![](images/data-preparation/dataset-location.png)

#### Ajouter des champs d’identité au jeu de données

Si vous importez des données provenant de [!DNL Adobe Audience Manager], [!DNL Adobe Analytics] ou d’une autre source externe, vous avez la possibilité de définir un champ de schéma comme champ d’identité. Pour définir un champ de schéma comme champ d’identité, consultez la section sur la définition de champs d’identité dans le tutoriel [IU](../xdm/tutorials/create-schema-ui.md#identity-field) ou [API](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) pour créer un schéma.

Si vous ingérez des données à partir d’un fichier CSV local, vous pouvez passer à la section suivante sur [le mappage et l’ingestion de données](#ingest).

#### Mapper et ingérer des données {#ingest}

Après avoir créé un schéma et un jeu de données CEE, vous pouvez commencer à mapper vos tableaux de données au schéma et ingérer ces données dans Experience Platform. Consultez le tutoriel sur [le mappage d’un fichier CSV à un schéma XDM](../ingestion/tutorials/map-csv/overview.md) pour savoir comment effectuer cette opération dans l’interface utilisateur. Vous pouvez utiliser l’[exemple de fichier JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) suivant pour tester le processus d’ingestion avant d’utiliser vos propres données.

Une fois qu’un jeu de données a été renseigné, le même jeu de données peut être utilisé pour ingérer des fichiers de données supplémentaires.

Si vos données sont stockées dans une application tierce prise en charge, vous pouvez également choisir de créer un [connecteur source](../sources/home.md) pour ingérer en temps réel les données de vos événements marketing dans [!DNL Experience Platform].

## Étapes suivantes {#next-steps}

Ce document fournit des instructions générales sur la préparation des données en vue de leur utilisation dans [!DNL Intelligent Services]. Si vous avez besoin de conseils supplémentaires en fonction de votre cas d’utilisation, contactez l’assistance Adobe Consulting.

Une fois que vous avez renseigné un jeu de données avec vos données d’expérience client, vous pouvez utiliser [!DNL Intelligent Services] pour générer des informations. Reportez-vous aux documents suivants pour commencer :

* [Présentation d’Attribution AI](./attribution-ai/overview.md)
* [Présentation de Customer AI](./customer-ai/overview.md)
