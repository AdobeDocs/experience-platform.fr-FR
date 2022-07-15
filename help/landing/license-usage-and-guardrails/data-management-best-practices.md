---
keywords: Experience Platform;accueil;rubriques les plus consultées;gestion des données;droits de licence;licences;bonnes pratiques
title: Bonnes pratiques relatives aux droits de licence de gestion des données
description: Ce document décrit les bonnes pratiques à suivre et les outils que vous pouvez utiliser pour mieux gérer vos droits de licence avec Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 02882957fc38058ff092938d631e290725d4bdc2
workflow-type: tm+mt
source-wordcount: '2531'
ht-degree: 100%

---

# Bonnes pratiques relatives aux droits de licence de gestion des données

Adobe Experience Platform est un système ouvert qui transforme vos données en profils clients fiables qui se mettent à jour en temps réel. Il utilise également des informations basées sur l’IA pour vous permettre de proposer des expériences adaptées sur tous les canaux. Vous pouvez saisir des données de différents types, volumes et historiques dans Experience Platform à l’aide de sources. Vous pouvez ensuite adapter ces données à des cas d’utilisation allant de la segmentation et de la personnalisation à l’analyse et au machine learning.

Platform propose des licences qui déterminent le nombre de profils que vous pouvez créer et la quantité de données que vous pouvez importer. Compte tenu de la capacité à importer n’importe quelle source, volume ou historique de données, il est possible que vous dépassiez vos droits de licence à mesure que les volumes de données augmentent.

Ce document décrit les bonnes pratiques à suivre et les outils que vous pouvez utiliser pour mieux gérer vos droits de licence avec Adobe Experience Platform.

## Présentation du stockage des données dans Adobe Experience Platform

Experience Platform se compose principalement de deux référentiels de données : le [!DNL Data Lake] et le magasin de profils.

Le **[!DNL Data Lake]** remplit principalement les fonctions suivantes :

* Il sert de zone de test pour l’intégration des données dans Experience Platform.
* Il sert de stockage de données à long terme pour toutes les données Experience Platform.
* Il permet des cas d’utilisation tels que l’analyse des données et la science des données.

Le **magasin de profils** permet de créer les profils des clients et remplit principalement les fonctions suivantes :

* Il sert de stockage de données pour les profils utilisés afin de prendre en charge les expériences en temps réel.
* Il permet des cas d’utilisation tels que la segmentation, l’activation et la personnalisation.

>[!NOTE]
>
>Votre accès au [!DNL Data Lake] peut dépendre du SKU de produit que vous avez acheté. Pour plus d’informations sur les SKU de produit, contactez votre représentant Adobe.

## Utilisation des licences {#license-usage}

Lorsque vous acquérez une licence pour Experience Platform, vous recevez des droits d’utilisation de licence qui varient selon le SKU :

**[!DNL Addressable Audience]** : le nombre total de profils clients autorisés par contrat dans Experience Platform, y compris les profils connus et pseudonymes.

**[!DNL Profile Richness]** : le volume moyen des données de profil dans Experience Platform. Vous pouvez augmenter vos droits de [!DNL Profile Richness] en achetant un pack d’augmentation de richesse.

La mesure de [!DNL Profile Richness] varie en fonction de la licence que vous avez achetée. Deux calculs de [!DNL Profile Richness] sont disponibles :

* La somme de toutes les données de production stockées dans Real-time Customer Data Platform (c’est-à-dire le service de profil et le service d’identités) à tout moment, divisée par l’[!DNL Addressable Audience]
* La somme de toutes les données stockées dans Platform (y compris, mais sans s’y limiter, le [!DNL Data Lake], le service de profil et le service d’identités) à tout moment et toutes les données que vous diffusez via Platform (au lieu de les stocker) au cours des 12 derniers mois, divisées par l’[!DNL Addressable Audience]

La disponibilité de ces mesures et la définition spécifique de chacune d’elles varient en fonction des licences achetées par l’entreprise.

## Tableau de bord d’utilisation de la licence

