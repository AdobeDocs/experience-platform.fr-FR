---
keywords: Experience Platform;accueil;rubriques populaires;Connecteur source Analytics;Connecteur Analytics;Source Analytics;Analytics
solution: Experience Platform
title: Création d’une connexion source Adobe Analytics dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Adobe Analytics dans l’interface utilisateur pour importer des données client dans Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 06232d4b567ba1d6bed55226aaa08147510c4498
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 8%

---

# Création d’une connexion source Adobe Analytics dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source Adobe Analytics dans l’interface utilisateur afin d’apporter [!DNL Analytics] Données de suite de rapports dans Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Terminologie clé

Il est important de comprendre les termes clés suivants utilisés dans ce document :

* **Attribut standard**: Les attributs standard sont tous les attributs prédéfinis par Adobe. Elles contiennent la même signification pour tous les clients et sont disponibles dans la variable [!DNL Analytics] données sources et [!DNL Analytics] groupes de champs de schéma.
* **Attribut personnalisé**: Les attributs personnalisés sont n’importe quel attribut de la hiérarchie de variables personnalisées dans [!DNL Analytics]. Les attributs personnalisés sont utilisés dans une mise en oeuvre Adobe Analytics pour capturer des informations spécifiques dans une suite de rapports. Leur utilisation peut différer d’une suite de rapports à l’autre. Les attributs personnalisés incluent des eVars, des props et des listes. Voir ce qui suit : [[!DNL Analytics] documentation sur les variables de conversion](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) pour plus d’informations sur les eVars.
* **N’importe quel attribut dans les groupes de champs personnalisés**: Les attributs provenant de groupes de champs créés par les clients sont tous définis par l’utilisateur et ne sont considérés comme des attributs ni standard ni personnalisés.
* **Noms conviviaux**: Les noms conviviaux sont des étiquettes fournies par l’utilisateur pour les variables personnalisées dans une [!DNL Analytics] implémentation. Voir ce qui suit : [[!DNL Analytics] documentation sur les variables de conversion](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) pour plus d’informations sur les noms conviviaux.

## Création d’une connexion source avec Adobe Analytics

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également utiliser la barre de recherche pour réduire les sources affichées.

Sous , **[!UICONTROL Adobe des applications]** catégorie, sélectionnez **[!UICONTROL Adobe Analytics]** puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/analytics/catalog.png)

### Choix des données

Le **[!UICONTROL Ajout de données à la source Analytics]** s’affiche. Sélectionner **[!UICONTROL Suite de rapports]** pour commencer à créer une connexion source pour les données d’une suite de rapports Analytics, puis sélectionnez la suite de rapports à ingérer. Les suites de rapports qui ne peuvent pas être sélectionnées ont déjà été ingérées dans cet environnement de test ou dans un autre environnement de test. Sélectionner **[!UICONTROL Suivant]** pour continuer.

>[!NOTE]
>
>Plusieurs connexions entrantes peuvent être établies pour importer plusieurs suites de rapports, mais une seule suite de rapports peut être utilisée avec Real-time Customer Data Platform à la fois.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Mappage

>[!IMPORTANT]
>
>Prise en charge de la préparation des données pour le [!DNL Analytics] source est actuellement en version bêta. La fonctionnalité et la documentation peuvent être modifiées.

Avant de pouvoir mapper votre [!DNL Analytics] pour cibler un schéma XDM, vous devez d’abord choisir si vous utilisez un schéma par défaut ou un schéma personnalisé.

Un schéma par défaut crée un nouveau schéma à votre place, contenant la variable [!DNL Adobe Analytics ExperienceEvent Template] groupe de champs. Pour utiliser un schéma par défaut, sélectionnez **[!UICONTROL Schéma par défaut]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

Avec un schéma personnalisé, vous pouvez choisir n’importe quel schéma disponible pour votre [!DNL Analytics] tant que ce schéma contient la variable [!DNL Adobe Analytics ExperienceEvent Template] groupe de champs. Pour utiliser un schéma personnalisé, sélectionnez **[!UICONTROL Schéma personnalisé]**.

![custom-schema](../../../../images/tutorials/create/analytics/custom-schema.png)

Le [!UICONTROL Mappage] fournit une interface permettant de mapper les champs sources à leurs champs de schéma cible appropriés. À partir de là, vous pouvez mapper des variables personnalisées à de nouveaux groupes de champs de schéma et appliquer des calculs comme pris en charge par Data Prep. Sélectionnez un schéma cible pour lancer le processus de mappage.

