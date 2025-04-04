---
title: Bonnes pratiques relatives aux droits de licence de gestion des données
description: Découvrez les bonnes pratiques à suivre et les outils que vous pouvez utiliser pour mieux gérer vos droits de licence avec Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 66%

---

# Bonnes pratiques relatives aux droits de licence de gestion des données

Adobe Experience Platform est un système ouvert qui transforme vos données en profils clients fiables qui se mettent à jour en temps réel. Il utilise également des informations basées sur l’IA pour vous permettre de proposer des expériences adaptées sur tous les canaux. Vous pouvez saisir des données de différents types, volumes et historiques dans Experience Platform à l’aide de sources. Vous pouvez ensuite adapter ces données à des cas d’utilisation allant de la segmentation et de la personnalisation à l’analyse et au machine learning.

Experience Platform propose des licences qui déterminent le nombre de profils que vous pouvez créer et la quantité de données que vous pouvez importer. Compte tenu de la capacité à importer n’importe quelle source, volume ou historique de données, il est possible que vous dépassiez vos droits de licence à mesure que les volumes de données augmentent.

Ce document décrit les bonnes pratiques à suivre et les outils que vous pouvez utiliser pour mieux gérer vos droits de licence avec Adobe Experience Platform.

## Présentation du stockage des données dans Adobe Experience Platform

Experience Platform se compose principalement de deux référentiels de données : le [!DNL data lake] et le magasin de profils.

Le **[!DNL data lake]** remplit principalement les fonctions suivantes :

* Il sert de zone de test pour l’intégration des données dans Experience Platform.
* Il sert de stockage de données à long terme pour toutes les données Experience Platform.
* Il permet des cas d’utilisation tels que l’analyse des données et la science des données.

Le **magasin de profils** permet de créer les profils des clients et remplit principalement les fonctions suivantes :

* Il sert de stockage de données pour les profils utilisés afin de prendre en charge les expériences en temps réel.
* Il permet des cas d’utilisation tels que la segmentation, l’activation et la personnalisation.

>[!NOTE]
>
>Votre accès au [!DNL data lake] peut dépendre du SKU de produit que vous avez acheté. Pour plus d’informations sur les SKU de produit, contactez votre représentant Adobe.

## Utilisation des licences {#license-usage}

Lorsque vous acquérez une licence pour Experience Platform, vous recevez des droits d’utilisation de licence qui varient selon le SKU :

**[!DNL Addressable Audience]** : le nombre total de profils clients autorisés par contrat dans Experience Platform, y compris les profils connus et pseudonymes.

**[!DNL Total Data Volume]** : quantité totale de données disponibles pour le service de profil Adobe Experience Platform à utiliser dans les workflows d’engagement.

La disponibilité de ces mesures et la définition spécifique de chacune d’elles varient en fonction des licences achetées par l’entreprise.

## Tableau de bord d’utilisation de la licence

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher un instantané des données liées aux licences de l’entreprise pour Experience Platform. Les données du tableau de bord s’affichent exactement comme elles apparaissent au moment précis où l’instantané a été pris. L’instantané n’est ni une approximation ni un échantillon des données et le tableau de bord n’est pas mis à jour en temps réel.

