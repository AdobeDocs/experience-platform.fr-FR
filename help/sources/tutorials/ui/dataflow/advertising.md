---
keywords: Experience Platform;accueil;rubriques les plus consultées;configurer le flux de données;connecteur publicitaire
solution: Experience Platform
title: Création d’un flux de données à l’aide d’une source Advertising dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Platform. Ce tutoriel décrit les étapes à suivre pour créer un flux de données pour une source publicitaire à l’aide de l’interface utilisateur de Platform.
exl-id: 8dd1d809-e812-4a13-8831-189726b2430e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 50%

---

# Création d’un flux de données à l’aide d’une source publicitaire dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données dans Adobe Experience Platform. Ce tutoriel décrit les étapes à suivre pour créer un flux de données pour une source publicitaire à l’aide de l’interface utilisateur de Platform.

>[!NOTE]
>
>Pour créer un flux de données, vous devez déjà disposer d’un compte authentifié avec une source publicitaire. Vous trouverez une liste des tutoriels pour créer différents comptes de source publicitaire dans l’interface utilisateur de la section [présentation des sources](../../../home.md#advertising).

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Platform : 

* [Sources](../../../home.md) : Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de [!DNL Platform].
* [[!DNL Experience Data Model (XDM)] Système](../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Data Prep]](../../../../data-prep/home.md): Permet aux ingénieurs de données de mapper, de transformer et de valider des données vers et depuis le modèle de données d’expérience (XDM).

## Ajouter des données

Après avoir créé votre compte source de publicité, la variable **[!UICONTROL Ajouter des données]** s’affiche, fournissant une interface vous permettant d’explorer la hiérarchie des tableaux de votre compte de source publicitaire.

* La moitié gauche de l’interface est un navigateur qui affiche la liste des tableaux de données contenus dans votre compte. L’interface comprend également une option de recherche qui vous permet d’identifier rapidement les données source que vous prévoyez d’utiliser.
* La moitié droite de l’interface est un panneau d’aperçu qui vous permet de prévisualiser jusqu’à 100 lignes de données.

>[!NOTE]
>
>L’option de données de source de recherche est disponible pour toutes les sources basées sur un tableau, à l’exception d’Adobe Analytics, [!DNL Amazon Kinesis], et [!DNL Azure Event Hubs].

Une fois que vous avez trouvé les données sources, sélectionnez le tableau, puis sélectionnez **[!UICONTROL Suivant]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## Fournir des détails sur le flux de données

La page [!UICONTROL Détails du flux de données] vous permet de choisir si vous souhaitez utiliser un jeu de données existant ou un nouveau jeu de données. Au cours de ce processus, vous pouvez également configurer les paramètres de [!UICONTROL Jeu de données de profil], [!UICONTROL Diagnostics d’erreur], [!UICONTROL Ingestion partielle] et [!UICONTROL Alertes].