>[!TIP]
>
>Seuls les schémas qui ont la variable [!DNL Adobe Analytics ExperienceEvent Template] les groupes de champs s’affichent dans le menu de sélection de schéma. Les autres schémas sont omis. Si aucun schéma approprié n’est disponible pour les données de votre suite de rapports, vous devez créer un nouveau schéma. Pour obtenir des instructions détaillées sur la création de schémas, consultez le guide sur la [création et modification de schémas dans l’interface utilisateur](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

Le [!UICONTROL Mappage des champs standard] affiche des panneaux pour [!UICONTROL Mappings standard appliqués], [!UICONTROL Mappings standard non correspondants] et [!UICONTROL Mappings personnalisés]. Consultez le tableau suivant pour obtenir des informations spécifiques sur chaque catégorie :

| Mappage des champs standard | Description |
| --- | --- |
| [!UICONTROL Mappings standard appliqués] | Le [!UICONTROL Mappings standard appliqués] affiche le nombre total d’attributs mappés. Les mappages standard font référence aux jeux de mappages entre tous les attributs de la source. [!DNL Analytics] données et attributs correspondants dans [!DNL Analytics] groupe de champs. Ils sont prémappés et ne peuvent pas être modifiés. |
| [!UICONTROL Mappings standard non correspondants] | Le [!UICONTROL Mappings standard non correspondants] fait référence au nombre d’attributs mappés contenant des conflits de nom conviviaux. Ces conflits apparaissent lorsque vous réutilisez un schéma qui comporte déjà un ensemble rempli de descripteurs de champ provenant d’une autre suite de rapports. Vous pouvez procéder comme suit : [!DNL Analytics] flux de données même avec des conflits de nom conviviaux. |
| [!UICONTROL Mappings personnalisés] | Le [!UICONTROL Mappings personnalisés] affiche le nombre d’attributs personnalisés mappés, y compris les eVars, les props et les listes. Les mappages personnalisés font référence aux jeux de mappages entre les attributs personnalisés dans la source. [!DNL Analytics] données et attributs dans les groupes de champs personnalisés inclus dans le schéma sélectionné. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Pour prévisualiser le [!DNL Analytics] Groupe de champs de schéma de modèle ExperienceEvent, sélectionnez **[!UICONTROL Affichage]** dans le [!UICONTROL Mappings standard appliqués] du panneau.

![view](../../../../images/tutorials/create/analytics/view.png)

Le [!UICONTROL Groupe de champs de schéma de modèle Adobe Analytics ExperienceEvent] vous fournit une interface à utiliser pour examiner la structure de votre schéma. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Fermer]**.

