---
title: Bonnes pratiques relatives aux droits de licence de gestion des données
description: Découvrez les bonnes pratiques à suivre et les outils que vous pouvez utiliser pour mieux gérer vos droits de licence avec Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 163ff97da651ac3a68b5e37e8745b10440519e6f
workflow-type: tm+mt
source-wordcount: '3390'
ht-degree: 38%

---

# Bonnes pratiques relatives aux droits de licence de gestion des données

Adobe Experience Platform est un système ouvert qui transforme vos données en profils clients fiables qui se mettent à jour en temps réel. Il utilise également des informations basées sur l’IA pour vous permettre de proposer des expériences adaptées sur tous les canaux. Vous pouvez saisir des données de différents types, volumes et historiques dans Experience Platform à l’aide de sources. Vous pouvez ensuite adapter ces données à des cas d’utilisation allant de la segmentation et de la personnalisation à l’analyse et au machine learning.

Experience Platform propose des licences qui déterminent le nombre de profils que vous pouvez créer et la quantité de données que vous pouvez importer. Compte tenu de la capacité à importer n’importe quelle source, volume ou historique de données, il est possible que vous dépassiez vos droits de licence à mesure que les volumes de données augmentent.

Lisez ce guide pour connaître les bonnes pratiques à suivre et les outils que vous pouvez utiliser pour mieux gérer vos droits de licence avec Experience Platform.

## Résumé des fonctionnalités {#summary-of-features}

Utilisez les bonnes pratiques et les outils décrits dans ce document pour mieux gérer les droits d’utilisation de licence dans Experience Platform. Ce document est mis à jour au fur et à mesure que des fonctionnalités supplémentaires sont publiées pour offrir visibilité et contrôle à tous les clients Experience Platform.

Le tableau suivant présente la liste des fonctionnalités actuellement disponibles afin de mieux gérer les droits d’utilisation de licence.