L’interface utilisateur d’Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher un instantané des données liées aux licences de votre entreprise pour Platform. Les données du tableau de bord s’affichent exactement comme elles apparaissent au moment précis où l’instantané a été pris. L’instantané n’est ni une approximation ni un échantillon des données et le tableau de bord n’est pas mis à jour en temps réel.

Pour plus d’informations, consultez le guide sur l’[utilisation du tableau de bord d’utilisation de la licence dans l’interface utilisateur de Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data). 

## Bonnes pratiques relatives à la gestion des données

Les sections suivantes décrivent les bonnes pratiques à suivre pour mieux gérer vos données.

### Présentation des données

Toutes les données ne sont pas identiques dans Adobe Experience Platform. Certaines données peuvent être denses, mais de faible valeur, tandis que d’autres peuvent être éparses, mais de grande valeur. Certaines données peuvent perdre en valeur dès qu’elles sont générées, tandis que d’autres peuvent conserver leur valeur pendant des mois, voire des années.

Vous devez tenir compte de trois dimensions pour déterminer la valeur des données :

| Dimension | Description | Exemple |
| --- | --- | --- |
| Volume | Représente la quantité et le total des données ingérées. | Clics sur le Web : volume élevé et fidélité modérée. La valeur peut diminuer rapidement. |
| Durée | Représente la durée pendant laquelle les données ingérées conservent leur valeur. | Achats hors ligne : fidélité et volume modérés, mais la valeur peut être conservée pendant de longues périodes. |
| Fidélité | Représente la richesse des données en matière d’informations. | Comptes clients : faible volume, mais fidélité élevée. La valeur peut dépasser la durée de vie d’un client. |

### Outils de gestion des données {#data-management-tools}

Vous devez prendre en compte deux scénarios principaux pour vous assurer que l’utilisation des données respecte les limites de droits de licence :

### Quelles données importer dans Platform ?

Un ou plusieurs systèmes dans Platform peuvent ingérer les données, à savoir le [!DNL Data Lake] et/ou le magasin de profils. Cela signifie que des données différentes peuvent exister dans les deux systèmes pour différents cas d’utilisation. Par exemple, vous pouvez conserver des données historiques dans le [!DNL Data Lake], mais pas dans le magasin de profils. Vous pouvez sélectionner les données à envoyer au magasin de profils en activant un jeu de données pour l’ingestion de profils.

>[!NOTE]
>
>Votre accès au [!DNL Data Lake] peut dépendre du SKU de produit que vous avez acheté. Pour plus d’informations sur les SKU de produit, contactez votre représentant Adobe.

### Quelles données conserver ?

Vous pouvez appliquer à la fois des filtres d’ingestion de données et des règles d’expiration (également appelées Durée de vie « TTL ») pour supprimer les données devenues obsolètes pour vos cas d’utilisation. En règle générale, les données comportementales (telles que les données Analytics) consomment beaucoup plus de stockage que les données d’enregistrement (telles que les données de gestion de la relation client). Par exemple, pour de nombreux utilisateurs de Platform, les données comportementales constituent à elles seules jusqu’à 90 % des profils, par rapport aux données d’enregistrement. Par conséquent, la gestion des données comportementales est essentielle pour garantir la conformité aux droits de licence.

Vous pouvez utiliser un certain nombre d’outils pour respecter vos droits d’utilisation de licence :