![dataflow-detail](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### Utiliser un jeu de données existant

Pour ingérer vos données dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Vous pouvez soit récupérer un jeu de données existant à l’aide de l’option de [!UICONTROL Recherche avancée], soit faire défiler la liste des jeux de données existants dans le menu déroulant. Une fois que vous avez sélectionné un jeu de données, indiquez un nom et une description pour votre flux de données.

![existing-dataset](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### Utiliser un nouveau jeu de données

Pour procéder à lʼingestion dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**, puis saisissez un nom pour le jeu de données de sortie et une description facultative. Sélectionnez ensuite un schéma à mapper à l’aide de l’option [!UICONTROL Recherche avancée] ou en faisant défiler la liste des schémas existants dans le menu déroulant. Une fois que vous avez sélectionné un schéma, saisissez un nom et une description pour votre flux de données.

![new-dataset](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### Activer [!DNL Profile] et les diagnostics d’erreur

Sélectionnez ensuite le bouton (bascule) du **[!UICONTROL Jeu de données de profil]** pour activer votre jeu de données pour [!DNL Profile]. Cela vous permet de créer une vue holistique des attributs et des comportements d’une entité. Les données issues de tous les jeux de données activés par le [!DNL Profile] seront incluses dans [!DNL Profile] et les modifications sont appliquées lorsque vous enregistrez votre flux de données.

Le [!UICONTROL diagnostic d’erreur] permet de générer un message d’erreur détaillé pour tout enregistrement erroné survenant dans votre flux de données, tandis que l’[!UICONTROL ingestion partielle] vous permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil que vous définissez manuellement. Pour plus d’informations, consultez la [présentation de l’ingestion par lots partiels](../../../../ingestion/batch-ingestion/partial.md).

![profile-and-errors](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### Activer les alertes

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des sources dans l’interface utilisateur](../alerts.md).

Lorsque vous avez terminé de renseigner votre flux de données, sélectionnez **[!UICONTROL Suivant]**.

![alertes](../../../images/tutorials/dataflow/table-based/alerts.png)

## Mappage des champs de données à un schéma XDM

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, reportez-vous à la section [Guide de l’interface utilisateur de la préparation de données](../../../../data-prep/ui/mapping.md).

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![mappage](../../../images/tutorials/dataflow/table-based/mapping.png)

## Planification des exécutions d’ingestion

Le [!UICONTROL Planification] s’affiche, ce qui vous permet de configurer un planning d’ingestion pour ingérer automatiquement les données source sélectionnées à l’aide des mappages configurés. Par défaut, la planification est définie sur `Once`. Pour régler la fréquence d’ingestion, sélectionnez **[!UICONTROL Fréquence]** puis sélectionnez une option dans le menu déroulant.

>[!TIP]
>
>L’intervalle et le renvoi ne sont pas visibles lors d’une ingestion unique.

![scheduling](../../../images/tutorials/dataflow/table-based/scheduling.png)

Si vous définissez votre fréquence d’ingestion sur `Minute`, `Hour`, `Day`ou `Week`, vous devez ensuite définir un intervalle pour établir une période définie entre chaque ingestion. Par exemple, une fréquence d’ingestion définie sur `Day` et un intervalle défini sur `15` signifie que votre flux de données est planifié pour ingérer des données tous les 15 jours.

Au cours de cette étape, vous pouvez également activer **renvoyer** et définissez une colonne pour l’ingestion incrémentielle des données. Le renvoi est utilisé pour ingérer des données historiques, tandis que la colonne que vous définissez pour l’ingestion incrémentielle permet de différencier les nouvelles données des données existantes.

Consultez le tableau ci-dessous pour plus d’informations sur les configurations de planification.

| Champ | Description |
| --- | --- |
| Fréquence | Fréquence d’ingestion. Les fréquences sélectionnées incluent `Once`, `Minute`, `Hour`, `Day`, et `Week`. |
| Intervalle | Entier qui définit l’intervalle pour la fréquence sélectionnée. La valeur de l’intervalle doit être un entier non nul et doit être définie sur supérieur ou égal à 15. |
| Heure de début | Horodatage UTC indiquant quand la toute première ingestion est configurée pour se produire. L’heure de début doit être supérieure ou égale à l’heure UTC actuelle. |
| Renvoi | Valeur boolean qui détermine les données ingérées initialement. Si le renvoi est activé, tous les fichiers actuels du chemin spécifié seront ingérés lors de la première ingestion planifiée. Si le renvoi est désactivé, seuls les fichiers chargés entre la première exécution de l’ingestion et l’heure de début seront ingérés. Les fichiers chargés avant l’heure de début ne seront pas ingérés. |
| Chargement des données incrémentielles par | Une option avec un ensemble filtré de champs de schéma source de type, date ou heure. Ce champ sert à différencier les données nouvelles des données existantes. Les données incrémentielles seront ingérées en fonction de la date et de l’heure de la colonne sélectionnée. |

![renvoyer](../../../images/tutorials/dataflow/table-based/backfill.png)

## Vérifier le flux de données

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.
* **[!UICONTROL Planification]**: Affiche la période, la fréquence et l’intervalle principaux du planning d’ingestion.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![review](../../../images/tutorials/dataflow/table-based/review.png)

## Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées et afficher les informations relatives au taux d’ingestion, aux succès et aux erreurs. Pour plus d’informations sur la surveillance du flux de données, consultez le tutoriel sur [surveillance des comptes et des flux de données dans l’interface utilisateur](../monitor.md).

## Supprimer le flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]**, disponible dans l’espace de travail **[!UICONTROL Flux de données]**. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur la [suppression de flux de données dans l’interface utilisateur](../delete.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour importer des données de votre source publicitaire vers Platform. Les données entrantes peuvent désormais être utilisées par les services [!DNL Platform] en aval tels que [!DNL Real-Time Customer Profile] et [!DNL Data Science Workspace]. Consultez les documents suivants pour plus d’informations :

* [Présentation de [!DNL Real-Time Customer Profile]](../../../../profile/home.md)
* [Présentation de [!DNL Data Science Workspace]](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> L’interface utilisateur de Platform affichée dans la vidéo suivante est obsolète. Consultez la documentation pour découvrir les dernières captures dʼécran et fonctionnalités de lʼinterface utilisateur.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)