| Fonctionnalité | Description |
| --- | --- |
| [Interface utilisateur du jeu de données - Conservation des données d’événement d’expérience](../../catalog/datasets/user-guide.md#data-retention-policy) | Configurez une période de conservation fixe pour les données dans le lac de données et le magasin de profils. Les enregistrements sont supprimés à la fin de la période de conservation configurée. |
| [Activation/désactivation de jeux de données pour le profil client en temps réel](../../catalog/datasets/user-guide.md) | Activez ou désactivez l’ingestion du jeu de données dans le profil client en temps réel. |
| [Expirations d’événements d’expérience dans la banque de profils](../../profile/event-expirations.md) | Appliquez un délai d’expiration pour tous les événements ingérés dans un jeu de données activé pour Profile. Contactez votre équipe de compte Adobe ou l’assistance clientèle pour activer cette fonctionnalité. |
| [Filtres de préparation de données Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) | Appliquez des filtres [!DNL Kafka] pour exclure les données inutiles de l’ingestion. |
| [Filtres de connecteur source Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Appliquez des filtres de connexion source Audience Manager pour exclure les données inutiles de l’ingestion. |
| [Filtres de données de transfert d’événement](../../tags/ui/event-forwarding/overview.md) | Appliquez des filtres [!DNL Kafka] côté serveur pour exclure les données inutiles de l’ingestion.  Pour plus d’informations, consultez la documentation sur les [règles de balise](../../tags/ui/managing-resources/rules.md). |
| [Interface utilisateur du tableau de bord d’utilisation de la licence](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Surveillez la consommation des produits Experience Platform par votre entreprise par rapport aux droits de licence. Accédez à des instantanés d’utilisation quotidienne, à des tendances prédictives et à des données détaillées au niveau du sandbox pour prendre en charge la gestion proactive des licences. |
| [API Dataset Overlap Report](../../profile/tutorials/dataset-overlap-report.md) | Génère les jeux de données qui contribuent le plus à l’audience adressable. |
| [API Identity Overlap Report](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Génère les espaces de noms d’identité qui contribuent le plus à l’audience adressable. |
| [Expiration des données de profils pseudonymes](../../profile/pseudonymous-profiles.md) | Configurez les délais d’expiration des données pour les profils pseudonymes et supprimez automatiquement les données de la banque de profils. |

{style="table-layout:auto"}

## Présentation du stockage des données dans Experience Platform

Experience Platform se compose principalement de deux référentiels de données : le lac de données et le magasin de profils.

Le lac de données remplit principalement les fonctions suivantes :

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

**[!DNL Addressable Audience]** : nombre total de profils client autorisés par contrat dans Experience Platform, y compris les profils connus et pseudonymes.

**[!DNL Total Data Volume]** : quantité totale de données disponibles pour le profil client en temps réel à utiliser dans les workflows d’engagement.

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

Vous devez également décider d’activer ou non les jeux de données de recherche pour le profil client en temps réel, en plus de les utiliser à des fins de recherche générale. Suivez les conseils ci-dessous pour éviter de dépasser vos limites de licence.

#### Activation du profil pour les jeux de données de recherche {#profile-enablement-lookup-datasets}

Un jeu de données de recherche est un jeu de données que vous activez dans Experience Platform afin que les applications puissent le référencer au moment de l’exécution. Utilisez des jeux de données de recherche pour stocker des informations clés relativement statiques telles que des détails de produit, des métadonnées de magasin ou des configurations d’offre, plutôt que des jeux de données dont l’objectif principal est de contribuer aux attributs de profil (par exemple, nom, e-mail ou niveau de fidélité) ou aux événements d’expérience (par exemple, pages vues ou achats).

Les applications Experience Platform telles que les applications [!DNL Journey Optimizer] et autres applications de prise de décision utilisent ces jeux de données pour récupérer des champs supplémentaires en fonction d’une clé (par exemple, l’ID de produit ou l’ID de magasin) et enrichir les workflows de personnalisation, de prise de décision et d’orchestration. L’activation des jeux de données de recherche pour le profil client en temps réel affecte le volume de données de votre profil. Suivez donc les conseils suivants pour respecter vos droits de licence.

Lorsque vous configurez des jeux de données à des fins de recherche, tenez compte des deux rôles qu’un jeu de données peut jouer dans Experience Platform :

* **Jeux de données de recherche** : autorisez les applications à récupérer des données de référence pour des services tels que la personnalisation et la prise de décision dans [!DNL Journey Optimizer].
* **Jeux de données activés pour Profil** : contribuez des attributs et des événements aux profils clients unifiés dans le profil client en temps réel. Ces jeux de données rendent leurs champs disponibles pour les cas d’utilisation de segmentation et d’activation.

>[!IMPORTANT]
>
>Activez uniquement un jeu de données de recherche pour le profil client en temps réel lorsque vous devez utiliser des champs de ce jeu de données dans le profil client en temps réel (par exemple, pour les définitions d’audience, l’activation ou la segmentation d’entités multiples). L’activation d’un jeu de données de recherche pour le profil client en temps réel augmente le volume des données de profil. Pour plus d’informations, consultez le tutoriel sur la [segmentation d’entités multiples](../../segmentation/tutorials/multi-entity-segmentation.md).

**Quand activer des jeux de données pour le profil client en temps réel**

Activez un jeu de données pour le profil client en temps réel dans les cas suivants :

* Le jeu de données contient des attributs du client que vous devez unifier en profils de clients (par exemple, niveau de fidélité, préférences, informations de compte).
* Le jeu de données contient des événements d’expérience qui contribuent à l’analyse et à la segmentation du comportement des clients.
* Le jeu de données contient des attributs de référence ou d’enrichissement (par exemple, les attributs de produit, de magasin ou de compte) que vous devez utiliser dans les définitions d’audience, y compris la segmentation d’entités multiples ou l’activation en aval.

**Si vous ne souhaitez PAS activer de jeux de données pour le profil client en temps réel :**

Évitez d’activer un jeu de données pour le profil client en temps réel dans les cas suivants :

* Le jeu de données contient des données de référence telles que des catalogues de produits, des détails de SKU, des emplacements de magasin ou d’autres données non client. Vous n’avez pas besoin de ces attributs dans le profil client en temps réel pour la segmentation ou l’activation, y compris la segmentation d’entités multiples.
* Le jeu de données contient des données d’enrichissement qui ne sont utilisées que dans les recherches au moment de l’exécution et qui ne sont pas requises dans le cadre de l’identité du client ou dans les définitions d’audience.

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

### Rapports sur la composition du magasin de profils

Plusieurs rapports sont disponibles pour vous aider à comprendre la composition de la banque de profils. Ces rapports vous aident à prendre des décisions éclairées sur la définition des expirations d’événements d’expérience et sur leur emplacement, afin d’optimiser l’utilisation de votre licence :

* **API Dataset Overlap Report** : indique les jeux de données qui contribuent le plus à l’audience adressable. Vous pouvez utiliser ce rapport pour identifier les jeux de données [!DNL ExperienceEvent] pour lesquels définir une expiration. Pour plus d’informations, consultez le tutoriel sur la [génération du rapport de chevauchement de jeux de données](../../profile/tutorials/dataset-overlap-report.md).
* **API Identity Overlap Report** : indique les espaces de noms d’identité qui contribuent le plus à l’audience adressable. Pour plus d’informations, consultez le tutoriel sur la [génération du rapport de chevauchement d’identités](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report).
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

### Expirations des données de profils pseudonymes {#pseudonymous-profile-expirations}

Utilisez la fonctionnalité d’expiration des données de profils pseudonymes pour supprimer automatiquement de la banque de profils les données qui ne sont plus valides ou utiles pour vos cas d’utilisation. L’expiration des données de profils pseudonymes supprime les enregistrements d’événement et de profil. Par conséquent, ce paramètre réduira les volumes d’audiences adressables. Pour plus d’informations sur cette fonctionnalité, veuillez lire la [ Présentation de l’expiration des données de profils pseudonymes ](../../profile/pseudonymous-profiles.md).

### Interface utilisateur du jeu de données - Conservation du jeu de données d’événement d’expérience {#data-retention}

Configurez les paramètres d’expiration et de conservation des jeux de données pour imposer une période de conservation fixe pour vos données dans le lac de données et le magasin de profils. Une fois la période de conservation terminée, les données sont supprimées. L’expiration des données d’événements d’expérience supprime uniquement les événements et non les données de classe de profil, ce qui réduit le [ volume total de données ](total-data-volume.md) dans les mesures d’utilisation de licence. Pour plus d’informations, consultez le guide sur la [définition d’une politique de conservation des données](../../catalog/datasets/user-guide.md#data-retention-policy).

### Expirations des événements d’expérience de profil {#event-expirations}

Configurez les délais d’expiration pour supprimer automatiquement les données comportementales de votre jeu de données activé pour Profile une fois qu’elles ne sont plus utiles pour vos cas d’utilisation. Lisez la présentation sur l’[Expiration des événements d’expérience](../../profile/event-expirations.md) pour plus d’informations.

## Résumé des bonnes pratiques pour la conformité de l’utilisation des licences {#best-practices}

Vous trouverez ci-dessous une liste des bonnes pratiques recommandées pour garantir une meilleure conformité aux droits d’utilisation de licence :

* Utilisez le [tableau de bord d’utilisation de la licence](../../dashboards/guides/license-usage.md) pour suivre et surveiller les tendances d’utilisation des clients. Vous pouvez ainsi anticiper les potentiels dépassements qui peuvent survenir.
* Configurez les [filtres d’ingestion](#ingestion-filters) en identifiant les événements requis pour les cas d’utilisation de segmentation et de personnalisation. Cela vous permet d’envoyer uniquement les événements importants nécessaires aux cas d’utilisation.
* Assurez-vous que vous n’avez [activé que les jeux de données pour le profil](#ingestion-filters) qui sont nécessaires aux d’utilisation de segmentation et de personnalisation.
* Configurez les options [Expiration des événements d’expérience](../../catalog/datasets/user-guide.md#data-retention-policy) et [Expiration des données de profils pseudonymes](../../profile/pseudonymous-profiles.md) pour les données haute fréquence, telles que les données web.
* Configurez des politiques de conservation [durée de vie (TTL) pour les jeux de données d’événements d’expérience](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) dans le lac de données pour supprimer automatiquement les enregistrements obsolètes et optimiser l’utilisation du stockage en fonction de vos droits de licence.
* Vérifiez régulièrement les [rapports sur la composition de profils](#profile-store-composition-reports) pour comprendre la composition de votre banque de profils. Cela vous permet de comprendre les sources de données qui contribuent le plus à la consommation de l’utilisation des licences.

## Cas pratique : conformité d’utilisation de licence

### Pourquoi envisager ce cas d’utilisation

En vous assurant de votre conformité aux **dispositions relatives à l’utilisation des licences** pour le stockage des lacs de données et des profils, vous pouvez éviter les dépassements, optimiser les coûts et aligner vos politiques de conservation des données sur les besoins de votre entreprise.

### Prérequis et planification

Tenez compte des conditions préalables suivantes dans votre processus de planification :

* **Accès et autorisations** :
   * Assurez-vous de disposer de l’autorisation **Gérer les jeux de données** pour utiliser la durée de vie des événements d’expérience.
   * Assurez-vous de disposer de l’autorisation **Gérer les paramètres de profil** pour utiliser la durée de vie du profil pseudonyme.
* **Présentation de la politique de conservation des données** :
   * Politiques d’entreprise concernant la conservation et la conformité des données
   * Besoins de l’entreprise en matière d’analyse des données et d’intervalles de recherche en amont de segmentation

### Fonctionnalités de l’interface utilisateur, composants Experience Platform et produits Experience Cloud que vous utiliserez

Pour réussir l’implémentation de ce cas d’utilisation, vous devez utiliser plusieurs zones de Adobe Experience Platform. Vérifiez que vous disposez des autorisations de contrôle d’accès basé sur les attributs nécessaires pour toutes ces zones ou demandez à votre administrateur système de les accorder.

* Tableau de bord d’utilisation des licences : affichez l’utilisation actuelle des droits au niveau du sandbox.
* Gestion des jeux de données - Surveillez et gérez les politiques de conservation au niveau des jeux de données.
* Audiences (profil client en temps réel) - Assurez-vous que les règles de segmentation regardent en arrière et s’alignent sur les fenêtres de conservation des données.
* Surveillance et alertes : suivez les mises à jour et obtenez des informations sur les opérations de conservation des jeux de données.

### Comment réaliser le cas d’utilisation : instructions détaillées

Lisez les sections ci-dessous, qui incluent des liens vers d’autres documents, pour effectuer chacune des étapes de la présentation de haut niveau ci-dessus.

**Vérifier l’utilisation actuelle de votre licence**

Tout d’abord, accédez au **tableau de bord d’utilisation des licences** et passez en revue votre utilisation des droits au niveau du sandbox.

>[!BEGINTABS]

>[!TAB  Sandbox de production ]

Utilisez l’interface [!UICONTROL Metrics] pour afficher les mesures d’utilisation des licences. L’interface affiche par défaut des informations sur votre sandbox de production.

![Interface utilisateur du tableau de bord d’utilisation de la licence affichant les mesures d’utilisation de la licence pour un sandbox de production.](../images/data-management/prod-sandbox.png)

>[!TAB Sandbox de développement]

Sélectionnez [!UICONTROL Development] pour afficher les mesures d’utilisation de licence liées à vos sandbox de développement.

![Interface utilisateur du tableau de bord d’utilisation de la licence affichant vos mesures d’utilisation de la licence pour les sandbox de développement.](../images/data-management/dev-sandbox.png)

>[!ENDTABS]

Pour plus d’informations, consultez la documentation relative à l’[utilisation du tableau de bord d’utilisation des licences](../../dashboards/guides/license-usage.md).

**Analyse de l’utilisation du stockage au niveau du jeu de données**

Utilisez la **vue de navigation du jeu de données** pour consulter les mesures d’utilisation de votre jeu de données pour le lac de données et le profil client en temps réel. Sélectionnez les en-têtes de colonne pour **[!UICONTROL Data Lake Storage]** ou **[!UICONTROL Profile Storage]**, puis sélectionnez **[!UICONTROL Sort Descending]** dans le panneau pop-up.

>[!BEGINTABS]

>[!TAB Stockage du lac de données]

Les jeux de données du lac de données sont triés par taille de stockage. Utilisez cette fonctionnalité pour identifier les plus gros consommateurs de stockage dans le lac de données.

![Les jeux de données du lac de données sont triés du plus grand au plus petit.](../images/data-management/data-lake-storage.png)

>[!TAB Stockage des profils]

Les jeux de données dans le profil sont triés par taille de stockage. Utilisez cette fonctionnalité pour identifier les plus gros consommateurs de stockage dans Profile.

![Les jeux de données de Profile sont triés du plus grand au plus petit.](../images/data-management/profile-storage.png)

>[!ENDTABS]

**Évaluation et configuration des règles de rétention**

Ensuite, déterminez si vos jeux de données disposent des politiques de conservation appropriées en fonction des limites de licence et des exigences commerciales pour Analytics et Segmentation. Pour afficher la politique de conservation d’un jeu de données, sélectionnez les points de suspension (`...`) à côté de votre jeu de données, puis sélectionnez **[!UICONTROL Set data retention policy]**.

![Le panneau pop-up avec des options de jeu de données, y compris « Définir une politique de conservation des données »](../images/data-management/set-retention-policy.png)

L’interface *[!UICONTROL Set dataset retention]* s’affiche. Utilisez cette interface pour configurer une politique de rétention pour votre jeu de données. Vous pouvez également l’utiliser pour afficher la quantité d’espace de stockage consommée par votre jeu de données dans le lac de données ou le profil.

![Interface « Définir la conservation des jeux de données ».](../images/data-management/dataset-retention.png)

Vous pouvez analyser plus en détail l’impact de la rétention de votre jeu de données à l’aide du prévisionniste d’impact. Sélectionnez **[!UICONTROL View ExperienceEvent data distribution]** pour afficher un graphique qui affiche votre fenêtre de conservation et le pourcentage total de stockage qui est défini pour expirer.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]**

![Le prévisionniste d’impact depuis l’interface de conservation des jeux de données.](../images/data-management/impact-forecaster.png)

**Valider les modifications de conservation**

Une fois vos politiques de conservation appliquées, vous pouvez utiliser les outils suivants pour valider vos modifications :

* [Mesures d’utilisation des jeux de données](../../catalog/datasets/user-guide.md#enhanced-visibility-of-retention-periods-and-storage-metrics) dans la vue de navigation des jeux de données.
* Le [tableau de bord de surveillance](../../dataflows/ui/monitor.md) pour afficher et analyser l’impact de la rétention.
* Le [tableau de bord d’utilisation des licences](../../dashboards/guides/license-usage.md) pour afficher des instantanés quotidiens, des tendances prédictives et des informations au niveau du sandbox.
