---
keywords: Experience Platform;accueil;rubriques les plus consultées;gestion des données;droits de licence;licences;bonnes pratiques
title: Bonnes pratiques relatives au droit à la licence de Data Management
description: Ce document décrit les bonnes pratiques à suivre et les outils que vous pouvez utiliser pour mieux gérer vos droits de licence avec Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: a15b5525d3a2fa034715803c83dc22a94915347e
workflow-type: tm+mt
source-wordcount: '2586'
ht-degree: 2%

---

# Bonnes pratiques relatives aux droits de licence Data Management

Adobe Experience Platform est un système ouvert qui transforme vos données en profils clients fiables qui se mettent à jour en temps réel et qui utilise des insights pilotés par l’IA pour vous aider à offrir les expériences adéquates sur chaque canal. Vous pouvez saisir des données de différents types, volumes et historiques pour les Experience Platform à l’aide de sources, puis traiter ces données pour des cas d’utilisation allant de la segmentation et la personnalisation à l’analyse et à l’apprentissage automatique.

Platform offre des licences qui établissent le nombre de profils que vous pouvez créer et la quantité de données que vous pouvez importer. Compte tenu de la capacité à importer n’importe quelle source, volume ou historique de données, il est possible de dépasser vos droits de licence à mesure que vos volumes de données augmentent.

Ce document décrit les bonnes pratiques à suivre et les outils que vous pouvez utiliser pour mieux gérer vos droits de licence avec Adobe Experience Platform.

## Présentation du stockage des données Adobe Experience Platform

Experience Platform se compose principalement de deux référentiels de données : la valeur [!DNL Data Lake] et le magasin de profils.

Le **[!DNL Data Lake]** sert principalement les objectifs suivants :

* sert de zone d’évaluation pour l’intégration des données dans Experience Platform ;
* sert de stockage de données à long terme pour toutes les données Experience Platform ;
* Active les cas d’utilisation tels que l’analyse des données et la science des données.

Le **Boutique de profils** est l’endroit où les profils client sont créés et qui remplit principalement les fonctions suivantes :

* sert de stockage de données pour les profils utilisés pour prendre en charge les expériences en temps réel ;
* Active les cas d’utilisation tels que la segmentation, l’activation et la personnalisation.

>[!NOTE]
>
>Votre accès au [!DNL Data Lake] peut dépendre du SKU du produit que vous avez acheté. Pour plus d’informations sur les SKU des produits, veuillez contacter votre représentant Adobe.

## Utilisation des licences {#license-usage}

Lorsque vous acquérez une licence d’Experience Platform, vous recevez des droits d’utilisation de licence qui varient selon le SKU :

**[!DNL Addressable Audience]** : nombre total de profils clients autorisés par contrat dans Experience Platform, y compris les profils connus et pseudonymes.

**[!DNL Profile Richness]** - taille moyenne de vos données de profil dans Experience Platform. Vous pouvez augmenter vos [!DNL Profile Richness] Tout droit en achetant un pack riche.

Le [!DNL Profile Richness] varie en fonction de la licence que vous avez achetée. Il existe deux calculs pour [!DNL Profile Richness] disponible :

* La somme de toutes les données de production stockées dans Real-time Customer Data Platform (c’est-à-dire le service de profil et le service d’identité) à tout moment, divisée par le [!DNL Addressable Audience];
* La somme de toutes les données stockées dans Platform (y compris, mais sans s’y limiter, à la variable [!DNL Data Lake], Profile Service et Identity Service) à tout moment et toutes les données que vous diffusez via (au lieu de les stocker dans) Platform au cours des 12 derniers mois, divisées par la variable [!DNL Addressable Audience].

La disponibilité de ces mesures et la définition spécifique de chacune d’elles varient en fonction des licences achetées par votre entreprise.

## Tableau de bord d’utilisation de la licence

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher un instantané des données liées aux licences de votre entreprise pour Platform. Les données du tableau de bord s’affichent exactement comme elles apparaissent au moment précis où l’instantané a été pris. L’instantané n’est ni une approximation ni un échantillon de données, et le tableau de bord n’est pas mis à jour en temps réel.

