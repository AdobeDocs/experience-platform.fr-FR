---
keywords: Experience Platform;prise en main;IA dédiée à l’attribution;rubriques populaires;Entrée IA dédiée à l’attribution;Sortie IA dédiée à l’attribution;
feature: Attribution AI
title: Entrée et sortie dans Attribution AI
description: Le document suivant décrit les différentes entrées et sorties utilisées dans l’IA dédiée à l’attribution.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2474'
ht-degree: 13%

---

# Entrée et sortie en [!DNL Attribution AI]

Le document suivant décrit les différentes entrées et sorties utilisées dans [!DNL Attribution AI].

## [!DNL Attribution AI] des données d’entrée

L’IA dédiée à l’attribution analyse les jeux de données suivants pour calculer les scores algorithmiques :

- Jeux de données Adobe Analytics utilisant le connecteur source [Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Jeux de données d’événements d’expérience (EE) en général à partir d’un schéma Adobe Experience Platform
- Jeux de données d’événements d’expérience client (CEE)

Vous pouvez désormais ajouter plusieurs jeux de données provenant de sources différentes en fonction du **mappage d’identités** (champ) si chacun des jeux de données partage le même type d’identité (espace de noms), tel qu’un ECID. Une fois que vous avez sélectionné une identité et un espace de noms, les mesures d’exhaustivité de la colonne d’ID s’affichent, indiquant le volume de données regroupées. Pour en savoir plus sur l’ajout de plusieurs jeux de données, consultez le guide d’utilisation d’[Attribution AI](./user-guide.md#identity).

Les informations du canal ne sont pas toujours mappées par défaut. Dans certains cas, si le mediaChannel (champ) est vide, vous ne pourrez pas « continuer » tant que vous n’aurez pas mappé un champ à mediaChannel, car il s’agit d’une colonne obligatoire. Si le canal est détecté dans le jeu de données, il est mappé à mediaChannel par défaut. Les autres colonnes telles que **type de média** et **action de média** sont toujours facultatives.

Après avoir mappé le champ de canal, passez à l’étape « Définir des événements » où vous pouvez sélectionner les événements de conversion et les événements de point de contact, puis choisir des champs spécifiques à partir de jeux de données individuels.

>[!IMPORTANT]
>
>Le connecteur source Adobe Analytics peut prendre jusqu’à quatre semaines pour renvoyer les données. Si vous avez récemment configuré un connecteur, vous devez vérifier que le jeu de données contient la longueur minimale de données requise pour l’IA dédiée à l’attribution. Veuillez consulter la section [données historiques](#data-requirements) pour vérifier que vous disposez de suffisamment de données pour calculer des scores algorithmiques précis.

Pour plus d’informations sur la configuration du schéma [!DNL Consumer Experience Event] (CEE), reportez-vous au guide [Préparation des données des services intelligents](../data-preparation.md). Pour plus d’informations sur le mappage des données d’Adobe Analytics, consultez la documentation [Mappages de champs d’Analytics](../../sources/connectors/adobe-applications/analytics.md).

Toutes les colonnes du schéma [!DNL Consumer Experience Event] (CEE) ne sont pas obligatoires pour l’IA dédiée à l’attribution.

Vous pouvez configurer les points de contact à l’aide des champs recommandés ci-dessous dans le schéma ou le jeu de données sélectionné.

| Colonnes recommandées | Nécessaire pour |
| --- | --- |
| Champ d’identité du Principal | Point de contact/conversion |
| Date et heure | Point de contact/conversion |
| Canal._type | Point de contact |
| Channel.mediaAction | Point de contact |
| Channel.mediaType | Point de contact |
| Marketing.trackingCode | Point de contact |
| Marketing.campaignname | Point de contact |
| Marketing.campaigngroup | Point de contact |
| Commerce | Conversion |

En règle générale, l’attribution est exécutée sur les colonnes de conversion telles que les commandes, les achats et les passages en caisse sous « commerce ». Les colonnes « canal » et « marketing » sont utilisées pour définir les points de contact d’Attribution AI (par exemple, `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). Pour des résultats et des informations optimaux, il est vivement recommandé d’inclure autant de colonnes de conversion et de points de contact que possible. De plus, vous n’êtes pas limité aux colonnes ci-dessus. Vous pouvez inclure n’importe quelle autre colonne recommandée ou personnalisée comme définition de conversion ou de point de contact.

Les jeux de données d’événement d’expérience (EE) n’ont pas besoin de disposer explicitement de mixins Canal et Marketing tant que les informations de canal ou de campagne pertinentes pour configurer un point de contact sont présentes dans l’un des champs de mixin ou de transmission.

>[!TIP]
>
>Si vous utilisez des données Adobe Analytics dans votre schéma CEE, les informations de point de contact pour Analytics sont généralement stockées dans `channel.typeAtSource` (par exemple, `channel.typeAtSource = 'email'`).

## Données historiques {#data-requirements}

>[!IMPORTANT]
>
> La quantité minimale de données nécessaire au fonctionnement de l’IA dédiée à l’attribution est la suivante :
> - Vous devez fournir au moins 3 mois (90 jours) de données pour exécuter un modèle correct.
> - Vous avez besoin d’au moins 1 000 conversions.

L’IA dédiée à l’attribution nécessite des données historiques comme entrée pour l’entraînement du modèle. La durée des données requises est principalement déterminée par deux facteurs clés : le créneau d’entraînement et le créneau de recherche en amont. Les entrées avec des fenêtres d’entraînement plus courtes sont plus sensibles aux tendances récentes, tandis que des fenêtres d’entraînement plus longues permettent de produire des modèles plus stables et plus précis. Il est important de modéliser l’objectif avec des données historiques qui représentent le mieux les objectifs de votre entreprise.

La [configuration de la fenêtre de formation](./user-guide.md#training-window) filtre les événements de conversion définis à inclure pour la formation du modèle en fonction du temps d’occurrence. Actuellement, la fenêtre de formation minimale est de 1 trimestre (90 jours). L’[intervalle de recherche en amont](./user-guide.md#lookback-window) fournit une période indiquant le nombre de jours avant l’inclusion des points de contact de l’événement de conversion liés à cet événement de conversion. L’ensemble de ces deux concepts détermine la quantité de données d’entrée (mesurée en jours) requise pour une application.

Par défaut, l’IA dédiée à l’attribution définit la fenêtre de formation comme les 2 derniers trimestres (6 mois) et la fenêtre de recherche en amont comme 56 jours. En d’autres termes, le modèle prend en compte tous les événements de conversion définis qui se sont produits au cours des 2 derniers trimestres et recherche tous les points de contact qui se sont produits au cours des 56 jours précédant le ou les événements de conversion associés.

**Formule** :

Longueur minimale des données requises = créneau de formation + créneau de recherche en amont

>[!TIP]
>
> La longueur minimale de données requise pour une application avec des configurations par défaut est de : 2 trimestres (180 jours) + 56 jours = 236 jours.

Exemple :

- Vous devez attribuer les événements de conversion qui se sont produits au cours des 90 derniers jours (3 mois) et suivre tous les points de contact qui se sont produits au cours des 4 semaines précédant l’événement de conversion. La durée des données d’entrée doit s’étendre sur les 90 derniers jours + 28 derniers jours (4 semaines). L’intervalle de formation est de 90 jours et l’intervalle de recherche en amont de 28 jours, soit un total de 118 jours.

## Données de sortie de l’IA dédiée à l’attribution

L’IA dédiée à l’attribution génère les éléments suivants :

- [Scores granulaires bruts](#raw-granular-scores)
- [Scores agrégés](#aggregated-attribution-scores)

**Exemple de schéma de sortie :**

![](./images/input-output/schema_output.gif)

### Scores granulaires bruts {#raw-granular-scores}

L’IA dédiée à l’attribution génère les scores d’attribution au niveau le plus granulaire possible afin que vous puissiez découper les scores selon n’importe quelle colonne de score. Pour afficher ces scores dans l’interface utilisateur, lisez la section sur l’[affichage des chemins des scores bruts](#raw-score-path). Pour télécharger les scores à l’aide de l’API, consultez le document [téléchargement des scores dans l’IA dédiée à l’attribution](./download-scores.md).

>[!NOTE]
>
> Vous pouvez afficher n’importe quelle colonne de création de rapports souhaitée à partir du jeu de données d’entrée dans le jeu de données de sortie de score uniquement si l’une des conditions suivantes est vraie :
> - La colonne de création de rapports est incluse dans la page de configuration dans le cadre de la configuration des points de contact ou des définitions de conversion.
> - La colonne de rapport est incluse dans les colonnes supplémentaires du jeu de données de note.

Le tableau suivant décrit les champs de schéma dans l’exemple de sortie de scores bruts :

| Nom de la colonne (DataType) | Nul | Description |
| --- | --- | --- |
| timestamp (DateTime) | False | Heure à laquelle un événement de conversion ou une observation s’est produit. <br> **Exemple :** 2020-06-09T00:01:51.000Z |
| identityMap (carte) | True | identityMap de l’utilisateur similaire au format XDM CEE. |
| eventType (chaîne) | True | Type d’événement principal pour cet enregistrement de série temporelle. <br> **Exemple :** « Commande », « Achat », « Visite » |
| eventMergeId (chaîne) | True | Identifiant à mettre en corrélation ou à fusionner plusieurs [!DNL Experience Events] qui constituent essentiellement le même événement ou qui doivent être fusionnés. Ce champ est destiné à être renseigné par le producteur de données avant l’ingestion. <br> **Exemple :** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (chaîne) | False | Identifiant unique de l’événement de série temporelle. <br> **Exemple :** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (objet) | False | Conteneur d&#39;objets de niveau supérieur correspondant à votre ID de client. <br> **Exemple :** _atsdsnrmsv2 |
| your_schema_name (objet) | False | Noter la ligne avec l’événement de conversion, tous les événements de point de contact qui y sont associés et leurs métadonnées. <br> **Exemple :** scores de l’IA dédiée à l’attribution - Nom du modèle __2020 |
| segmentation (chaîne) | True | Segment de conversion tel que la segmentation géographique en fonction de laquelle le modèle est créé. En cas d’absence de segments, segment est identique à conversionName. <br> **Exemple:** ORDER_US |
| conversionName (chaîne) | True | Nom de la conversion qui a été configurée lors de la configuration. <br> **Exemple :** Commande, Lead, Visite |
| conversion (objet) | False | Colonnes de métadonnées de conversion. |
| dataSource (chaîne) | True | Identification unique globale d’une source de données. <br> **Exemple :** Adobe Analytics |
| eventSource (chaîne) | True | Source au moment où l’événement réel s’est produit. <br> **Exemple:** Adobe.com |
| eventType (chaîne) | True | Type d’événement principal pour cet enregistrement de série temporelle. <br> **Exemple :** Order |
| geo (chaîne) | True | Emplacement géographique où la conversion a été diffusée `placeContext.geo.countryCode`. <br> **Exemple :** US |
| priceTotal (Double) | True | Chiffre d’affaires généré par le <br> de conversion **Exemple :** 99.9 |
| product (chaîne) | True | Identifiant XDM du produit lui-même. <br> **Exemple :** RX 1080 ti |
| productType (chaîne) | True | Nom d’affichage du produit tel qu’il est présenté à l’utilisateur pour cette vue de produit. <br> **Exemple : Gpu** |
| quantity (entier) | True | Quantité achetée lors de la conversion. <br> **Exemple :** 1 1080 ti |
| receivedTimestamp (DateTime) | True | Date et heure de réception de la conversion. <br> **Exemple :** 2020-06-09T00:01:51.000Z |
| skuId (chaîne) | True | Unité de stock (SKU), identifiant unique d’un produit défini par le fournisseur. <br> **Exemple :** MJ-03-XS-Black |
| timestamp (DateTime) | True | Date et heure de la conversion. <br> **Exemple :** 2020-06-09T00:01:51.000Z |
| passThrough (objet) | True | Colonnes du jeu de données de note supplémentaires spécifiées par l’utilisateur lors de la configuration du modèle. |
| commerce_order_purchaseCity (chaîne) | True | Colonne de jeu de données de score supplémentaire. <br> **Exemple :** ville : San Jose |
| customerProfile (objet) | False | Détails d’identité de l’utilisateur ou de l’utilisatrice utilisés pour créer le modèle. |
| identity (objet) | False | Contient les détails de l’utilisateur ou de l’utilisatrice utilisé(e) pour créer le modèle, tels que `id` et `namespace`. |
| id (chaîne) | True | ID d’identité de l’utilisateur tel que l’ID de cookie, l’ID Adobe Analytics (AAID) ou l’ID Experience Cloud (ECID, également appelé MCID ou en tant qu’ID de visiteur), etc. <br> **Exemple :** 17348762725408656344688320891369597404 |
| namespace (String) | True | Espace de noms d’identité utilisé pour créer les chemins d’accès et donc le modèle. <br> **Exemple :** aaid |
| touchpointsDetail (Tableau d’objets) | True | La liste des détails des points de contact qui ont conduit à la conversion classée par | occurrence ou horodatage du point de contact. |
| touchpointName (chaîne) | True | Nom du point de contact qui a été configuré lors de la configuration. <br> **Exemple :** PAID_SEARCH_CLICK |
| scores (objet) | True | Contribution du point de contact à cette conversion sous forme de score. Pour plus d’informations sur les scores générés dans cet objet, consultez la section [scores d’attribution agrégés](#aggregated-attribution-scores). |
| touchPoint (objet) | True | Métadonnées du point de contact. Pour plus d’informations sur les scores générés dans cet objet, reportez-vous à la section [scores agrégés](#aggregated-scores). |

### Affichage des chemins de score brut (interface utilisateur) {#raw-score-path}

Vous pouvez afficher le chemin d’accès à vos scores bruts dans l’interface utilisateur. Commencez par sélectionner **[!UICONTROL Schémas]** dans l’interface utilisateur d’Experience Platform, puis recherchez et sélectionnez votre schéma de scores de l’IA dédiée à l’attribution dans l’onglet **[!UICONTROL Parcourir]**.

![Choisissez votre schéma](./images/input-output/schemas_browse.png)

Sélectionnez ensuite un champ dans la fenêtre **[!UICONTROL Structure]** de l’interface utilisateur. L’onglet **[!UICONTROL Propriétés du champ]** s’ouvre. Dans **[!UICONTROL Propriétés du champ]** se trouve le champ de chemin qui correspond à vos scores bruts.

![Choisir un schéma](./images/input-output/field_properties.png)

### Notes d’attribution agrégées {#aggregated-attribution-scores}

Les scores agrégés peuvent être téléchargés au format CSV à partir de l’interface utilisateur d’Experience Platform si la période est inférieure à 30 jours.

Attribution AI prend en charge deux catégories de scores d’attribution : les scores algorithmiques et les scores basés sur des règles.

Attribution AI produit deux types différents de scores algorithmiques : les scores incrémentiels et les scores influencés. Un score influencé représente la fraction de la conversion dont chaque point de contact marketing est à l’origine. Un score incrémentiel représente le degré d’impact marginal directement causé par le point de contact marketing. La principale différence entre le score incrémentiel et le score influencé est que le score incrémentiel prend en compte l’effet de base. Il ne présume pas qu’une conversion est provoquée uniquement par les points de contact marketing précédents.

Voici un aperçu rapide d’un exemple de sortie de schéma IA dédiée à l’attribution provenant de l’interface utilisateur de Adobe Experience Platform :

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

**Référence de score brut (scores d’attribution)**

Le tableau ci-dessous mappe les scores d’attribution aux scores bruts. Si vous souhaitez télécharger vos scores bruts, consultez la documentation [téléchargement des scores dans l’IA dédiée à l’attribution](./download-scores.md).

| Scores d’attribution | Colonne de référence de score brut |
| --- | --- |
| Influencé (algorithmique) | _tenantID.your_schema_name.element.touchpoint.algorithmicInfluected |
| Incrémentiel (algorithmique) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInfluected |
| Première touche | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Dernière touche | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Linéaire | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linéaire |
| En forme de U | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| Décroissance temporelle | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Scores agrégés {#aggregated-scores}

Les scores agrégés peuvent être téléchargés au format CSV à partir de l’interface utilisateur d’Experience Platform si la période est inférieure à 30 jours. Pour plus d’informations sur chacune de ces colonnes agrégées, consultez le tableau ci-dessous.

| Nom de la colonne | Contrainte | Nul | Description |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Format défini et fixe par l’utilisateur | False | Date de l’événement client au format AAAA-MM-JJ. <br> **Exemple** : 2016-05-02 |
| mediatouchpoints_date (DateTime) | Format défini et fixe par l’utilisateur | True | Date du point de contact du média au format AAAA-MM-JJ <br> **Exemple** : 21/04/2017 |
| segment (chaîne) | Calculé | False | Segment de conversion tel que la segmentation géographique sur laquelle le modèle est créé. En cas d’absence de segments, segment est identique à conversion_scope. <br> **Exemple** : ORDER_AMER |
| conversion_scope (chaîne) | Défini par l’utilisateur | False | Nom de la conversion tel que configuré par l’utilisateur. <br> **Exemple** : ORDER |
| touchpoint_scope (chaîne) | Défini par l’utilisateur | True | Nom du point de contact tel que configuré par l’<br> utilisateur **Exemple** : PAID_SEARCH_CLICK |
| product (chaîne) | Défini par l’utilisateur | True | Identifiant XDM du produit. <br> **Exemple** : CC |
| product_type (chaîne) | Défini par l’utilisateur | True | Nom d’affichage du produit tel qu’il est présenté à l’utilisateur pour cette vue de produit. <br> **Exemple** : processeurs graphiques, ordinateurs portables |
| geo (chaîne) | Défini par l’utilisateur | True | Emplacement géographique où la conversion a été effectuée (placeContext.geo.countryCode) <br> **Exemple** : États-Unis |
| event_type (chaîne) | Défini par l’utilisateur | True | Type d’événement principal pour cet enregistrement de série temporelle <br> **Exemple** : Conversion payante |
| media_type (chaîne) | ENUM | False | Décrit le type de média : exposition médiatique achetée, exposition médiatique détenue ou exposition médiatique gagnée. <br> **Exemple** : PAYANT, PROPRIÉTAIRE |
| channel (chaîne) | ENUM | False | La propriété `channel._type` utilisée pour fournir une classification grossière des canaux avec des propriétés similaires dans [!DNL Consumer Experience Event] XDM. <br> **Exemple** : RECHERCHE |
| action (chaîne) | ENUM | False | La propriété `mediaAction` est utilisée pour fournir un type d’action de média d’événement d’expérience. <br> **Exemple** : CLICK |
| campaign_group (chaîne) | Défini par l’utilisateur | True | Nom du groupe de campagnes dans lequel plusieurs campagnes sont regroupées, comme « 50%_DISCOUNT ». <br> **Exemple** : COMMERCIAL |
| campaign_name (chaîne) | Défini par l’utilisateur | True | Nom de la campagne utilisé pour identifier la campagne marketing, tel que « 50%_DISCOUNT_USA » ou « 50%_DISCOUNT_ASIA ». <br> **Exemple** : Thanksgiving Sale |

**Référence de score brut (agrégée)**

Le tableau ci-dessous mappe les scores agrégés aux scores bruts. Si vous souhaitez télécharger vos scores bruts, consultez la documentation [téléchargement des scores dans l’IA dédiée à l’attribution](./download-scores.md). Pour afficher les chemins d’accès aux notes brutes depuis l’interface utilisateur, consultez la section sur l’[affichage des chemins d’accès aux notes brutes](#raw-score-path) dans ce document.

| Nom de la colonne | Colonne de référence de score brut |
| --- | --- |
| customerevents_date | date et heure |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segment | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| produit | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| géo | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| action | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| nom_campagne | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - L’IA dédiée à l’attribution utilise uniquement des données mises à jour pour la formation et la notation. De même, lorsque vous demandez la suppression de données, l’IA dédiée aux clients s’abstient d’utiliser les données supprimées.
> - L’IA dédiée à l’attribution utilise les jeux de données Experience Platform. Pour prendre en charge les demandes de droits des consommateurs qu’une marque peut recevoir, les marques doivent utiliser Experience Platform Privacy Service pour envoyer les demandes d’accès et de suppression des clients afin de supprimer leurs données dans le lac de données, le service d’identités et le profil client en temps réel.
> - Tous les jeux de données que nous utilisons pour l’entrée/la sortie des modèles suivront les directives d’Experience Platform. Le chiffrement des données d’Experience Platform s’applique aux données au repos et en transit. Consultez la documentation pour en savoir plus sur le [&#x200B; chiffrement des données &#x200B;](../../../help/landing/governance-privacy-security/encryption.md)

## Étapes suivantes {#next-steps}

Une fois vos données préparées et vos informations d’identification et schémas en place, commencez par suivre le guide d’utilisation d’[Attribution AI](./user-guide.md). Ce guide vous guide tout au long de la création d’une instance pour Attribution AI.
