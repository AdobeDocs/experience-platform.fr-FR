---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Adobe Analytics dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 0479f5097b530dd97e28474d8e5eb832e5e44e5a
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 16%

---


# Création d’un connecteur source Adobe Analytics dans l’interface utilisateur

Ce didacticiel décrit les étapes à suivre pour créer un connecteur source Adobe Analytics dans l’interface utilisateur afin d’importer des données de consommation dans Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Créer une connexion source avec Adobe Analytics

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail sources. L’écran *Catalogue* affiche les sources disponibles pour créer des connexions entrantes avec, et chaque source affiche le nombre de comptes et de flux de jeux de données existants qui leur sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie des applications **[!UICONTROL d’]** Adobe, sélectionnez **[!UICONTROL Adobe Analytics]** pour afficher une barre d’informations sur le côté droit de l’écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour vue des comptes existants, sélectionnez **[!UICONTROL Comptes]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Sélectionner des données

L’étape **[!UICONTROL Adobe Analytics]** s’affiche. Les flux de jeux de données précédemment établis pour Analytics sont répertoriés dans cet écran. Vous pouvez créer un flux de jeux de données en cliquant sur **[!UICONTROL Sélectionner les données]**.

>[!NOTE]
>
>Plusieurs connexions entrantes à une source peuvent être établies pour apporter différentes données.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

Dans la liste des suites de rapports disponibles, sélectionnez celle que vous souhaitez importer dans la plateforme et cliquez sur **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Nommer votre flux de données

L’étape détaillée **[!UICONTROL du flux de]** jeux de données s’affiche, où vous devez fournir un nom et une description facultative du flux de jeux de données. Select **[!UICONTROL Next]** when finished.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### Vérifier le flux de vos jeux de données

L’étape **[!UICONTROL Révision]** s’affiche, ce qui vous permet de revoir votre nouveau flux de jeux de données liés à Analytics avant de le créer. Les détails de la connexion sont regroupés par catégorie, notamment :

* **[!UICONTROL Connexion]**: Affiche le type de connexion source et la suite de rapports sélectionnée.
* **[!UICONTROL Attribuer des champs]** de jeu de données et de mappage : Lors de la création d’autres connecteurs source, ce conteneur indique dans quel jeu de données les données source sont imbriquées, y compris le schéma auquel adhère le jeu de données. Le schéma de sortie et le jeu de données sont automatiquement configurés pour les flux de jeux de données Analytics.

![](../../../../images/tutorials/create/analytics/review.png)

### Surveiller le flux de vos jeux de données

Une fois le flux de votre jeu de données créé, vous pouvez surveiller les données qui y sont ingérées. Dans l’écran **[!UICONTROL Catalogue]** , sélectionnez Flux **[!UICONTROL de]** données pour vue d’une liste de flux établis associés à votre compte Analytics.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

L’écran Flux *de* données s’affiche. Cette page contient une paire de flux de jeux de données, y compris des informations sur leur nom, leurs données source, leur heure de création et leur état.

Le connecteur instancie deux flux de jeux de données. L’un représente les données de renvoi et l’autre les données actives. Les données de renvoi ne sont pas configurées pour le Profil, mais sont envoyées au lac de données pour des utilisations analytiques et scientifiques des données.

Pour plus d’informations sur le renvoi, les données actives et leurs latences respectives, voir l’aperçu [du connecteur de données](../../../../connectors/adobe-applications/analytics.md)Analytics.

Sélectionnez le flux de jeux de données que vous souhaitez vue à partir de la liste.

![](../../../../images/tutorials/create/analytics/backfill.png)

La page activité *des* jeux de données s&#39;affiche. Cette page affiche le taux de messages consommés sous forme de graphique. Sélectionnez Gouvernance *des* données dans l’en-tête supérieur pour accéder aux champs d’étiquetage.

![](../../../../images/tutorials/create/analytics/batches.png)

Vous pouvez vue les étiquettes héritées d’un flux de données à partir de l’écran de gouvernance *des* données. Pour accéder à des libellés spécifiques, sélectionnez le bouton Modifier en haut à droite.

![](../../../../images/tutorials/create/analytics/data-gov.png)

The *Edit governance labels* panel appears. Cet écran vous permet d&#39;accéder et de modifier le contrat, l&#39;identité et les étiquettes sensibles d&#39;un flux de données.

Pour plus d’informations sur la manière d’étiqueter les données provenant d’Analytics, consultez le guide [des étiquettes d’utilisation des](../../../../../data-governance/labels/user-guide.md)données.

![](../../../../images/tutorials/create/analytics/labels.png)

## Étapes suivantes et ressources supplémentaires

Une fois la connexion créée, un schéma de cible et un flux de jeux de données sont automatiquement créés pour contenir les données entrantes. En outre, un remplissage de données se produit et ingère jusqu’à 13 mois de données historiques. Une fois l’assimilation initiale terminée, les données Analytics sont utilisées par les services de plateforme en aval, tels que le service de Profil client en temps réel et le service de segmentation. Pour plus d’informations, voir les documents suivants :

* [Présentation du profil client en temps réel](../../../../../profile/home.md)
* [Présentation du service de segmentation](../../../../../segmentation/home.md)
* [Présentation de Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Présentation de Query Service](../../../../../query-service/home.md)

La vidéo suivante est destinée à vous aider à comprendre comment ingérer des données à l’aide du connecteur Adobe Analytics Source :

>[!WARNING]
>
> L’ [!DNL Platform] interface utilisateur affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation ci-dessus pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

