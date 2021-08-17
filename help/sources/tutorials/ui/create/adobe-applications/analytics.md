---
keywords: Experience Platform;accueil;rubriques populaires;Connecteur source Analytics;Connecteur Analytics;Source Analytics;Analytics
solution: Experience Platform
title: Création d’une connexion source Adobe Analytics dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Adobe Analytics dans l’interface utilisateur pour importer des données client dans Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 0af9290a3143b85311fbbd8d194f4799b0c9a873
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 8%

---

# Création d’une connexion source Adobe Analytics dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source Adobe Analytics dans l’interface utilisateur afin d’importer les données [!DNL Analytics] de suite de rapports dans Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Terminologie clé

Il est important de comprendre les termes clés suivants utilisés dans ce document :

* **Attribut** standard : Les attributs standard sont tous les attributs prédéfinis par Adobe. Ils ont la même signification pour tous les clients et sont disponibles dans les groupes de champs de schéma [!DNL Analytics] et de données source [!DNL Analytics].
* **Attribut** personnalisé : Les attributs personnalisés sont n’importe quel attribut de la hiérarchie de dimension personnalisée dans  [!DNL Analytics]. Ils font également partie des schémas définis par l’Adobe, mais peuvent être interprétés différemment par différents clients. Les attributs personnalisés incluent des eVars, des props et des listes. Pour plus d’informations sur les eVars, consultez la [[!DNL Analytics] documentation suivante sur les variables de conversion](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) .
* **N’importe quel attribut dans les groupes** de champs personnalisés : Les attributs provenant de groupes de champs créés par les clients sont tous définis par l’utilisateur et ne sont considérés comme des attributs ni standard ni personnalisés.
* **Noms** conviviaux : Les noms conviviaux sont des étiquettes fournies par l’utilisateur pour les variables personnalisées dans une  [!DNL Analytics] mise en oeuvre. Pour plus d’informations sur les noms conviviaux, consultez la [[!DNL Analytics] documentation suivante sur les variables de conversion](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) .

## Création d’une connexion source avec Adobe Analytics

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également utiliser la barre de recherche pour réduire les sources affichées.

Dans la catégorie **[!UICONTROL Adobe des applications]** , sélectionnez **[!UICONTROL Adobe Analytics]**, puis **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/analytics/catalog.png)

### Sélectionner des données

L’étape **[!UICONTROL Ajout de données à la source Analytics]** s’affiche. Sélectionnez **[!UICONTROL Suite de rapports]** pour commencer à créer une connexion source pour les données de la suite de rapports Analytics, puis sélectionnez la suite de rapports à ingérer. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

>[!NOTE]
>
>Plusieurs connexions entrantes à une source peuvent être établies pour importer différentes données.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Mappage

>[!IMPORTANT]
>
>La fonctionnalité de prise en charge de la préparation de données pour la source [!DNL Analytics] est en version bêta.

La page [!UICONTROL Mapping] fournit une interface permettant de mapper les champs sources aux champs de schéma cible appropriés. À partir de là, vous pouvez mapper des variables personnalisées à de nouveaux groupes de champs de schéma et appliquer des calculs comme pris en charge par Data Prep. Sélectionnez un schéma cible pour lancer le processus de mappage.

>[!TIP]
>
>Seuls les schémas dont le groupe de champs de modèle est [!DNL Analytics] s’affichent dans le menu de sélection des schémas. Les autres schémas sont omis. Si aucun schéma approprié n’est disponible pour les données de votre suite de rapports, vous devez créer un nouveau schéma. Pour obtenir des instructions détaillées sur la création de schémas, consultez le guide sur la [création et l’édition de schémas dans l’interface utilisateur](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

La section [!UICONTROL Mapper les champs standard] affiche des panneaux pour les [!UICONTROL Mappages standard appliqués], [!UICONTROL Mappings standard non correspondants] et [!UICONTROL Mappages personnalisés]. Consultez le tableau suivant pour obtenir des informations spécifiques sur chaque catégorie :

| Mappage des champs standard | Description |
| --- | --- |
| [!UICONTROL Mappings standard appliqués] | Le panneau [!UICONTROL Mappages standard appliqués] affiche le nombre total d’attributs standard mappés. Les mappages standard se rapportent aux jeux de mappages entre les attributs standard dans les données [!DNL Analytics] source et les attributs standard dans le groupe de champs [!DNL Analytics]. Ils sont prémappés et ne peuvent pas être modifiés. |
| [!UICONTROL Mappings standard non correspondants] | Le panneau [!UICONTROL Mappages standard non correspondants] fait référence au nombre d’attributs standard mappés contenant des conflits de noms conviviaux. Ces conflits apparaissent lorsque vous réutilisez un schéma qui comporte déjà un ensemble de descripteurs de champ renseigné. Vous pouvez poursuivre votre flux de données [!DNL Analytics] même avec des conflits de noms conviviaux. |
| [!UICONTROL Mappings personnalisés] | Le panneau [!UICONTROL Mappages personnalisés] affiche le nombre d’attributs personnalisés mappés, y compris les eVars, les props et les listes. Les mappages personnalisés se rapportent aux jeux de mappages entre les attributs personnalisés dans les données [!DNL Analytics] source et les attributs personnalisés dans le groupe de champs [!DNL Analytics]. Les attributs personnalisés peuvent être mappés à d’autres attributs personnalisés, ainsi qu’à des attributs standard. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Pour prévisualiser le groupe de champs de schéma de modèle ExperienceEvent [!DNL Analytics], sélectionnez **[!UICONTROL Afficher]** dans le panneau [!UICONTROL Mappages standard appliqués] .

![view](../../../../images/tutorials/create/analytics/view.png)

La page [!UICONTROL Groupe de champs de schéma de modèle Adobe Analytics ExperienceEvent] vous offre une interface à utiliser pour examiner la structure de votre schéma. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Fermer]**.