* [Filtres d’ingestion](#ingestion-filters)
* [Durée de vie du service de profil](#profile-service)

### Filtres d’ingestion {#ingestion-filters}

Les filtres d’ingestion vous permettent d’importer uniquement les données nécessaires à vos cas d’utilisation et d’exclure tous les événements qui ne sont pas requis.

| Filtre d’ingestion | Description |
| --- | --- |
| Filtrage de la source Adobe Audience Manager | Lorsque vous créez une connexion source Adobe Audience Manager, vous pouvez sélectionner les segments et les caractéristiques à importer dans le [!DNL Data Lake] et le service de profil, plutôt que d’ingérer l’intégralité des données d’Audience Manager. Pour plus d’informations, consultez le guide sur la [création d’une connexion source Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Préparation de données Adobe Analytics | Vous pouvez utiliser les fonctionnalités de [!DNL Data Prep] lors de la création d’une connexion source Analytics pour filtrer les données qui ne sont pas requises pour vos cas d’utilisation. [!DNL Data Prep] vous permet de définir les attributs/colonnes à publier dans le profil. Vous pouvez également fournir des instructions conditionnelles pour indiquer à Platform si les données doivent être publiées dans le profil ou uniquement dans le [!DNL Data Lake]. Pour plus d’informations, consultez le guide sur la [création d’une connexion source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Prise en charge de l’activation et de la désactivation des jeux de données pour le profil | Pour ingérer des données dans le service de profil, vous devez activer un jeu de données à utiliser dans le magasin de profils. Ce faisant, vous élargissez l’[!DNL Addressable Audience] et les droits de [!DNL Profile Richness]. Une fois qu’un jeu de données n’est plus nécessaire pour les cas d’utilisation de profil client, vous pouvez désactiver l’intégration de ce jeu de données au profil afin de vous assurer que vos données restent conformes à la licence. Pour plus d’informations, consultez le guide sur l’[activation et la désactivation des jeux de données pour le profil](../../catalog/datasets/enable-for-profile.md). |
| Exclusion des données du SDK Web et du SDK mobile | Il existe deux types de collecte de données par le SDK Web et Mobile : les données collectées automatiquement et les données collectées explicitement par le développeur. Pour mieux gérer la conformité de licence, vous pouvez désactiver la collecte de données automatique dans la configuration du SDK via le paramètre contextuel. Les données personnalisées peuvent également être supprimées ou ne pas être définies par le développeur. Pour plus d’informations, consultez le guide sur la [configuration des principes de base du SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=fr#fundamentals). |
| Exclusion des données du transfert côté serveur | Si vous envoyez des données à Platform à l’aide du transfert côté serveur, vous pouvez exclure les données envoyées en supprimant le mappage dans une action de règle pour l’exclure de tous les événements ou en ajoutant des conditions à la règle afin que les données ne se déclenchent que pour certains événements. Pour plus d’informations, consultez la documentation sur les [événements et conditions](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html?lang=fr#events-and-conditions-(if)). |

{style=&quot;table-layout:auto&quot;}

### Service de profil {#profile-service}

La fonctionnalité de durée de vie (TTL) du service de profil vous permet d’appliquer une durée de vie aux données du magasin de profils. Cela permet au système de supprimer automatiquement les données dont la valeur a diminué au fil du temps.

Le magasin de profils comprend les composants suivants :

| Composant de magasin de profils | Description |
| --- | --- |
| Fragments de profil | Chaque profil client est composé de plusieurs **fragments de profil** qui ont été fusionnés afin d’obtenir une vue unique de ce client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs **fragments de profil** associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont assemblés à l’aide du graphique d’identités afin de créer un profil unique pour ce client. Les **fragments de profil** se composent d’un espace de noms d’identité comme identifiant, avec les données d’enregistrement et/ou les données de série temporelle associées. |
| Données d’enregistrement (attributs) | Un profil est la représentation d’un sujet, d’une organisation ou d’un individu. Il est composé de nombreux **attributs** (également appelés **données d’enregistrement**). Par exemple, le profil d’un produit peut inclure un SKU et une description, tandis que le profil d’une personne contient des informations telles que le prénom, le nom et l’adresse e-mail. Le volume des **données d’enregistrement** est généralement faible/modéré, mais leur valeur reste élevée pendant de longues périodes. |
| Données de série temporelle (comportement) | Les **données de série temporelle** fournissent des informations sur le comportement d’un utilisateur. Représentées par la classe de schéma standard du modèle de données d’expérience (XDM) [!DNL ExperienceEvent], les données de série temporelle peuvent décrire des événements tels que l’ajout d’articles à un panier, l’utilisation de liens et la lecture de vidéos. La valeur du comportement peut diminuer au fil du temps. |
| Espace de noms d’identité (identités) | Une fois réunies, les données client sont fusionnées en un profil unique grâce aux **espaces de noms d’identité** et à la possibilité d’assembler ces identités lors de l’acquisition d’informations supplémentaires sur le client. Pour plus d’informations, consultez la [présentation des espaces de noms d’identité](../../identity-service/namespaces.md). |

{style=&quot;table-layout:auto&quot;}

#### Rapports sur la composition du magasin de profils

Plusieurs rapports permettant de déterminer la composition du magasin de profils sont disponibles. Ces rapports vous aident à prendre des décisions éclairées sur la définition des durées de vie des profils et sur leur emplacement, afin d’optimiser l’utilisation des licences :

* **API Dataset Overlap Report** : indique les jeux de données qui contribuent le plus à l’audience adressable. Vous pouvez utiliser ce rapport pour identifier les jeux de données [!DNL ExperienceEvent] pour lesquels définir une durée de vie. Pour plus d’informations, consultez le tutoriel sur la [génération du rapport de chevauchement de jeux de données](../../profile/tutorials/dataset-overlap-report.md).
* **API Identity Overlap Report** : indique les espaces de noms d’identité qui contribuent le plus à l’audience adressable. Pour plus d’informations, consultez le tutoriel sur la [génération du rapport de chevauchement d’identités](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report).
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous TTL for different time thresholds. You can use this report to identify which pseudonymous TTL threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Durée de vie du jeu de données [!DNL ExperienceEvent] {#dataset-ttl}

Vous pouvez appliquer une durée de vie à des jeux de données compatibles avec les profils afin de supprimer les données comportementales du magasin de profils qui n’ont plus de valeur pour vos cas d’utilisation. Une fois que la durée de vie est appliquée à un jeu de données compatible avec les profils, Platform supprime automatiquement les données qui ne sont plus nécessaires grâce à un processus en deux parties :

* Désormais, la valeur d’expiration de durée de vie est appliquée à toutes les nouvelles données au moment de l’ingestion.
* La valeur d’expiration de durée de vie est appliquée à toutes les données existantes dans le cadre d’une tâche de système de renvoi unique.

La valeur de durée de vie de chaque événement provient généralement de la date et heure d’événement. Tous les événements antérieurs à la valeur d’expiration de durée de vie sont immédiatement abandonnés lors de l’exécution de la tâche de système. Tous les autres événements sont abandonnés lorsqu’ils se rapprochent de la valeur d’expiration de durée de vie indiquée dans la date et heure d’événement.

Consultez l’exemple suivant pour mieux comprendre la durée de vie du jeu de données [!DNL ExperienceEvent].

Si vous appliquez une valeur de durée de vie de 30 jours le 15 mai :

* tous les nouveaux événements sont soumis à une durée de vie de 30 jours ;
* tous les événements existants dont la date et heure sont antérieures au 15 avril sont immédiatement supprimés par une tâche de système ; 
* les événements dont la date et heure sont postérieures au 15 avril ont une date d’expiration correspondant à la date et heure d’événement + les jours de durée de vie. Ainsi, un événement dont la date et heure correspondent au 18 avril est abandonné trois jours après le 15 mai.

>[!IMPORTANT]
>
>Une fois qu’une durée de vie est appliquée, toutes les données antérieures au nombre de jours de la durée de vie sélectionnée sont **supprimées de manière permanente** et ne peuvent pas être restaurées.

Avant d’appliquer la durée de vie, vous devez vous assurer de conserver un intervalle de recherche en amont pour tous les segments situés dans la limite de durée de vie. Sinon, les résultats de segmentation peuvent être incorrects après l’application de la durée de vie. Par exemple, si vous appliquez une durée de vie de 30 jours aux données Adobe Analytics et une durée de vie de 365 jours aux données de transactions en magasin, le segment suivant produit des résultats incorrects :

* Page produit affichée au cours des 60 derniers jours, suivie d’un achat en magasin
* Ajout au panier suivi d’aucun achat au cours des 60 derniers jours.

Inversement, le segment suivant génère toujours des résultats corrects :

* Page produit affichée au cours des 14 derniers jours, suivie d’un achat en magasin
* Page d’aide en ligne spécifique affichée au cours des 30 derniers jours
* Achat hors ligne d’un produit au cours des 120 derniers jours
* Ajout au panier suivi d’un achat au cours des 14 derniers jours.

>[!TIP]
>
>Vous pouvez, à des fins pratiques, conserver la même durée de vie pour tous les jeux de données. Ainsi, vous ne devez pas vous soucier de l’impact de la durée de vie sur les jeux de données dans la logique de segmentation.

Pour plus d’informations sur l’application de la durée de vie aux données de profil, consultez la documentation sur la [durée de vie du service de profil](../../profile/apply-ttl.md).

## Résumé des bonnes pratiques pour la conformité de l’utilisation des licences {#best-practices}

Vous trouverez ci-dessous une liste des bonnes pratiques recommandées pour garantir une meilleure conformité aux droits d’utilisation de licence :

* Utilisez le [tableau de bord d’utilisation de la licence](../../dashboards/guides/license-usage.md) pour suivre et surveiller les tendances d’utilisation des clients. Vous pouvez ainsi anticiper les potentiels dépassements qui peuvent survenir.
* Configurez les [filtres d’ingestion](#ingestion-filters) en identifiant les événements requis pour les cas d’utilisation de segmentation et de personnalisation. Cela vous permet d’envoyer uniquement les événements importants nécessaires aux cas d’utilisation.
* Assurez-vous que vous n’avez [activé que les jeux de données pour le profil](#ingestion-filters) qui sont nécessaires aux d’utilisation de segmentation et de personnalisation.
* Configurez une [[!DNL ExperienceEvent] durée de vie de jeu de données](#dataset-ttl) pour les données haute fréquence, telles que les données Web.
* Vérifiez régulièrement les [rapports sur la composition de profils](#profile-store-composition-reports) pour déterminer la composition du magasin de profils. Cela vous permet de comprendre les sources de données qui contribuent le plus à la consommation de l’utilisation des licences.

## Résumé et disponibilité des fonctionnalités {#feature-summary}

Les bonnes pratiques et outils décrits dans ce document vous aideront à mieux gérer les droits d’utilisation de licence dans Adobe Experience Platform. Ce document sera mis à jour lorsque des fonctionnalités supplémentaires seront disponibles pour offrir visibilité et contrôle à tous les clients Experience Platform.

Le tableau suivant présente la liste des fonctionnalités actuellement disponibles afin de mieux gérer les droits d’utilisation de licence.

| Fonctionnalité | Description |
| --- | --- |
| [Activation/désactivation de jeux de données pour le profil](../../catalog/datasets/user-guide.md) | Activez ou désactivez l’ingestion du jeu de données dans le service de profil |
| Durée de vie du jeu de données [!DNL ExperienceEvent] | Appliquez une durée de vie d’expiration pour les jeux de données comportementaux dans le magasin de profils. Contactez votre représentant du service d’assistance Adobe. |
| [Filtres de préparation de données Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Appliquez des filtres [!DNL Kafka] pour exclure les données inutiles de l’ingestion |
| [Filtres de connecteur source Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Appliquez des filtres de connexion source Audience Manager pour exclure les données inutiles de l’ingestion. |
| [Filtres Alloy de données du SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | Appliquez des filtres Alloy pour exclure les données inutiles de l’ingestion. |
| [Filtres de données de transfert d’événement](../../tags/ui/event-forwarding/overview.md) | Appliquez des filtres [!DNL Kafka] côté serveur pour exclure les données inutiles de l’ingestion.  Pour plus d’informations, consultez la documentation sur les [règles de balise](../../tags/ui/managing-resources/rules.md). |
| [Interface utilisateur du tableau de bord d’utilisation de la licence](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Affichez un instantané des données liées aux licences de l’entreprise pour Experience Platform. |
| [API Dataset Overlap Report](../../profile/tutorials/dataset-overlap-report.md) | Génère les jeux de données qui contribuent le plus à l’audience adressable. |
| [API Identity Overlap Report](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Génère les espaces de noms d’identité qui contribuent le plus à l’audience adressable. |

{style=&quot;table-layout:auto&quot;}
