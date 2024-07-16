---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;campaign;campaign managed services
title: Créer une connexion source Adobe Campaign Managed Cloud Services à l’aide de l’interface utilisateur de Platform
description: Découvrez comment connecter Adobe Experience Platform à Adobe Campaign Managed Cloud Services à l’aide de l’interface utilisateur de Platform.
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 46%

---

# Créer une connexion source Adobe Campaign Managed Cloud Services à l’aide de l’interface utilisateur de Platform

Ce tutoriel décrit les étapes à suivre pour créer une connexion source afin d’apporter vos données Adobe Campaign Managed Cloud Services à Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [Sandbox](../../../../../sandboxes/home.md) : Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Connexion de Adobe Campaign Managed Cloud Services à Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également utiliser la barre de recherche pour réduire les sources affichées.

Sous la catégorie **[!UICONTROL Adobe applications]**, sélectionnez **[!UICONTROL Adobe Campaign Managed Cloud Services]**, puis **[!UICONTROL Ajouter des données]**.

![Catalogue des sources affichant la carte Adobe Campaign Managed Cloud Services.](../../../../images/tutorials/create/campaign/catalog.png)

### Sélectionner les données {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Instance d&#39;environnement Adobe Campaign"
>abstract="Nom de l&#39;environnement Adobe Campaign que vous souhaitez utiliser."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Mapping de ciblage"
>abstract="Les mappings de ciblage sont des objets techniques utilisés par Campaign pour diffuser des messages. Ils contiennent tous les paramètres techniques nécessaires à l’envoi de diffusions (adresses, numéros de téléphone, indicateurs d’accord préalable, identifiants additionnels, etc.)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Nom du schéma"
>abstract="Nom de l’entité définie dans la base de données Adobe Campaign."
>text="Learn more in documentation"

L’étape [!UICONTROL Sélectionner les données] s’affiche et vous fournit une interface pour configurer votre [!UICONTROL instance Adobe Campaign], le [!UICONTROL mapping de ciblage] et le [!UICONTROL nom du schéma].

| Propriété | Description |
| --- | --- |
| Instance Adobe Campaign | Nom de l’instance d’environnement Adobe Campaign que vous utilisez. |
| Mapping de ciblage | Les objets techniques utilisés par Campaign pour diffuser des messages et contiennent tous les paramètres techniques requis pour envoyer des diffusions. |
| Nom du schéma | Nom de l’entité de schéma que vous apportez à Platform. Les options incluent Journal de diffusion et Journal de suivi. |

![Interface dans laquelle vous pouvez configurer votre instance Adobe Campaign, le mapping de ciblage et le nom du schéma.](../../../../images/tutorials/create/campaign/select-data.png)

Une fois que vous avez renseigné les valeurs de votre instance Campaign, du mapping de ciblage et du nom du schéma, l’écran se met à jour pour afficher un aperçu de votre schéma ainsi qu’un exemple de jeu de données. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![ Aperçu de la hiérarchie de votre schéma ainsi qu’un exemple de votre jeu de données ](../../../../images/tutorials/create/campaign/preview.png)

### Utiliser un jeu de données existant

La page [!UICONTROL Détails du flux de données] vous permet de choisir si vous souhaitez utiliser un jeu de données existant ou configurer un nouveau jeu de données pour votre flux de données.

Pour utiliser un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Vous pouvez soit récupérer un jeu de données existant à l’aide de l’option de [!UICONTROL Recherche avancée], soit en faisant défiler la liste des jeux de données existants dans le menu déroulant.

Une fois un jeu de données sélectionné, donnez un nom à votre flux de données et une description facultative.

![Interface affichant l’option de jeu de données existant.](../../../../images/tutorials/create/campaign/existing-dataset.png)

### Utiliser un nouveau jeu de données

Pour utiliser un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**, puis fournissez un nom de jeu de données de sortie et une description facultative. Sélectionnez ensuite un schéma à mapper à l’aide de l’option [!UICONTROL Recherche avancée] ou en faisant défiler la liste des schémas existants dans le menu déroulant. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Interface affichant la nouvelle option de jeu de données.](../../../../images/tutorials/create/campaign/new-dataset.png)

### Activer les alertes

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données. Sélectionnez une alerte dans la liste pour vous abonner et recevoir des notifications sur l’état de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des sources dans l’interface utilisateur](../../alerts.md).

Lorsque vous avez terminé de renseigner votre flux de données, sélectionnez **[!UICONTROL Suivant]**.

![Une sélection de différents types d’alerte que vous pouvez activer pour votre flux de données.](../../../../images/tutorials/create/campaign/alerts.png)

### Mappage des champs de données à un schéma XDM

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [guide de l’interface utilisateur de la préparation des données](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>Lors du mappage de vos champs source aux champs XDM cible, vous devez vous assurer que vous mappez votre champ d’identité principale désigné avec son champ XDM cible approprié.

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![Arborescence de mappage avec quatre champs de données source mappés à leurs champs de schéma XDM correspondants.](../../../../images/tutorials/create/campaign/mapping.png)

### Vérifier le flux de données

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![Une page de révision présentant des informations sur la connexion et le jeu de données.](../../../../images/tutorials/create/campaign/review.png)

### Surveillance de l’activité du jeu de données

Une fois votre flux de données créé, vous pouvez surveiller les données qui sont ingérées par celui-ci pour afficher des informations sur les taux ingérés et les lots réussis et en échec.

Pour commencer à afficher votre activité de jeu de données, sélectionnez **[!UICONTROL Flux de données]** dans le catalogue de sources.

![Page du catalogue des sources avec l’onglet de l’en-tête du flux de données sélectionné.](../../../../images/tutorials/create/campaign/dataflows.png)

Sélectionnez ensuite le jeu de données cible dans la liste des flux de données qui s’affichent.

![Liste des flux de données existants avec le jeu de données cible Logs de diffusion Adobe Campaign sélectionné.](../../../../images/tutorials/create/campaign/target-dataset.png)

La page d’activité du jeu de données s’affiche. À partir de là, vous pouvez consulter des informations sur les performances de votre flux de données, notamment le taux d’ingestion, les lots réussis et les lots en échec.

Cette page vous fournit également une interface permettant de mettre à jour la description des métadonnées de votre flux de données, d’activer les diagnostics d’ingestion et d’erreur partiels et d’ajouter de nouvelles données à votre jeu de données.

![Interface avec des graphiques représentant le taux d’ingestion d’un jeu de données sélectionné.](../../../../images/tutorials/create/campaign/dataset-activity.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour importer vos données de logs de diffusion et de tracking Campaign v8 dans Platform. Ces données entrantes peuvent désormais être utilisées par les services de Platform en aval, comme [!DNL Real-Time Customer Profile] et [!DNL Data Science Workspace]. Consultez les documents suivants pour plus d’informations :

* [Présentation de [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Présentation de [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