Pour plus d’informations, consultez le guide sur l’utilisation [ du tableau de bord d’utilisation des licences dans l’interface utilisateur d’Experience Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

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

### Quelles données importer dans Experience Platform ?

Les données peuvent être ingérées dans un ou plusieurs systèmes dans Experience Platform, à savoir le [!DNL data lake] et/ou le magasin de profils. Cela signifie que des données différentes peuvent exister dans les deux systèmes pour différents cas d’utilisation. Par exemple, vous pouvez conserver des données historiques dans le [!DNL data lake], mais pas dans le magasin de profils. Vous pouvez sélectionner les données à envoyer au magasin de profils en activant un jeu de données pour l’ingestion de profils.

>[!NOTE]
>
>Votre accès au [!DNL data lake] peut dépendre du SKU de produit que vous avez acheté. Pour plus d’informations sur les SKU de produit, contactez votre représentant Adobe.

### Quelles données conserver ?

Vous pouvez appliquer à la fois des filtres d’ingestion de données et des règles d’expiration pour supprimer les données devenues obsolètes pour vos cas d’utilisation. En règle générale, les données comportementales (telles que les données Analytics) consomment beaucoup plus de stockage que les données d’enregistrement (telles que les données de gestion de la relation client). Par exemple, pour de nombreux utilisateurs d’Experience Platform, les données comportementales constituent à elles seules jusqu’à 90 % des profils, par rapport aux données d’enregistrement. Par conséquent, la gestion des données comportementales est essentielle pour garantir la conformité aux droits de licence.

Vous pouvez utiliser un certain nombre d’outils pour respecter vos droits d’utilisation de licence :

* [Filtres d’ingestion](#ingestion-filters)
* [Magasin de profils](#profile-service)

### Service d’identités et audience adressable {#identity-service}

Les graphiques d’identités ne sont pas pris en compte dans les droits totaux d’audience adressable, car l’audience adressable fait référence à votre nombre total de profils client.

Toutefois, les limites des graphiques d’identités peuvent affecter votre audience adressable en raison du fractionnement des identités. Par exemple, si l’ECID le plus ancien est supprimé du graphique, il continuera d’exister dans le profil client en temps réel sous la forme d’un profil pseudonyme. Vous pouvez définir [Expiration des données de profil pseudonymes](../../profile/pseudonymous-profiles.md) pour contourner ce comportement. Pour plus d’informations, consultez les [mécanismes de sécurité pour les données du Service d’identités](../../identity-service/guardrails.md).

### Filtres d’ingestion {#ingestion-filters}

Les filtres d’ingestion vous permettent d’importer uniquement les données nécessaires à vos cas d’utilisation et d’exclure tous les événements qui ne sont pas requis.

| Filtre d’ingestion | Description |
| --- | --- |
| Filtrage de la source Adobe Audience Manager | Lorsque vous créez une connexion source Adobe Audience Manager, vous pouvez sélectionner les segments et les caractéristiques à importer dans le [!DNL data lake] et le profil client en temps réel, plutôt que d’ingérer l’intégralité des données d’Audience Manager. Pour plus d’informations, consultez le guide sur la [création d’une connexion source Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Préparation de données Adobe Analytics | Vous pouvez utiliser les fonctionnalités de [!DNL Data Prep] lors de la création d’une connexion source Analytics pour filtrer les données qui ne sont pas requises pour vos cas d’utilisation. [!DNL Data Prep] vous permet de définir les attributs/colonnes à publier dans le profil. Vous pouvez également fournir des instructions conditionnelles pour indiquer à Experience Platform si les données doivent être publiées dans le profil ou uniquement dans le [!DNL data lake]. Pour plus d’informations, consultez le guide sur la [création d’une connexion source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Prise en charge de l’activation et de la désactivation des jeux de données pour le profil | Pour ingérer des données dans le profil client en temps réel, vous devez activer un jeu de données à utiliser dans la banque de profils. Ce faisant, vous élargissez l’[!DNL Addressable Audience] et les droits de [!DNL Total Data Volume]. Une fois qu’un jeu de données n’est plus nécessaire pour les cas d’utilisation de profil client, vous pouvez désactiver l’intégration de ce jeu de données au profil afin de vous assurer que vos données restent conformes à la licence. Pour plus d’informations, consultez le guide sur l’[activation et la désactivation des jeux de données pour le profil](../../catalog/datasets/enable-for-profile.md). |
| Exclusion des données du SDK Web et du SDK mobile | Il existe deux types de collecte de données par le SDK Web et Mobile : les données collectées automatiquement et les données collectées explicitement par le développeur. Pour mieux gérer la conformité de licence, vous pouvez désactiver la collecte de données automatique dans la configuration du SDK via le paramètre contextuel. Les données personnalisées peuvent également être supprimées ou ne pas être définies par le développeur. |
| Exclusion des données du transfert côté serveur | Si vous envoyez des données à Experience Platform à l’aide du transfert côté serveur, vous pouvez exclure les données envoyées en supprimant le mappage dans une action de règle pour l’exclure de tous les événements ou en ajoutant des conditions à la règle afin que les données ne se déclenchent que pour certains événements. Pour plus d’informations, consultez la documentation sur les [événements et conditions](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if). |
| Filtrer des données au niveau de la source | Vous pouvez utiliser des opérateurs logiques et de comparaison pour filtrer les données au niveau des lignes à partir de vos sources avant de créer une connexion et d’ingérer des données vers Experience Platform. Pour plus d’informations, consultez le guide sur le [filtrage des données au niveau des lignes pour une source à l’aide de l’ [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Magasin de profils {#profile-service}

Le magasin de profils se compose des composants suivants :

| Composant de magasin de profils | Description |
| --- | --- |
| Fragments de profil | Chaque profil client est composé de plusieurs **fragments de profil** qui ont été fusionnés afin d’obtenir une vue unique de ce client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs **fragments de profil** associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Experience Platform, ils sont assemblés à l’aide du graphique d’identités afin de créer un profil unique pour ce client. Les **fragments de profil** se composent d’un espace de noms d’identité comme identifiant, avec les données d’enregistrement et/ou les données de série temporelle associées. |
| Données d’enregistrement (attributs) | Un profil est la représentation d’un sujet, d’une organisation ou d’un individu. Il est composé de nombreux **attributs** (également appelés **données d’enregistrement**). Par exemple, le profil d’un produit peut inclure un SKU et une description, tandis que le profil d’une personne contient des informations telles que le prénom, le nom et l’adresse e-mail. Le volume des **données d’enregistrement** est généralement faible/modéré, mais leur valeur reste élevée pendant de longues périodes. |
| Données de série temporelle (comportement) | Les **données de série temporelle** fournissent des informations sur le comportement d’un utilisateur. Représentées par la classe de schéma standard du modèle de données d’expérience (XDM) [!DNL ExperienceEvent], les données de série temporelle peuvent décrire des événements tels que l’ajout d’articles à un panier, l’utilisation de liens et la lecture de vidéos. La valeur du comportement peut diminuer au fil du temps. |
| Espace de noms d’identité (identités) | Une fois réunies, les données client sont fusionnées en un profil unique grâce aux **espaces de noms d’identité** et à la possibilité d’assembler ces identités lors de l’acquisition d’informations supplémentaires sur le client. Pour plus d’informations, consultez la [présentation des espaces de noms d’identité](../../identity-service/features/namespaces.md). |

{style="table-layout:auto"}

#### Rapports sur la composition du magasin de profils

Plusieurs rapports sont disponibles pour vous aider à comprendre la composition de la banque de profils. Ces rapports vous aident à prendre des décisions éclairées sur la définition des expirations d’événements d’expérience et sur leur emplacement, afin d’optimiser l’utilisation de votre licence :

* **API Dataset Overlap Report** : indique les jeux de données qui contribuent le plus à l’audience adressable. Vous pouvez utiliser ce rapport pour identifier les jeux de données [!DNL ExperienceEvent] pour lesquels définir une expiration. Pour plus d’informations, consultez le tutoriel sur la [génération du rapport de chevauchement de jeux de données](../../profile/tutorials/dataset-overlap-report.md).
* **API Identity Overlap Report** : indique les espaces de noms d’identité qui contribuent le plus à l’audience adressable. Pour plus d’informations, consultez le tutoriel sur la [génération du rapport de chevauchement d’identités](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report).
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Expirations des données de profils pseudonymes {#pseudonymous-profile-expirations}

Cette fonctionnalité vous permet de supprimer automatiquement les profils pseudonymes obsolètes de la banque de profils. Pour plus d’informations sur cette fonctionnalité, veuillez lire la [ Présentation de l’expiration des données de profils pseudonymes ](../../profile/pseudonymous-profiles.md).

#### Expirations des événements d’expérience {#event-expirations}

Cette fonctionnalité vous permet de supprimer automatiquement les données comportementales d’un jeu de données activé pour Profile qui n’a plus de valeur pour vos cas d’utilisation. Consultez la présentation sur l’[expiration des événements d’expérience](../../profile/event-expirations.md) pour plus d’informations sur le fonctionnement de ce processus une fois qu’il est activé pour un jeu de données.

## Résumé des bonnes pratiques pour la conformité de l’utilisation des licences {#best-practices}

Vous trouverez ci-dessous une liste des bonnes pratiques recommandées pour garantir une meilleure conformité aux droits d’utilisation de licence :

* Utilisez le [tableau de bord d’utilisation de la licence](../../dashboards/guides/license-usage.md) pour suivre et surveiller les tendances d’utilisation des clients. Vous pouvez ainsi anticiper les potentiels dépassements qui peuvent survenir.
* Configurez les [filtres d’ingestion](#ingestion-filters) en identifiant les événements requis pour les cas d’utilisation de segmentation et de personnalisation. Cela vous permet d’envoyer uniquement les événements importants nécessaires aux cas d’utilisation.
* Assurez-vous que vous n’avez [activé que les jeux de données pour le profil](#ingestion-filters) qui sont nécessaires aux d’utilisation de segmentation et de personnalisation.
* Configurez les options [Expiration des événements d’expérience](#event-expirations) et [Expiration des données de profils pseudonymes](#pseudonymous-profile-expirations) pour les données haute fréquence, telles que les données web.
* Vérifiez régulièrement les [rapports sur la composition de profils](#profile-store-composition-reports) pour comprendre la composition de votre banque de profils. Cela vous permet de comprendre les sources de données qui contribuent le plus à la consommation de l’utilisation des licences.

## Résumé et disponibilité des fonctionnalités {#feature-summary}

Les bonnes pratiques et outils décrits dans ce document vous aideront à mieux gérer les droits d’utilisation de licence dans Adobe Experience Platform. Ce document sera mis à jour lorsque des fonctionnalités supplémentaires seront disponibles pour offrir visibilité et contrôle à tous les clients Experience Platform.

Le tableau suivant présente la liste des fonctionnalités actuellement disponibles afin de mieux gérer les droits d’utilisation de licence.

| Fonctionnalité | Description |
| --- | --- |
| [Activation/désactivation de jeux de données pour le profil](../../catalog/datasets/user-guide.md) | Activez ou désactivez l’ingestion du jeu de données dans le profil client en temps réel. |
| [Expirations des événements d’expérience](../../profile/event-expirations.md) | Appliquez un délai d’expiration pour tous les événements ingérés dans un jeu de données activé pour Profile. Contactez votre équipe de compte Adobe ou l’assistance clientèle pour activer cette fonctionnalité. |
| [Filtres de préparation de données Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Appliquez des filtres [!DNL Kafka] pour exclure les données inutiles de l’ingestion |
| [Filtres de connecteur source Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Appliquez des filtres de connexion source Audience Manager pour exclure les données inutiles de l’ingestion. |
| [Filtres de données de transfert d’événement](../../tags/ui/event-forwarding/overview.md) | Appliquez des filtres [!DNL Kafka] côté serveur pour exclure les données inutiles de l’ingestion.  Pour plus d’informations, consultez la documentation sur les [règles de balise](../../tags/ui/managing-resources/rules.md). |
| [Interface utilisateur du tableau de bord d’utilisation de la licence](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Affichez un instantané des données liées aux licences de l’entreprise pour Experience Platform. |
| [API Dataset Overlap Report](../../profile/tutorials/dataset-overlap-report.md) | Génère les jeux de données qui contribuent le plus à l’audience adressable. |
| [API Identity Overlap Report](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Génère les espaces de noms d’identité qui contribuent le plus à l’audience adressable. |

{style="table-layout:auto"}