![champ-groupe-aperçu](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform détecte automatiquement vos jeux de mappages pour tout conflit de noms convivial. S’il n’y a aucun conflit avec vos jeux de mappages, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![mapping](../../../../images/tutorials/create/analytics/mapping.png)

S’il existe des conflits de nom conviviaux entre votre suite de rapports source et votre schéma sélectionné, vous pouvez continuer avec votre [!DNL Analytics] dataflow, reconnaissant que les descripteurs de champ ne seront pas modifiés. Vous pouvez également choisir de créer un nouveau schéma avec un ensemble vide de descripteurs.

Sélectionner **[!UICONTROL Suivant]** pour continuer.

![attention](../../../../images/tutorials/create/analytics/caution.png)

#### Mappings personnalisés

Pour utiliser les fonctions de préparation de données et ajouter un nouveau mappage ou des champs calculés pour les attributs personnalisés, sélectionnez **[!UICONTROL Affichage des mappages personnalisés]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Ensuite, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**.

Selon vos besoins, vous pouvez sélectionner l’une des options suivantes : **[!UICONTROL Ajouter un nouveau mappage]** ou **[!UICONTROL Ajouter un champ calculé]** des options qui s’affichent.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

Un jeu de mappages vide s’affiche. Sélectionnez l’icône de mappage pour ajouter un champ source.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

Vous pouvez utiliser l’interface pour parcourir la structure du schéma source et identifier le nouveau champ source que vous souhaitez utiliser. Une fois que vous avez sélectionné le champ source à mapper, sélectionnez **[!UICONTROL Sélectionner]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Sélectionnez ensuite l’icône de mappage sous [!UICONTROL Champ cible] pour mapper le champ source sélectionné à son champ cible approprié.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Tout comme le schéma source, vous pouvez utiliser l’interface pour parcourir la structure du schéma cible et sélectionner le champ cible à mapper. Une fois que vous avez sélectionné le champ cible approprié, sélectionnez **[!UICONTROL Sélectionner]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

Une fois votre jeu de mappages personnalisé terminé, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

La documentation suivante fournit d’autres ressources sur la préparation des données, les champs calculés et les fonctions de mappage :

* [Présentation de la préparation des données](../../../../../data-prep/home.md)
* [Fonctions de mappage de la préparation de données](../../../../../data-prep/functions.md)
* [Ajouter des champs calculés](../../../../../data-prep/ui/mapping.md#calculated-fields)

### Fournir des détails sur les flux de données

Le **[!UICONTROL Détails du flux de données]** s’affiche, où vous devez fournir un nom et une description facultative du flux de données. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Suivant]**.

![dataflow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Révision

Le [!UICONTROL Réviser] s’affiche, ce qui vous permet de consulter votre nouveau flux de données Analytics avant qu’il ne soit créé. Les détails de la connexion sont regroupés par catégories, notamment :

* [!UICONTROL Connexion]: Affiche la plateforme source de la connexion.
* [!UICONTROL Type de données]: Affiche la suite de rapports sélectionnée et l’identifiant de suite de rapports correspondant.

![review](../../../../images/tutorials/create/analytics/review.png)

### Surveillance de votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données qui sont ingérées par celui-ci. Dans la [!UICONTROL Catalogue] écran, sélectionnez **[!UICONTROL Flux de données]** pour afficher la liste des flux établis associés à votre compte Analytics.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

Le **Flux de données** s’affiche. Sur cette page, vous trouverez une paire de flux de jeux de données, y compris des informations sur leur nom, les données source, l’heure de création et l’état.

Le connecteur instancie deux flux de jeux de données. L’un représente les données de renvoi, l’autre les données actives. Les données de renvoi ne sont pas configurées pour Profile, mais sont envoyées au lac de données à des fins d’analyse et de cas d’utilisation en science des données.

Pour plus d’informations sur le renvoi, les données actives et leurs latences respectives, voir la section [Présentation d’Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md).

Sélectionnez le flux du jeu de données que vous souhaitez afficher dans la liste.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

Le **[!UICONTROL Activité du jeu de données]** s’affiche. Cette page affiche le taux de messages en cours de consommation sous la forme d&#39;un graphique. Sélectionner **[!UICONTROL Gouvernance des données]** à partir de l’en-tête supérieur pour accéder aux champs d’étiquetage.

![dataset-activity](../../../../images/tutorials/create/analytics/dataset-activity.png)

Vous pouvez afficher les libellés hérités d’un flux de jeux de données à partir du [!UICONTROL Gouvernance des données] écran. Pour plus d’informations sur la manière d’étiqueter les données provenant d’Analytics, consultez la page [guide des libellés d’utilisation des données](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Pour supprimer un flux de données, accédez à la section [!UICONTROL Flux de données] puis sélectionnez les ellipses (`...`) en regard du nom du flux de données, puis sélectionnez [!UICONTROL Supprimer].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Étapes suivantes et ressources supplémentaires

Une fois la connexion créée, le flux de données est automatiquement créé pour contenir les données entrantes et renseigner un jeu de données avec votre schéma sélectionné. En outre, un remplissage de données se produit et ingère jusqu’à 13 mois de données historiques. Une fois l’ingestion initiale terminée, [!DNL Analytics] données et être utilisé par les services Platform en aval, tels que [!DNL Real-time Customer Profile] et Segmentation Service. Pour plus d’informations, consultez les documents suivants :

* [Présentation de [!DNL Real-time Customer Profile]](../../../../../profile/home.md)
* [Présentation de [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Présentation de [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Présentation de [!DNL Query Service]](../../../../../query-service/home.md)

La vidéo suivante est destinée à vous aider à comprendre l’ingestion de données à l’aide du connecteur source Adobe Analytics :

>[!WARNING]
>
> Lʼinterface utilisateur de [!DNL Platform] affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation ci-dessus pour connaître les dernières captures d’écran et fonctionnalités de l’interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
