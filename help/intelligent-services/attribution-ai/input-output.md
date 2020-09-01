---
keywords: Experience Platform;getting started;Attribution ai;popular topics;Attribution ai input;Attribution ai output;
solution: Experience Platform
title: Entrée et sortie Attribution AI
topic: Input and Output data for Attribution AI
description: Le document suivant décrit les différents apports et extrants utilisés dans l'Attribution AI.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '2075'
ht-degree: 16%

---


# [!DNL Attribution AI] entrée et sortie

Le document suivant décrit les différents apports et extrants utilisés dans [!DNL Attribution AI].

## [!DNL Attribution AI] données d’entrée

[!DNL Attribution AI] utilise [!DNL Consumer Experience Event] les données pour calculer les scores algorithmiques. Pour plus d’informations sur [!DNL Consumer Experience Event]cette solution, reportez-vous à la section [Préparation des données à utiliser dans la documentation](../data-preparation.md)relative aux services intelligents.

Toutes les colonnes du schéma [!DNL Consumer Experience Event] (CEE) ne sont pas obligatoires pour l’Attribution AI.

>[!NOTE]
>
> Les 9 colonnes suivantes sont obligatoires, d’autres colonnes sont facultatives, mais recommandées/nécessaires si vous souhaitez utiliser les mêmes données pour d’autres solutions d’Adobe telles que [!DNL Customer AI] et [!DNL Journey AI].

| Colonnes obligatoires | Nécessaire pour |
| --- | --- |
| Champ d&#39;identité Principal | Point de contact / Conversion |
| Horodatage | Point de contact / Conversion |
| Channel._type | Point de contact |
| Channel.mediaAction | Point de contact |
| Channel.mediaType | Point de contact |
| Marketing.trackingCode | Point de contact |
| Marketing.campaignname | Point de contact |
| Marketing.campaigngroup | Point de contact |
| Commerce | Conversion  |

En règle générale, l’attribution est exécutée sur les colonnes de conversion telles que la commande, les achats et les passages en caisse sous &quot;commerce&quot;. Les colonnes &quot;canal&quot; et &quot;marketing&quot; sont fortement conseillées pour définir des points de contact pour obtenir de bonnes informations. Cependant, vous pouvez inclure toute autre colonne supplémentaire ainsi que les colonnes ci-dessus à configurer comme une conversion ou une définition de point de contact.

Les colonnes ci-dessous ne sont pas obligatoires, mais il est recommandé de les inclure dans votre schéma CEE si vous disposez des informations disponibles.

**Colonnes supplémentaires recommandées :**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### Données historiques

>[!IMPORTANT]
>
> La quantité minimale de données nécessaire au fonctionnement d’Attribution AI est la suivante :
> - Vous devez fournir au moins 3 mois (90 jours) de données pour exécuter un bon modèle.
> - Vous avez besoin d’au moins 1 000 conversions.


attribution ai nécessite des données historiques comme entrée pour la formation au modèle. La durée des données requises est principalement déterminée par deux facteurs clés : fenêtre de formation et fenêtre de rappel. Les entrées avec des fenêtres de formation plus courtes sont plus sensibles aux tendances récentes, tandis que des fenêtres de formation plus longues permettent de produire des modèles plus stables et précis. Il est important de modéliser l&#39;objectif avec des données historiques qui représentent le mieux vos objectifs commerciaux.