![champ-groupe-aperçu](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform détecte automatiquement vos jeux de mappages pour tout conflit de noms convivial. En l’absence de conflit avec vos jeux de mappages, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![mapping](../../../../images/tutorials/create/analytics/mapping.png)

En cas de conflits de noms conviviaux dans vos jeux de mappages, vous pouvez continuer avec votre flux de données [!DNL Analytics], en reconnaissant que les descripteurs de champ seront les mêmes. Vous pouvez également choisir de créer un nouveau schéma avec un ensemble vide de descripteurs.

Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![attention](../../../../images/tutorials/create/analytics/caution.png)

#### Mappings personnalisés

Pour utiliser les fonctions de préparation de données et ajouter un nouveau mappage ou des champs calculés pour les attributs personnalisés, sélectionnez **[!UICONTROL Afficher les mappages personnalisés]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Sélectionnez ensuite **[!UICONTROL Ajouter un nouveau mappage]**.

Selon vos besoins, vous pouvez sélectionner **[!UICONTROL Ajouter un nouveau mappage]** ou **[!UICONTROL Ajouter un champ calculé]** parmi les options qui s’affichent.

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
* [Ajouter des champs calculés](../../../../../data-prep/calculated-fields.md)

### Fournir des détails sur les flux de données

L’étape **[!UICONTROL Détails du flux de données]** s’affiche, où vous devez fournir un nom et une description facultative du flux de données. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Suivant]**.

![dataflow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Révision

L’étape [!UICONTROL Réviser] s’affiche, ce qui vous permet de passer en revue votre nouveau flux de données Analytics avant qu’il ne soit créé. Les détails de la connexion sont regroupés par catégories, notamment :

* [!UICONTROL Connexion] : Affiche la plateforme source de la connexion.
* [!UICONTROL Type] de données : Affiche la suite de rapports sélectionnée et son identifiant de suite de rapports correspondant.

![review](../../../../images/tutorials/create/analytics/review.png)

### Surveillance de votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données qui sont ingérées par celui-ci. Dans l’écran [!UICONTROL Catalogue], sélectionnez **[!UICONTROL Flux de données]** pour afficher la liste des flux établis associés à votre compte Analytics.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

L’écran **Flux de données** s’affiche. Sur cette page, vous trouverez une paire de flux de jeux de données, y compris des informations sur leur nom, les données source, l’heure de création et l’état.

Le connecteur instancie deux flux de jeux de données. L’un représente les données de renvoi, l’autre les données actives. Les données de renvoi ne sont pas configurées pour Profile, mais sont envoyées au lac de données à des fins d’analyse et de cas d’utilisation en science des données.

Pour plus d’informations sur le renvoi, les données en direct et leurs latences respectives, consultez la [présentation d’Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md).

Sélectionnez le flux du jeu de données que vous souhaitez afficher dans la liste.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

La page **[!UICONTROL Activité du jeu de données]** s’affiche. Cette page affiche le taux de messages en cours de consommation sous la forme d&#39;un graphique. Sélectionnez **[!UICONTROL Gouvernance des données]** dans l’en-tête supérieur pour accéder aux champs d’étiquetage.

![dataset-activity](../../../../images/tutorials/create/analytics/dataset-activity.png)

Vous pouvez afficher les libellés hérités d’un flux de données à partir de l’écran [!UICONTROL Gouvernance des données]. Pour plus d’informations sur la manière d’étiqueter les données provenant d’Analytics, consultez le [guide des libellés d’utilisation des données](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Pour supprimer un flux de données, accédez à la page [!UICONTROL Flux de données] , puis sélectionnez les ellipses (`...`) en regard du nom du flux de données, puis sélectionnez [!UICONTROL Supprimer].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Étapes suivantes et ressources supplémentaires

Une fois la connexion créée, un schéma cible et un flux de données sont automatiquement créés pour contenir les données entrantes. En outre, un remplissage de données se produit et ingère jusqu’à 13 mois de données historiques. Une fois l’ingestion initiale terminée, les données [!DNL Analytics] sont utilisées par les services Platform en aval tels que [!DNL Real-time Customer Profile] et Segmentation Service. Pour plus d’informations, consultez les documents suivants :

* [Présentation d’[!DNL Real-time Customer Profile]](../../../../../profile/home.md)
* [Présentation d’[!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Présentation d’[!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Présentation d’[!DNL Query Service]](../../../../../query-service/home.md)

La vidéo suivante est destinée à vous aider à comprendre l’ingestion de données à l’aide du connecteur source Adobe Analytics :

>[!WARNING]
>
> Lʼinterface utilisateur de [!DNL Platform] affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation ci-dessus pour connaître les dernières captures d’écran et fonctionnalités de l’interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