Pour plus d’informations, consultez le guide sur [utilisation du tableau de bord d’utilisation des licences dans l’interface utilisateur de Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Bonnes pratiques relatives à la gestion des données

Les sections suivantes décrivent les bonnes pratiques à suivre pour mieux gérer vos données.

### Compréhension des données

Toutes les données ne sont pas identiques dans Adobe Experience Platform. Certaines données peuvent être denses, mais de faible valeur, tandis que d&#39;autres peuvent être éparses, mais de grande valeur. Certaines données peuvent perdre de la valeur dès leur génération, tandis que d’autres peuvent être utiles pendant des mois, voire des années.

Il existe trois dimensions à prendre en compte pour comprendre la valeur de vos données :

| Dimension | Description | Exemple |
| --- | --- | --- |
| Volume | Représente la quantité et la totalité des données ingérées. | Clics Web : volume élevé et fidélité modérée. La valeur peut diminuer rapidement. |
| Timespan | Représente la durée pendant laquelle les données ingérées continuent de rester précieuses. | Achats hors ligne : modérez en volume et en fidélité, mais peut s’avérer utile pendant de longues périodes. |
| Fidélité | Représente la richesse des données par rapport aux informations. | Comptes clients : volume faible, mais fidélité élevée. Peut être utile au-delà de la durée de vie d’un client. |

### Outils Data Management {#data-management-tools}

Il existe deux scénarios principaux à prendre en compte lorsque vous assurez que votre utilisation des données reste conforme à vos limites de droits de licence :

### Quelles données importer dans Platform ?

Les données peuvent être ingérées dans un ou plusieurs systèmes dans Platform, à savoir : [!DNL Data Lake] et/ou le magasin de profils. Cela signifie que des données différentes peuvent exister dans les deux systèmes pour différents cas d’utilisation. Par exemple, vous pouvez conserver des données historiques dans la variable [!DNL Data Lake], mais pas dans la banque de profils. Vous pouvez sélectionner les données à envoyer au magasin de profils en activant un jeu de données pour l’ingestion de profils.

>[!NOTE]
>
>Votre accès au [!DNL Data Lake] peut dépendre du SKU du produit que vous avez acheté. Pour plus d’informations sur les SKU des produits, veuillez contacter votre représentant Adobe.

### Quelles données conserver ?

Vous pouvez appliquer à la fois des filtres d’ingestion de données et des règles d’expiration (également appelés &quot;durée de vie&quot;) pour supprimer les données devenues obsolètes pour vos cas d’utilisation. En règle générale, les données comportementales (telles que les données Analytics) consomment beaucoup plus de stockage que les données d’enregistrement (telles que les données de gestion de la relation client). Par exemple, de nombreux utilisateurs de Platform disposent de jusqu’à 90 % des profils renseignés par des données comportementales seules, par rapport à ceux des données d’enregistrement. Par conséquent, la gestion de vos données comportementales est essentielle pour garantir la conformité à vos droits de licence.

Vous pouvez utiliser un certain nombre d’outils pour vous conformer à vos droits d’utilisation de licence :

* [Filtres d’ingestion](#ingestion-filters)
* [TTL Service de profil](#profile-service)

### Filtres d’ingestion {#ingestion-filters}

Les filtres d’ingestion vous permettent d’importer uniquement les données nécessaires à vos cas d’utilisation et d’éliminer tous les événements qui ne sont pas requis.

| Filtre d’ingestion | Description |
| --- | --- |
| Filtrage de la source Adobe Audience Manager | Lorsque vous créez une connexion source Adobe Audience Manager, vous pouvez sélectionner les segments et les caractéristiques à importer dans la [!DNL Data Lake] et le service de profil, plutôt que d’ingérer les données d’Audience Manager dans leur intégralité. Consultez le guide sur la [création d’une connexion source d’Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) pour plus d’informations. |
| Préparation de données Adobe Analytics | Vous pouvez utiliser [!DNL Data Prep] fonctionnalités lors de la création d’une connexion source Analytics pour filtrer les données qui ne sont pas requises pour vos cas d’utilisation. Via [!DNL Data Prep], vous pouvez définir les attributs/colonnes à publier dans Profile. Vous pouvez également fournir des instructions conditionnelles pour indiquer à Platform si les données doivent être publiées dans Profile ou uniquement dans le [!DNL Data Lake]. Consultez le guide sur la [création d’une connexion source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) pour plus d’informations. |
| Prise en charge de l’activation/désactivation de jeux de données pour Profile | Pour ingérer des données dans le service de profil, vous devez activer un jeu de données à utiliser dans le magasin de profils. Cela permet d’ajouter à votre [!DNL Addressable Audience] et [!DNL Profile Richness] droits. Une fois qu’un jeu de données n’est plus nécessaire pour les cas d’utilisation de profil client, vous pouvez désactiver l’intégration de ce jeu de données à Profile pour vous assurer que vos données restent conformes à la licence. Consultez le guide sur la [activation et désactivation des jeux de données pour Profile](../../catalog/datasets/enable-for-profile.md) pour plus d’informations. |
| Exclusion des données du SDK web et du SDK mobile | Il existe deux types de données collectées par le SDK Web et Mobile : données collectées automatiquement et données explicitement collectées par votre développeur. Pour mieux gérer la conformité des licences, vous pouvez désactiver la collecte automatique des données dans la configuration du SDK via le paramètre de contexte. Les données personnalisées peuvent également être supprimées ou non définies par votre développeur. Consultez le guide sur la [configuration des principes de base du SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) pour plus d’informations. |
| Exclusion des données de transfert côté serveur | Si vous envoyez des données à Platform à l’aide du transfert côté serveur, vous pouvez exclure les données envoyées en supprimant le mappage dans une action de règle pour l’exclure de tous les événements ou en ajoutant des conditions à la règle afin que les données ne se déclenchent que pour certains événements. Consultez la documentation relative à [événements et conditions](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

### Service de profil {#profile-service}

La fonctionnalité TTL (durée de vie) du service Profile vous permet d’appliquer TTL sur les données de la banque de profils. Cela permet au système de supprimer automatiquement les données dont la valeur a diminué au fil du temps.

La banque de profils est composée des composants suivants :

| Composant Boutique de profils | Description |
| --- | --- |
| Fragments de profil | Chaque profil client est composé de plusieurs **fragments de profil** qui ont été fusionnés pour former une vue unique de ce client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre entreprise aura plusieurs **fragments de profil** relatif à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont assemblés à l’aide du graphique d’identités pour créer un profil unique pour ce client. **Fragments de profil** se compose d’un espace de noms d’identité comme identifiant, avec les données d’enregistrement et/ou les données de série temporelle associées. |
| Enregistrer les données (attributs) | Un profil est une représentation d’un sujet, d’une organisation ou d’un individu, composé de plusieurs **Attributs** (également appelé **données d’enregistrement**). Par exemple, le profil d’un produit peut inclure un SKU et une description, tandis que le profil d’une personne contient des informations telles que le prénom, le nom et l’adresse e-mail. **Enregistrer les données** est généralement faible/modéré en volume, mais utile pour de longues périodes de temps. |
| Données de série temporelle (comportement) | **Données de série temporelle** fournit des informations sur le comportement d’un utilisateur. Représenté par la classe de schéma standard Experience Data Model (XDM) [!DNL ExperienceEvent], les données de série temporelle peuvent décrire des événements tels que des éléments ajoutés à un panier, des liens sur lesquels l’utilisateur clique et des vidéos visionnées. La valeur du comportement peut diminuer au fil du temps. |
| Espace de noms d’identité (identités) | Lorsque les données client se combinent, elles sont fusionnées en un seul profil à l’aide de la fonction **espaces de noms d’identité** et la possibilité de regrouper ces identités au fur et à mesure que davantage d’informations deviennent connues sur l’utilisateur. Voir [espaces de noms d’identité - Aperçu](../../identity-service/namespaces.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

#### Rapports sur la composition de la banque de profils

Plusieurs rapports sont disponibles pour vous aider à comprendre la composition de la banque de profils. Ces rapports vous aident à prendre des décisions éclairées sur la manière et l’emplacement de définir vos TTL de profil pour optimiser l’utilisation de vos licences :

* **API du rapport de chevauchement de jeux de données**: Expose les jeux de données qui contribuent le plus à votre audience adressable. Vous pouvez utiliser ce rapport pour identifier lequel [!DNL ExperienceEvent] jeux de données pour lesquels définir un TTL. Voir le tutoriel sur [génération du rapport de chevauchement de jeux de données](../../profile/tutorials/dataset-overlap-report.md) pour plus d’informations.
* **API Rapport de chevauchement d’identités**: Expose les espaces de noms d’identité qui contribuent le plus à votre audience adressable. Voir le tutoriel sur [génération du rapport de chevauchement d’identités](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) pour plus d’informations.
* **API de rapport Profils inconnus**: Expose l’impact de l’application de TTL pseudonyme pour différents seuils temporels. Vous pouvez utiliser ce rapport pour identifier le seuil TTL pseudonyme à appliquer. Voir le tutoriel sur [génération du rapport des profils inconnus](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) pour plus d’informations.

#### [!DNL ExperienceEvent] Jeu de données TTL {#dataset-ttl}

Vous pouvez appliquer la durée de vie (TTL) à des jeux de données activés pour Profile afin de supprimer les données comportementales de la banque de profils qui ne sont plus importantes pour vos cas d’utilisation. Une fois que la durée de vie (TTL) est appliquée à un jeu de données activé par Profile, Platform supprime automatiquement les données qui ne sont plus nécessaires au moyen d’un processus en deux parties :

* La valeur d’expiration TTL sera appliquée à toutes les nouvelles données à venir au moment de l’ingestion.
* La valeur d’expiration TTL sera appliquée à toutes les données existantes dans le cadre d’une tâche de système de renvoi unique.

Vous pouvez vous attendre à ce que la valeur TTL de chaque événement provienne de l’horodatage de l’événement. Tous les événements antérieurs à la valeur d’expiration TTL sont immédiatement ignorés lors de l’exécution de la tâche système. Tous les autres événements sont ignorés lorsqu’ils approchent de la valeur d’expiration TTL désignée dans l’horodatage de l’événement.

Consultez l’exemple suivant pour mieux comprendre [!DNL ExperienceEvent] Jeu de données TTL.

Si vous appliquez une valeur TTL de 30 jours le 15 mai, alors :

* Tous les nouveaux événements seront soumis à une durée de vie de 30 jours au fur et à mesure de leur arrivée ;
* Tous les événements existants dont l’horodatage est antérieur au 15 avril sont immédiatement supprimés par une tâche système.;
* Les événements dont l’horodatage est postérieure au 15 avril recevront l’expiration de leur horodatage d’événement + jours TTL. Ainsi, un événement avec un horodatage du 18 avril sera abandonné trois jours après le 15 mai.

>[!IMPORTANT]
>
>Une fois qu’une durée de vie est appliquée, toutes les données antérieures au nombre de jours de durée de vie sélectionné sont **définitivement** supprimé et ne peut pas être restauré.

Avant d’appliquer la durée de vie (TTL), vous devez vous assurer de conserver une période de recherche arrière pour tous les segments à l’intérieur de la limite de durée de vie (TTL). Sinon, les résultats du segment peuvent devenir incorrects une fois la durée de vie appliquée. Par exemple, si vous avez appliqué un délai d’activation de 30 jours pour les données Adobe Analytics et un délai d’activation de 365 jours pour les données des transactions en magasin, le segment suivant créera des résultats incorrects :

* Page du produit affichée au cours des 60 derniers jours, suivie d’un achat en magasin ;
* Ajoutez au panier suivi d’aucun achat au cours des 60 derniers jours.

Inversement, les éléments suivants génèrent toujours des résultats corrects :

* Page des produits affichée au cours des 14 derniers jours, suivie d’un achat en magasin ;
* a consulté une page d’aide spécifique en ligne au cours des 30 derniers jours ;
* achat hors ligne d’un produit au cours des 120 derniers jours ;
* Ajout au panier suivi d’un achat au cours des 14 derniers jours.

>[!TIP]
>
>Pour des raisons pratiques, vous pouvez conserver le même TTL pour tous les jeux de données, de sorte que vous n’ayez pas à vous soucier de l’impact TTL sur les jeux de données dans la logique de segmentation.

Pour plus d’informations sur l’application de TTL aux données de profil, consultez la documentation sur [TTL Service de profil](../../profile/apply-ttl.md).

## Résumé des bonnes pratiques pour la conformité à l’utilisation des licences {#best-practices}

Vous trouverez ci-dessous une liste de bonnes pratiques recommandées pour garantir une meilleure conformité à vos droits d’utilisation des licences :

* Utilisez la variable [tableau de bord d’utilisation des licences](../../dashboards/guides/license-usage.md) pour suivre et surveiller les tendances d’utilisation des clients. Vous pouvez ainsi anticiper les dépassements potentiels qui peuvent survenir.
* Configurer [filtres d’ingestion](#ingestion-filters) en identifiant les événements requis pour vos cas d’utilisation de la segmentation et de la personnalisation. Cela vous permet d’envoyer uniquement les événements importants requis pour vos cas d’utilisation.
* Assurez-vous que vous ne disposez que de [jeux de données activés pour le profil](#ingestion-filters) qui sont requis pour vos cas d’utilisation de segmentation et de personnalisation.
* Configurez une [[!DNL ExperienceEvent] Jeu de données TTL](#dataset-ttl) pour les données à haute fréquence, telles que les données web.
* Vérifiez régulièrement le [Rapports de composition de profils](#profile-store-composition-reports) pour comprendre la composition de votre banque de profils. Cela vous permet de comprendre les sources de données qui contribuent le plus à votre consommation d’utilisation des licences.

## Résumé des fonctionnalités et disponibilité {#feature-summary}

Les bonnes pratiques et outils décrits dans ce document vous aideront à mieux gérer l’utilisation des droits de licence dans Adobe Experience Platform. Ce document sera mis à jour au fur et à mesure que des fonctionnalités supplémentaires seront publiées pour offrir visibilité et contrôle à tous les clients Experience Platform.

Le tableau suivant présente la liste des fonctionnalités actuellement disponibles à votre disposition afin de mieux gérer vos droits d’utilisation de licence.

| Fonctionnalité | Description |
| --- | --- |
| [Activation/désactivation de jeux de données pour Profile](../../catalog/datasets/user-guide.md) | Activation ou désactivation de l’ingestion des jeux de données dans Profile Service |
| [!DNL ExperienceEvent] Jeu de données TTL | Appliquez un délai d’expiration TTL pour les jeux de données comportementaux dans la banque de profils. Veuillez contacter votre représentant du support Adobe. |
| [Filtres de préparation de données Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Appliquer [!DNL Kafka] filtres pour exclure les données inutiles de l’ingestion |
| [Filtres du connecteur source Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Application de filtres de connexion source d’Audience Manager pour exclure les données inutiles de l’ingestion |
| [Allotion des filtres de données du SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | Application de filtres d’attributs pour exclure les données inutiles de l’ingestion |
| [Filtres de données de transfert d’événement](../../tags/ui/event-forwarding/overview.md) | Application côté serveur [!DNL Kafka] pour exclure les données inutiles de l’ingestion.  Consultez la documentation relative à [règles de balise](../../tags/ui/managing-resources/rules.md) pour plus d’informations. |
| [Interface utilisateur du tableau de bord de l’utilisation des licences](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Afficher un instantané des données liées aux licences de votre entreprise pour Experience Platform |
| [API du rapport de chevauchement de jeux de données](../../profile/tutorials/dataset-overlap-report.md) | Sort les jeux de données qui contribuent le plus à votre audience adressable |
| [API de rapport Profils inconnus](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) | Produit l’impact de l’application d’une durée de vie pseudonyme pour différents seuils temporels |
| [API Rapport de chevauchement d’identités](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Sort les espaces de noms d’identité qui contribuent le plus à votre audience adressable |

{style=&quot;table-layout:auto&quot;}