Les événements de conversion des filtres de la configuration [de la fenêtre de](./user-guide.md#training-window) formation sont définis pour être inclus pour la formation de modèle en fonction du temps d’occurrence. Actuellement, la période minimale de formation est de 1 quart (90 jours). The [lookback window](./user-guide.md#lookback-window) provides a time frame indicating how many days prior to the conversion event touchpoints related to this conversion event should be included. Ces deux concepts déterminent ensemble la quantité de données d’entrée (mesurées en jours) requise pour une application.

Par défaut, Attribution AI définit la fenêtre de formation comme les deux derniers trimestres (6 mois) et la fenêtre de recherche en amont comme 56 jours. En d&#39;autres termes, le modèle tiendra compte de tous les événements de conversion définis qui se sont produits au cours des 2 derniers trimestres et recherchera tous les points de contact qui se sont produits dans les 56 jours précédant le ou les événements de conversion associés.

**Formule**:

Longueur minimale de données requise = fenêtre de formation + fenêtre de recherche

>[!TIP]
>
> La longueur minimale de données requise pour une application avec des configurations par défaut est la suivante : 2 trimestres (180 jours) + 56 jours = 236 jours.

Exemple :

- Vous souhaitez attribuer des événements de conversion qui se sont produits au cours des 90 derniers jours (3 mois) et effectuer le suivi de tous les points de contact qui se sont produits dans les 4 semaines précédant le événement de conversion. La durée des données d’entrée doit s’étendre sur les 90 derniers jours + 28 jours (4 semaines). La fenêtre de formation est de 90 jours et la fenêtre de recherche est de 28 jours totalisant 118 jours.

## Données de sortie Attribution AI

attribution ai génère les résultats suivants :

- [Score granulaire brut](#raw-granular-scores)
- [Scores agrégées](#aggregated-attribution-scores)

**Exemple de schéma de sortie :**

![](./images/input-output/schema_output.gif)

### Score granulaire brut {#raw-granular-scores}

attribution ai génère des scores d’attribution au niveau le plus granulaire possible afin que vous puissiez les découper et les découper en fonction de n’importe quelle colonne de score. Pour vue ces scores dans l’interface utilisateur, lisez la section sur l’ [affichage des chemins](#raw-score-path)de score brut. Pour télécharger les scores à l’aide de l’API, consultez les scores de [téléchargement dans le document Attribution AI](./download-scores.md) .

>[!NOTE]
>
> Vous ne pouvez afficher une colonne de rapports du jeu de données d’entrée dans le jeu de données de sortie de score que si l’un des éléments suivants est vrai :
> - La colonne rapports est incluse dans la page de configuration dans le cadre de la configuration des points de contact ou des définitions de conversion.
> - La colonne rapports est incluse dans d’autres colonnes de jeux de données de score.


Le tableau suivant décrit les champs de schéma dans l’exemple de sortie des scores bruts :

| Nom de colonne (DataType) | Nullable | Description |
| --- | --- | --- |
| horodatage (DateTime) | False | Heure à laquelle un événement de conversion ou une observation s’est produit. <br> **Exemple :** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | True | identityMap de l’utilisateur similaire au format CEE XDM. |
| eventType (chaîne) | True | The primary event type for this time-series record. <br> **Exemple :** &quot;Commande&quot;, &quot;Achat&quot;, &quot;Visite&quot; |
| eventMergeId (chaîne) | True | ID permettant de corréler ou de fusionner plusieurs [!DNL Experience Events] ensembles qui sont essentiellement le même événement ou qui doivent être fusionnés. Le producteur de données doit l&#39;indiquer avant l&#39;assimilation. <br> **Exemple :** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (chaîne) | False | Identificateur unique du événement de la série chronologique. <br> **Exemple :** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _locataireId (objet) | False | Conteneur d’objet de niveau supérieur correspondant à votre ID de tentant. <br> **Exemple :** _atsdsnrmsv2 |
| your_schéma_name (Object) | False | Score la ligne avec le événement de conversion tous les événements de point de contact qui y sont associés et leurs métadonnées. <br> **Exemple :** Scores Attribution AI - Nom du modèle__2020 |
| segmentation (chaîne) | True | Segment de conversion tel que la géosegmentation sur lequel le modèle est construit. En cas d’absence de segments, le segment est identique à conversionName. <br> **Exemple :** ORDER_US |
| conversionName (chaîne) | True | Nom de la conversion configurée lors de la configuration. <br> **Exemple :** Commande, Piste, Visite |
| conversion (objet) | False | Colonnes de métadonnées de conversion. |
| dataSource (chaîne) | True | Identification globale unique d’une source de données. <br> **Exemple :** adobe analytics |
| eventSource (chaîne) | True | Source à laquelle le événement s’est produit. <br> **Exemple :** adobe.com |
| eventType (chaîne) | True | The primary event type for this time-series record. <br> **Exemple :** Ordre |
| geo (chaîne) | True | The geographic location where the conversion was delivered `placeContext.geo.countryCode`. <br> **Exemple :** US |
| priceTotal (Doublon) | True | Recettes obtenues par la conversion <br> **Exemple :** 99,9 |
| product (String) | True | Identifiant XDM du produit lui-même. <br> **Exemple :** RX 1080 ti |
| productType (chaîne) | True | Nom d’affichage du produit tel qu’il est présenté à l’utilisateur pour cette vue de produits. <br> **Exemple :** Gpus |
| quantité (entier) | True | Quantité achetée pendant la conversion. <br> **Exemple :** 1 1080 ti |
| receiveTimestamp (DateTime) | True | Horodatage reçu de la conversion. <br> **Exemple :** 2020-06-09T00:01:51.000Z |
| skuId (chaîne) | True | Stock keeping unit (SKU), the unique identifier for a product defined by the vendor. <br> **Exemple :** MJ-03-XS-Black |
| horodatage (DateTime) | True | Horodatage de la conversion. <br> **Exemple :** 2020-06-09T00:01:51.000Z |
| passThrough (objet) | True | Jeu de données Score supplémentaire Colonnes spécifiées par l’utilisateur lors de la configuration du modèle. |
| commerce_order_purchaseCity (chaîne) | True | Colonne du jeu de données Score supplémentaire. <br> **Exemple :** ville : San Jose |
| customerProfile (objet) | False | Détails d’identité de l’utilisateur utilisé pour créer le modèle. |
| identity (objet) | False | Contient les détails de l’utilisateur utilisé pour créer le modèle, tels que `id` et `namespace`. |
| id (chaîne) | True | Identifiant de l’utilisateur tel que l’ID de cookie ou AAID ou MCID, etc. <br> **Exemple :** 17348762725408656344688320891369597404 |
| espace de nommage (chaîne) | True | Espace de nommage d&#39;identité utilisé pour construire les chemins et par conséquent le modèle. <br> **Exemple :** aaid |
| touchpointsDetail (tableau d’objets) | True | Liste des détails du point de contact menant à la conversion ordonnée par l’occurrence du point de contact ou l’horodatage. |
| touchpointName (chaîne) | True | Nom du point de contact configuré lors de la configuration. <br> **Exemple :** PAID_SEARCH_CLICK |
| scores (Objet) | True | Contribution du point de contact à cette conversion en tant que score. Pour plus d’informations sur les scores produits dans cet objet, voir la section scores [d’attribution](#aggregated-attribution-scores) agrégés. |
| touchPoint (objet) | True | Métadonnées du point de contact. Pour plus d&#39;informations sur les scores produits dans cet objet, consultez la section scores [](#aggregated-scores) agrégés. |

### Affichage des chemins d’accès aux scores bruts (interface utilisateur) {#raw-score-path}

Vous pouvez vue le chemin d’accès à vos scores bruts dans l’interface utilisateur. Début en sélectionnant **[!UICONTROL Schémas]** dans l’interface utilisateur de la plate-forme, puis en recherchant et en sélectionnant votre schéma de scores AI d’attribution dans l’onglet **[!UICONTROL Parcourir]** .

![Choisissez votre schéma](./images/input-output/schemas_browse.png)

Ensuite, sélectionnez un champ dans la fenêtre **[!UICONTROL Structure]** de l’interface utilisateur. L’onglet Propriétés **[!UICONTROL du]** champ s’ouvre. Dans les propriétés **** de champ se trouve le champ **[!UICONTROL Chemin]** qui correspond à vos scores bruts.

![Choisir un Schéma](./images/input-output/field_properties.png)


### Scores d’attribution agrégés {#aggregated-attribution-scores}

Les scores agrégés peuvent être téléchargés au format CSV depuis l’interface utilisateur de la plate-forme si la période est inférieure à 30 jours.

Attribution AI prend en charge deux catégories de scores d’attribution : les scores algorithmiques et les scores basés sur des règles.

Attribution AI produit deux types différents de scores algorithmiques : les scores incrémentiels et les scores influencés. Un score influencé représente la fraction de la conversion dont chaque point de contact marketing est à l’origine. Un score incrémentiel représente le degré d’impact marginal directement causé par le point de contact marketing. La principale différence entre le score incrémentiel et le score influencé est que le score incrémentiel prend en compte l’effet de base. Il ne présume pas qu’une conversion est provoquée uniquement par les points de contact marketing précédents.

Voici un aperçu rapide d’un exemple de sortie Attribution AI schéma de l’interface utilisateur Adobe Experience Platform :

![](./images/input-output/schema_screenshot.png)

Consultez le tableau ci-dessous pour plus de détails sur chacun de ces scores d’attribution :

| Scores d’attribution | Description |
| ----- | ----------- |
| Influencé (algorithmique) | Le score influencé représente la fraction de la conversion dont chaque point de contact marketing est à l’origine. |
| Incrémentiel (algorithmique) | Le score incrémentiel représente le degré d’impact marginal directement causé par un point de contact marketing. |
| Première touche | Score d’attribution basé sur des règles qui attribue tous les crédits au point de contact initial d’un chemin de conversion. |
| Dernière touche | Score d’attribution basé sur des règles qui attribue tous les crédits au point de contact le plus proche de la conversion. |
| Linéaire | Score d’attribution basé sur des règles qui répartit de manière égale les crédits entre chaque point de contact d’un chemin de conversion. |
| En forme de U | Score d’attribution basé sur des règles qui attribue 40 % des crédits au premier point de contact et 40 % des crédits au dernier point de contact. Les autres points de contact se partagent de manière égale les 20 % restants. |
| Décroissance temporelle | Score d’attribution basé sur des règles qui attribue plus de crédits aux points de contact les plus proches de la conversion par rapport aux points de contact plus éloignés dans le temps de la conversion. |

**Référence du score brut (scores d’attribution)**

Le tableau ci-dessous mappe les scores d’attribution aux scores bruts. Si vous souhaitez télécharger vos scores bruts, consultez la documentation sur le [téléchargement dans Attribution AI](./download-scores.md) .

| Scores d’attribution | Colonne de référence de score brut |
| --- | --- |
| Influencé (algorithmique) | _locataireID.your_schéma_name.element.touchpoint.algorithmiqueInfluencé |
| Incrémentiel (algorithmique) | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.algorithamicInfluencé |
| Première touche | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.firstTouch |
| Dernière touche | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.lastTouch |
| Linéaire | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.linear |
| En forme de U | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.uShape |
| Décroissance temporelle | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.decayUnits |

### Scores agrégées {#aggregated-scores}

Les scores agrégés peuvent être téléchargés au format CSV depuis l’interface utilisateur de la plate-forme si la période est inférieure à 30 jours. Consultez le tableau ci-dessous pour plus d&#39;informations sur chacune de ces colonnes d&#39;agrégat.

| Nom de colonne | Contrainte | Nullable | Description |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Format défini par l&#39;utilisateur et fixe | False | Date du Événement client au format AAAA-MM-JJ. <br> **Exemple**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | Format défini par l&#39;utilisateur et fixe | True | Date du point de contact multimédia au format AAAA-MM-JJ <br> **Exemple**: 21/04/2017 |
| segment (chaîne) | Calculé | False | Segment de conversion tel que la géosegmentation sur lequel le modèle est construit. En cas d’absence de segments, le segment est identique à la variable conversion_scope. <br> **Exemple**: ORDER_AMER |
| conversion_scope (chaîne) | Défini par l&#39;utilisateur | False | Nom de la conversion tel que configuré par l’utilisateur. <br> **Exemple**: ORDER |
| touchpoint_scope (chaîne) | Défini par l&#39;utilisateur | True | Nom du point de contact tel que configuré par l’utilisateur. <br> **Exemple**: PAID_SEARCH_CLICK |
| product (String) | Défini par l&#39;utilisateur | True | The XDM identifier of the product. <br> **Exemple**: CC |
| product_type (chaîne) | Défini par l&#39;utilisateur | True | Nom d’affichage du produit tel qu’il est présenté à l’utilisateur pour cette vue de produits. <br> **Exemple**: gpus, ordinateurs portables |
| geo (chaîne) | Défini par l&#39;utilisateur | True | The geographic location where the conversion was delivered (placeContext.geo.countryCode) <br> **Exemple**: US |
| événement_type (chaîne) | Défini par l&#39;utilisateur | True | The primary event type for this time-series record <br> **Exemple**: Conversion payante |
| media_type (chaîne) | ENUM | False | Indique si le type de média est payé, détenu ou gagné. <br> **Exemple**: PAYÉ, PROPRIÉTAIRE |
| canal (chaîne) | ENUM | False | Propriété `channel._type` utilisée pour fournir une classification approximative des canaux avec des propriétés similaires dans [!DNL Consumer Experience Event] XDM. <br> **Exemple**: RECHERCHE |
| action (chaîne) | ENUM | False | La `mediaAction` propriété est utilisée pour fournir un type d’action multimédia de événement d’expérience. <br> **Exemple**: CLICK |
| campaign_group (chaîne) | Défini par l&#39;utilisateur | True | Nom du groupe de campagnes dans lequel plusieurs campagnes sont regroupées, par exemple &quot;50 %_DISCOUNT&quot;. <br> **Exemple**: COMMERCIAL |
| campaign_name (chaîne) | Défini par l&#39;utilisateur | True | Nom de la campagne utilisée pour identifier la campagne marketing telle que &#39;50%_DISCOUNT_USA&#39; ou &#39;50%_DISCOUNT_ASIA&#39;. <br> **Exemple**: La vente de Thanksgiving |

**Référence du score brut (agrégé)**

Le tableau ci-dessous mappe les scores agrégés aux scores bruts. Si vous souhaitez télécharger vos scores bruts, consultez la documentation sur le [téléchargement dans Attribution AI](./download-scores.md) . Pour vue des chemins d’accès aux scores bruts depuis l’interface utilisateur, consultez la section sur l’ [affichage des chemins d’accès aux](#raw-score-path) scores bruts dans ce document.

| Nom de colonne | Colonne de référence Note brute |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.timestamp |
| segment | _locataireID.your_schéma_name.segmentation |
| conversion_scope | _locataireID.your_schéma_name.conversion.conversionName |
| touchpoint_scope | _locataireID.your_schéma_name.touchpointsDetail.element.touchpointName |
| product | _locataireID.your_schéma_name.conversion.product |
| product_type | _locataireID.your_schéma_name.conversion.product_type |
| géo | _locataireID.your_schéma_name.conversion.geo |
| événement_type | eventType |
| media_type | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.mediaType |
| marketing | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.mediaChannel |
| action | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _locataireID.your_schéma_name.touchpointsDetail.element.touchpoint.campaignName |


## Étapes suivantes {#next-steps}

Once you have prepared your data and have all your credentials and schemas in place, start by following the [Attribution AI user guide](./user-guide.md). Ce guide vous guide tout au long de la création d’une instance pour Attribution AI.