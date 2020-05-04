---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Adobe Analytics dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: d2f8e11591b30a0bfd345e56a33a8bb62501358c

---


# Création d’un connecteur source Adobe Analytics dans l’interface utilisateur

Ce didacticiel décrit la procédure à suivre pour créer un connecteur source Adobe Analytics dans l’interface utilisateur afin d’importer des données de consommation dans Adobe Experience Platform.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

## Création d’une connexion source avec Adobe Analytics

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail des sources. L’écran *Catalogue* affiche les sources disponibles pour créer des connexions entrantes avec, et chaque source affiche le nombre de comptes et de flux de jeux de données existants qui leur sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie des applications ** Adobe, sélectionnez **[!UICONTROL Adobe Analytics]** pour afficher une barre d’informations sur le côté droit de l’écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour vue des comptes existants, sélectionnez **[!UICONTROL Accounts]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Sélectionner des données

L’étape *Adobe Analytics* s’affiche. Les flux de jeux de données précédemment établis pour Analytics sont répertoriés dans cet écran. Vous pouvez créer un flux de jeux de données en cliquant sur **[!UICONTROL Select data]**.

>[!NOTE] Plusieurs connexions entrantes à une source peuvent être établies pour apporter différentes données.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

Dans la liste des suites de rapports disponibles, sélectionnez celle que vous souhaitez importer dans la plateforme et cliquez sur **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Nommer votre flux de données

L’étape détaillée *du flux de* jeux de données s’affiche, où vous devez fournir un nom et une description facultative du flux de jeux de données. Sélectionnez **[UICONTROL ! Suivant]** lorsque terminé.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### Vérifier le flux de vos jeux de données

L’étape *Révision* s’affiche, ce qui vous permet de revoir votre nouveau flux de jeux de données liés à Analytics avant de le créer. Les détails de la connexion sont regroupés par catégorie, notamment :

* *Connexion*: Affiche le type de connexion source et la suite de rapports sélectionnée.
* *Affectez des champs* de jeu de données et de mappage : Lors de la création d’autres connecteurs source, ce conteneur indique dans quel jeu de données les données source sont imbriquées, y compris le schéma auquel adhère le jeu de données. Le schéma de sortie et le jeu de données sont automatiquement configurés pour les flux de jeux de données Analytics.

![](../../../../images/tutorials/create/analytics/review.png)

### Surveiller le flux de vos jeux de données

Une fois le flux de votre jeu de données créé, vous pouvez surveiller les données qui y sont ingérées. Dans l’écran *Catalogue* , sélectionnez Flux *de* données pour vue d’une liste de flux établis associés à votre compte Analytics.

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

Le panneau *Modifier les étiquettes* de gouvernance s’affiche. Cet écran vous permet d&#39;accéder et de modifier le contrat, l&#39;identité et les étiquettes sensibles d&#39;un flux de données.

Pour plus d’informations sur la manière d’étiqueter les données provenant d’Analytics, consultez le guide [des étiquettes d’utilisation des](../../../../../data-governance/labels/user-guide.md)données.

![](../../../../images/tutorials/create/analytics/labels.png)

## Étapes suivantes

Une fois la connexion créée, un schéma de cible et un flux de jeux de données sont automatiquement créés pour contenir les données entrantes. En outre, le renvoi des données se produit et ingère jusqu&#39;à 13 mois de données historiques. Une fois l’assimilation initiale terminée, les données Analytics sont utilisées par les services de plateforme en aval, tels que le service de Profil client en temps réel et le service de segmentation. Pour plus d’informations, voir les documents suivants :

* [Présentation du profil client en temps réel](../../../../../profile/home.md)
* [Présentation du service de segmentation](../../../../../segmentation/home.md)
* [Présentation de Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Présentation du service Requête](../../../../../query-service/home.md)
