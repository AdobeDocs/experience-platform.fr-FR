---
keywords: Experience Platform;accueil;services intelligents;rubriques les plus consultées;service intelligent;service intelligent
solution: Intelligent Services
title: Préparation des données à utiliser dans les services intelligents
topic-legacy: Intelligent Services
description: Pour que les services intelligents découvrent des informations à partir de vos données d’événements marketing, les données doivent être enrichies sémantiquement et conservées dans une structure standard. Pour ce faire, les services intelligents utilisent des schémas de modèle de données d’expérience (XDM).
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '2919'
ht-degree: 1%

---

# Préparation des données en vue de leur utilisation dans [!DNL Intelligent Services]

Pour [!DNL Intelligent Services] pour découvrir des informations à partir de vos données d’événements marketing, les données doivent être enrichies sémantiquement et conservées dans une structure standard. [!DNL Intelligent Services] exploitation [!DNL Experience Data Model] (XDM) pour ce faire. Plus précisément, tous les jeux de données utilisés dans [!DNL Intelligent Services] doit être conforme au schéma XDM Consumer ExperienceEvent (CEE) ou utiliser le connecteur Adobe Analytics. En outre, Customer AI prend en charge le connecteur Adobe Audience Manager.

Ce document fournit des conseils généraux sur le mappage de vos données d’événements marketing de plusieurs canaux au schéma CEE, décrivant les informations sur les champs importants du schéma pour vous aider à déterminer comment mapper efficacement vos données à sa structure. Si vous prévoyez d’utiliser les données Adobe Analytics, consultez la section pour [Préparation des données Adobe Analytics](#analytics-data). Si vous prévoyez d’utiliser des données Adobe Audience Manager (Customer AI uniquement), consultez la section pour [Préparation des données d’Adobe Audience Manager](#AAM-data).

## Exigences de données

[!DNL Intelligent Services] nécessitent différents volumes de données historiques en fonction de l’objectif que vous créez. Quoi qu’il en soit, les données que vous préparez **all** [!DNL Intelligent Services] doit inclure des parcours/événements client positifs et négatifs. Le fait d’avoir des événements négatifs et positifs améliore la précision et la précision du modèle.

Par exemple, si vous utilisez Customer AI pour prédire la propension à acheter un produit, le modèle de Customer AI nécessite à la fois des exemples de parcours d’achat réussis et des exemples de chemins d’accès infructueux. En effet, pendant la formation du modèle, Customer AI cherche à comprendre les événements et les parcours qui conduisent à un achat. Cela inclut également les actions entreprises par les clients qui n’ont pas effectué d’achat, par exemple une personne qui a arrêté son parcours lors de l’ajout d’un article au panier. Ces clients peuvent avoir des comportements similaires, mais Customer AI peut fournir des informations et analyser les principales différences et facteurs qui mènent à un score de propension plus élevé. De même, Attribution AI nécessite à la fois des types d’événements et de parcours afin d’afficher des mesures telles que l’efficacité des points de contact, les chemins de conversion principaux et les ventilations par position de point de contact.

Pour obtenir des exemples et des informations sur les exigences en matière de données historiques, consultez la page [Customer AI](./customer-ai/input-output.md#data-requirements) ou [Attribution AI](./attribution-ai/input-output.md#data-requirements) la section sur les exigences en matière de données historiques dans la documentation d’entrée/sortie.

### Instructions relatives à l’assemblage de données

Dans la mesure du possible, il est recommandé de regrouper les événements d’un utilisateur sur un identifiant commun. Par exemple, vous pouvez avoir des données utilisateur avec &quot;id1&quot; sur 10 événements. Par la suite, le même utilisateur a supprimé l’ID de cookie et est enregistré sous la forme &quot;id2&quot; sur les 20 événements suivants. Si vous savez que id1 et id2 correspondent à un même utilisateur, la bonne pratique consiste à regrouper les 30 événements avec un identifiant commun.

Si cela n’est pas possible, vous devez traiter chaque ensemble d’événements comme un utilisateur différent lors de la création de vos données d’entrée de modèle. Cela garantit les meilleurs résultats lors de la formation et de la notation des modèles.

## Résumé du workflow

Le processus de préparation varie selon que vos données sont stockées dans Adobe Experience Platform ou en externe. Cette section résume les étapes nécessaires à suivre, quel que soit le scénario.

### Préparation des données externes

Si vos données sont stockées en dehors de l’Experience Platform, vous devez les mapper aux champs requis et pertinents d’une [Schéma ExperienceEvent des clients](#cee-schema). Ce schéma peut être complété avec des groupes de champs personnalisés pour mieux capturer les données de vos clients. Une fois le mappage effectué, vous pouvez créer un jeu de données à l’aide de votre schéma ExperienceEvent dédié aux consommateurs. [ingérer vos données dans Platform](../ingestion/home.md). Le jeu de données CEE peut ensuite être sélectionné lors de la configuration d’un [!DNL Intelligent Service].

Selon le [!DNL Intelligent Service] Si vous souhaitez utiliser , différents champs peuvent être requis. Notez qu’il est recommandé d’ajouter des données à un champ si les données sont disponibles. Pour en savoir plus sur les champs requis, consultez la page [Attribution AI](./attribution-ai/input-output.md) ou [Customer AI](./customer-ai/input-output.md) guide d’entrée/de sortie.

### Préparation des données Adobe Analytics {#analytics-data}

Customer AI et Attribution AI prennent en charge les données Adobe Analytics en mode natif. Pour utiliser les données Adobe Analytics, suivez les étapes décrites dans la documentation pour configurer une [Connecteur source Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).

Une fois que le connecteur source diffuse vos données dans Experience Platform, vous pouvez sélectionner Adobe Analytics comme source de données suivi d’un jeu de données lors de la configuration de votre instance. Tous les groupes de champs de schéma et champs individuels requis sont automatiquement créés lors de la configuration de la connexion. Vous n’avez pas besoin d’utiliser un processus ETL (extraction, transformation, chargement) pour les jeux de données au format CEE.

Si vous comparez les données transportées par le connecteur source Adobe Analytics vers Adobe Experience Platform avec les données Adobe Analytics, vous constaterez peut-être des incohérences. Le connecteur source Analytics peut déposer des lignes pendant la transformation vers un schéma de modèle de données d’expérience (XDM). Il peut y avoir plusieurs raisons pour lesquelles la ligne entière n’est pas adaptée à la transformation, notamment des horodatages manquants, des ID de personne manquants, des ID de personne non valide ou volumineux, des valeurs analytiques non valides, etc.

Pour plus d’informations et d’exemples, consultez la documentation d’ [comparaison des données Adobe Analytics et Customer Journey Analytics](https://www.adobe.com/go/compare-aa-data-to-cja-data). Cet article est conçu pour vous aider à diagnostiquer et à résoudre ces différences afin que vous et votre équipe puissiez utiliser les données Adobe Experience Platform pour les services intelligents sans être entravés par des préoccupations d’intégrité des données.

Dans Adobe Experience Platform Query Services, exécutez le nombre total d’enregistrements suivant entre l’horodatage de début et de fin par requête channel.typeAtSource pour trouver le nombre par canaux marketing.

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
>Le connecteur Adobe Analytics met jusqu’à quatre semaines pour renvoyer les données. Si vous avez récemment configuré une connexion, vous devez vérifier que le jeu de données contient la longueur minimale de données requise pour le client ou Attribution AI. Consultez les sections Données historiques dans [Customer AI](./customer-ai/input-output.md#data-requirements) ou [Attribution AI](./attribution-ai/input-output.md#data-requirements)et vérifiez que vous disposez de suffisamment de données pour votre objectif de prédiction.

### Préparation des données Adobe Audience Manager (Customer AI uniquement) {#AAM-data}

Customer AI prend en charge les données Adobe Audience Manager en mode natif. Pour utiliser les données d’Audience Manager, suivez les étapes décrites dans la documentation pour configurer une [Connecteur source d’Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

Une fois que le connecteur source diffuse vos données dans Experience Platform, vous pouvez sélectionner Adobe Audience Manager comme source de données suivi d’un jeu de données lors de la configuration de Customer AI. Tous les groupes de champs de schéma et les champs individuels sont automatiquement créés lors de la configuration de la connexion. Vous n’avez pas besoin d’utiliser un processus ETL (extraction, transformation, chargement) pour les jeux de données au format CEE.

>[!IMPORTANT]
>
>Si vous avez récemment configuré un connecteur, vous devez vérifier que le jeu de données possède la longueur minimale de données requise. Consultez la section des données historiques dans la [documentation d’entrée/sortie](./customer-ai/input-output.md) pour Customer AI et vérifiez que vous disposez de suffisamment de données pour votre objectif de prédiction.

### [!DNL Experience Platform] préparation des données

Si vos données sont déjà stockées dans [!DNL Platform] et ne pas passer par les connecteurs source Adobe Analytics ou Adobe Audience Manager (Customer AI uniquement), procédez comme suit. Il est toujours recommandé de comprendre le schéma CEE.

1. Examinez la structure de la variable [Schéma ExperienceEvent des clients](#cee-schema) et déterminez si vos données peuvent être mappées à ses champs.
2. Contactez les services de conseil d’Adobe pour vous aider à mapper vos données au schéma et à les ingérer dans [!DNL Intelligent Services]ou [suivre les étapes de ce guide ;](#mapping) si vous souhaitez mapper les données vous-même.

## Présentation du schéma CEE {#cee-schema}

Le schéma ExperienceEvent du client décrit le comportement d’un individu en ce qui concerne les événements de marketing numérique (web ou mobile) ainsi que l’activité de commerce en ligne ou hors ligne. L’utilisation de ce schéma est requise pour [!DNL Intelligent Services] en raison de ses champs (colonnes) sémantiquement bien définis, en évitant les noms inconnus qui rendraient les données moins claires.

Le schéma CEE, comme tous les schémas XDM ExperienceEvent, capture l’état du système basé sur les séries temporelles lorsqu’un événement (ou un ensemble d’événements) s’est produit, y compris le moment et l’identité du sujet concerné. Les événements d’expérience sont des enregistrements factuels de ce qui s’est passé. Ils sont donc immuables et représentent ce qui s’est passé sans agrégation ni interprétation.

[!DNL Intelligent Services] utilisez plusieurs champs clés de ce schéma pour générer des informations à partir de vos données d’événements marketing, qui se trouvent toutes au niveau racine et sont développées pour afficher leurs sous-champs requis.

![](./images/data-preparation/schema-expansion.gif)

Comme tous les schémas XDM, le groupe de champs de schéma CEE est extensible. En d’autres termes, des champs supplémentaires peuvent être ajoutés au groupe de champs CEE et différentes variations peuvent être incluses dans plusieurs schémas, si nécessaire.

Vous trouverez un exemple complet du groupe de champs dans la section [référentiel XDM public](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). En outre, vous pouvez afficher et copier les éléments suivants : [Fichier JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) pour un exemple de la manière dont les données peuvent être structurées pour être conformes au schéma CEE. Reportez-vous à ces deux exemples lorsque vous en apprendrez plus sur les champs clés décrits dans la section ci-dessous, afin de déterminer comment mapper vos propres données au schéma.

## Champs clés

Plusieurs champs clés du groupe de champs CEE doivent être utilisés pour [!DNL Intelligent Services] pour générer des informations utiles. Cette section décrit le cas d’utilisation et les données attendues pour ces champs et fournit des liens vers la documentation de référence pour d’autres exemples.

### Champs obligatoires

Bien que l’utilisation de tous les champs clés soit fortement recommandée, deux champs sont **required** pour [!DNL Intelligent Services] pour travailler :

* [Un champ d’identité Principal](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (obligatoire uniquement pour Attribution AI)

#### Identité Principal {#identity}

L’un des champs de votre schéma doit être défini comme un champ d’identité Principal, qui permet d’activer [!DNL Intelligent Services] pour lier chaque instance de données de série temporelle à une personne.

Vous devez déterminer le meilleur champ à utiliser comme identité Principale en fonction de la source et de la nature de vos données. Un champ d’identité doit inclure une **namespace d’identité** qui indique le type de données d’identité attendu par le champ comme valeur. Certaines valeurs d’espace de noms valides sont les suivantes :

* &quot;adresse e-mail&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (pour les Adobe Audience Manager ID)
* &quot;aid&quot; (pour les Adobe Analytics ID)

Si vous ne savez pas quel champ vous devez utiliser comme identité Principale, contactez les services de conseil d’Adobe pour déterminer la meilleure solution. Si aucune identité Principale n’est définie, l’application Intelligent Service utilise le comportement par défaut suivant :

| Par défaut | IA dédiée à l’attribution | IA dédiée aux clients |
| --- | --- | --- |
| Colonne Identité | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Espace de noms | AAID | ECID |

Pour définir une identité Principale, accédez à votre schéma à partir du **[!UICONTROL Schémas]** et sélectionnez le lien hypertexte du nom du schéma pour ouvrir la **[!DNL Schema Editor]**.

![Accès au schéma](./images/data-preparation/navigate_schema.png)

Ensuite, accédez au champ que vous souhaitez définir comme identité Principale et sélectionnez-le. Le **[!UICONTROL Propriétés du champ]** s’ouvre pour ce champ.

![Sélectionner le champ](./images/data-preparation/find_field.png)

Dans le **[!UICONTROL Propriétés du champ]** , faites défiler l’écran vers le bas jusqu’à ce que vous trouviez la variable **[!UICONTROL Identité]** . Après avoir coché la case, l’option permettant de définir l’identité sélectionnée comme **[!UICONTROL Identité Principal]** apparaît. Cochez également cette case.

![Case à cocher](./images/data-preparation/set_primary_identity.png)

Ensuite, vous devez fournir un **[!UICONTROL Espace de noms d’identité]** dans la liste des espaces de noms prédéfinis dans la liste déroulante. Dans cet exemple, l’espace de noms ECID est sélectionné depuis un Adobe Audience Manager ID. `mcid.id` est en cours d’utilisation. Sélectionner **[!UICONTROL Appliquer]** pour confirmer les mises à jour, puis sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit pour enregistrer les modifications apportées à votre schéma.

![Enregistrez les modifications](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Ce champ représente la date et l’heure auxquelles l’événement s’est produit. Cette valeur doit être fournie sous la forme d’une chaîne, conformément à la norme ISO 8601.

#### xdm:channel {#channel}

>[!NOTE]
>
>Ce champ n’est obligatoire que lorsque vous utilisez Attribution AI.

Ce champ représente le canal marketing associé à ExperienceEvent. Le champ contient des informations sur le type de canal, le type de média et le type d’emplacement.

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

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:channel`, reportez-vous à la section [schéma du canal d’expérience](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) spec. Pour obtenir des exemples de mappages, reportez-vous à la section [tableau ci-dessous](#example-channels).

#### Exemples de mappages de canaux {#example-channels}

Le tableau suivant fournit des exemples de canaux marketing mappés à la variable `xdm:channel` schema :

| Canal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Recherche payante | https:/<span>/ns.adobe.com/xdm/channel-types/search | paid | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | earned | clics |
| Afficher  | https:/<span>/ns.adobe.com/xdm/channel-types/display | paid | clics |
| Adresse e-mail | https:/<span>/ns.adobe.com/xdm/channel-types/email | paid | clics |
| Référent interne | https:/<span>/ns.adobe.com/xdm/channel-types/direct | owned | clics |
| Afficher la vue publicitaire | https:/<span>/ns.adobe.com/xdm/channel-types/display | paid | impressions |
| Redirection du code QR | https:/<span>/ns.adobe.com/xdm/channel-types/direct | owned | clics |
| Mobile | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | owned | clics |

### Champs recommandés

Les autres champs clés sont décrits dans cette section. Bien que ces champs ne soient pas nécessairement requis pour [!DNL Intelligent Services] pour travailler, il est vivement recommandé d’en utiliser autant que possible afin d’obtenir des informations plus riches.

#### xdm:productListItems

Ce champ est un tableau d’éléments qui représente les produits sélectionnés par un client, y compris le SKU, le nom, le prix et la quantité du produit.

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

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:productListItems`, reportez-vous à la section [schéma des détails du commerce](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) spec.

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

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:commerce`, reportez-vous à la section [schéma des détails du commerce](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) spec.

#### xdm:web

Ce champ représente les détails web relatifs à ExperienceEvent, tels que l’interaction, les détails de la page et le référent.

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

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:productListItems`, reportez-vous à la section [Schéma des détails web d’ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) spec.

#### xdm:marketing

Ce champ contient des informations relatives aux activités marketing principales avec le point de contact.

![](./images/data-preparation/marketing.png)

**Exemple de schéma**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Pour obtenir des informations complètes sur chacun des sous-champs requis pour `xdm:productListItems`, reportez-vous à la section [sechma marketing](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) spec.

## Mappage et ingestion de données {#mapping}

Une fois que vous avez déterminé si vos données d’événements marketing peuvent être mappées au schéma CEE, l’étape suivante consiste à déterminer les données à importer. [!DNL Intelligent Services]. Toutes les données historiques utilisées dans [!DNL Intelligent Services] doit se situer dans le délai minimum de quatre mois de données, plus le nombre de jours prévu comme période de recherche arrière.

Après avoir décidé de la plage de données à envoyer, contactez les services de conseil d’Adobe pour les aider à mapper vos données au schéma et à les ingérer dans le service.

Si vous avez une [!DNL Adobe Experience Platform] et que vous souhaitez mapper et ingérer les données vous-même, suivez les étapes décrites dans la section ci-dessous.

### Utilisation de Adobe Experience Platform

>[!NOTE]
>
>Les étapes ci-dessous nécessitent un abonnement à Experience Platform. Si vous n’avez pas accès à Platform, passez directement à la [étapes suivantes](#next-steps) .

Cette section décrit le processus de mappage et d’ingestion de données dans Experience Platform en vue de les utiliser dans [!DNL Intelligent Services], y compris des liens vers des tutoriels pour obtenir des instructions détaillées.

#### Création d’un schéma et d’un jeu de données CEE

Lorsque vous êtes prêt à commencer à préparer vos données pour l’ingestion, la première étape consiste à créer un nouveau schéma XDM qui utilise le groupe de champs CEE. Les tutoriels suivants décrivent le processus de création d’un nouveau schéma dans l’interface utilisateur ou l’API :

* [Création d’un schéma dans l’interface utilisateur](../xdm/tutorials/create-schema-ui.md)
* [Création d’un schéma dans l’API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Les tutoriels ci-dessus suivent un workflow générique pour la création d’un schéma. Lors du choix d’une classe pour le schéma, vous devez utiliser la variable **Classe XDM ExperienceEvent**. Une fois cette classe choisie, vous pouvez ajouter le groupe de champs CEE au schéma.

Après avoir ajouté le groupe de champs CEE au schéma, vous pouvez ajouter d’autres groupes de champs selon les besoins pour des champs supplémentaires dans vos données.

Une fois que vous avez créé et enregistré le schéma, vous pouvez créer un nouveau jeu de données basé sur ce schéma. Les tutoriels suivants décrivent le processus de création d’un jeu de données dans l’interface utilisateur ou l’API :

* [Création d’un jeu de données dans l’interface utilisateur](../catalog/datasets/user-guide.md#create) (Suivez le workflow pour utiliser un schéma existant)
* [Création d’un jeu de données dans l’API](../catalog/datasets/create.md)

Une fois le jeu de données créé, vous pouvez le trouver dans l’interface utilisateur de Platform au sein de l’ **[!UICONTROL Jeux de données]** workspace.

![](images/data-preparation/dataset-location.png)

#### Ajout de champs d’identité au jeu de données

Si vous collectez des données depuis [!DNL Adobe Audience Manager], [!DNL Adobe Analytics], ou une autre source externe, vous avez la possibilité de définir un champ de schéma comme champ d’identité. Pour définir un champ de schéma comme champ d’identité, consultez la section sur la définition des champs d’identité dans le [Tutoriel sur l’interface utilisateur](../xdm/tutorials/create-schema-ui.md#identity-field) ou [Tutoriel sur l’API](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) pour créer un schéma.

Si vous ingérez des données à partir d’un fichier CSV local, vous pouvez passer à la section suivante sur [mappage et ingestion de données](#ingest).

#### Mappage et ingestion de données {#ingest}

Après avoir créé un schéma et un jeu de données CEE, vous pouvez commencer à mapper vos tableaux de données au schéma et ingérer ces données dans Platform. Voir le tutoriel sur [mappage d’un fichier CSV à un schéma XDM](../ingestion/tutorials/map-a-csv-file.md) pour savoir comment effectuer cette opération dans l’interface utilisateur. Vous pouvez utiliser les [exemple de fichier JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) pour tester le processus d’ingestion avant d’utiliser vos propres données.

Une fois qu’un jeu de données a été renseigné, le même jeu de données peut être utilisé pour ingérer des fichiers de données supplémentaires.

Si vos données sont stockées dans une application tierce prise en charge, vous pouvez également choisir de créer une [connecteur source](../sources/home.md) pour ingérer vos données d’événements marketing dans [!DNL Platform] en temps réel.

## Étapes suivantes {#next-steps}

Ce document fournit des instructions générales sur la préparation de vos données en vue de les utiliser dans [!DNL Intelligent Services]. Si vous avez besoin de conseils supplémentaires en fonction de votre cas d’utilisation, contactez l’assistance Adobe-conseil.

Une fois que vous avez renseigné un jeu de données avec vos données d’expérience client, vous pouvez utiliser [!DNL Intelligent Services] pour générer des informations. Consultez les documents suivants pour commencer :

* [Présentation d’Attribution AI](./attribution-ai/overview.md)
* [Présentation de Customer AI](./customer-ai/overview.md)
