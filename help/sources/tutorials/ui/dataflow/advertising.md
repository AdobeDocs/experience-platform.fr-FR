---
keywords: Experience Platform;accueil;rubriques les plus consultées;configurer le flux de données;connecteur publicitaire
solution: Experience Platform
title: Création d’un flux de données à l’aide d’une source Advertising dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Platform. Ce tutoriel décrit les étapes à suivre pour créer un flux de données pour une source publicitaire à l’aide de l’interface utilisateur de Platform.
exl-id: 8dd1d809-e812-4a13-8831-189726b2430e
source-git-commit: a9a443eda060606be4394dfc2e2707fe18618160
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 11%

---

# Création d’un flux de données à l’aide d’une source publicitaire dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données dans Adobe Experience Platform. Ce tutoriel décrit les étapes à suivre pour créer un flux de données pour une source publicitaire à l’aide de l’interface utilisateur de Platform.

>[!NOTE]
>
>Pour créer un flux de données, vous devez déjà disposer d’un compte authentifié avec une source publicitaire. Vous trouverez une liste des tutoriels pour créer différents comptes de source publicitaire dans l’interface utilisateur de la section [présentation des sources](../../../home.md#advertising).

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de Platform :

* [Sources](../../../home.md): Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [[!DNL Experience Data Model (XDM)] Système](../../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Data Prep]](../../../../data-prep/home.md): Permet aux ingénieurs de données de mapper, de transformer et de valider des données vers et depuis le modèle de données d’expérience (XDM).

## Ajout de données

Après avoir créé votre compte source de publicité, la variable **[!UICONTROL Ajouter des données]** s’affiche, fournissant une interface vous permettant d’explorer la hiérarchie des tableaux de votre compte de source publicitaire.

* La moitié gauche de l’interface est un navigateur qui affiche la liste des tableaux de données contenus dans votre compte. L’interface comprend également une option de recherche qui vous permet d’identifier rapidement les données source que vous prévoyez d’utiliser.
* La moitié droite de l’interface est un panneau d’aperçu qui vous permet de prévisualiser jusqu’à 100 lignes de données.

>[!NOTE]
>
>L’option de données de source de recherche est disponible pour toutes les sources basées sur un tableau, à l’exception d’Adobe Analytics, [!DNL Amazon Kinesis], et [!DNL Azure Event Hubs].

Une fois que vous avez trouvé les données sources, sélectionnez le tableau, puis sélectionnez **[!UICONTROL Suivant]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## Fournir des détails sur les flux de données

Le [!UICONTROL Détails du flux de données] vous permet de choisir si vous souhaitez utiliser un jeu de données existant ou un nouveau jeu de données. Au cours de ce processus, vous pouvez également configurer les paramètres de [!UICONTROL Jeu de données de profil], [!UICONTROL Diagnostics d’erreur], [!UICONTROL Ingestion partielle], et [!UICONTROL Alertes].

![dataflow-detail](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### Utilisation d’un jeu de données existant

Pour ingérer des données dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Vous pouvez soit récupérer un jeu de données existant à l’aide de l’option de [!UICONTROL Recherche avancée], soit en faisant défiler la liste des jeux de données existants dans le menu déroulant. Une fois que vous avez sélectionné un jeu de données, indiquez un nom et une description pour votre flux de données.

![existing-dataset](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### Utilisation d’un nouveau jeu de données

Pour ingérer un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** puis fournissez un nom de jeu de données de sortie et une description facultative. Sélectionnez ensuite un schéma à mapper à l’aide de l’option [!UICONTROL Recherche avancée] ou en faisant défiler la liste des schémas existants dans le menu déroulant. Une fois que vous avez sélectionné un schéma, indiquez un nom et une description pour votre flux de données.

![new-dataset](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### Activer [!DNL Profile] et diagnostics d’erreur

Sélectionnez ensuite le **[!UICONTROL Jeu de données de profil]** bascule pour activer votre jeu de données [!DNL Profile]. Cela vous permet de créer une vue holistique des attributs et des comportements d’une entité. Données de tous [!DNL Profile]Les jeux de données activés seront inclus dans [!DNL Profile] les modifications et sont appliquées lorsque vous enregistrez votre flux de données.

Le [!UICONTROL diagnostic d’erreur] permet de générer un message d’erreur détaillé pour tout enregistrement erroné survenant dans votre flux de données, tandis que l’[!UICONTROL ingestion partielle] vous permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil que vous définissez manuellement. Pour plus d’informations, consultez la [présentation de l’ingestion par lots partiels](../../../../ingestion/batch-ingestion/partial.md).

![profile-and-errors](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### Activation des alertes

Vous pouvez activer les alertes pour recevoir des notifications sur l’état de votre flux de données. Sélectionnez une alerte dans la liste pour vous abonner afin de recevoir des notifications sur l’état de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de sources à l’aide de l’interface utilisateur](../alerts.md).

Lorsque vous avez terminé de fournir des détails à votre flux de données, sélectionnez **[!UICONTROL Suivant]**.

![alertes](../../../images/tutorials/dataflow/table-based/alerts.png)

## Mappage des champs de données à un schéma XDM

Le [!UICONTROL Mappage] s’affiche, vous fournissant une interface pour mapper les champs source de votre schéma source à leurs champs XDM cibles appropriés dans le schéma cible.

Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs calculées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, reportez-vous à la section [Guide de l’interface utilisateur de la préparation de données](../../../../data-prep/ui/mapping.md).

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![mapping](../../../images/tutorials/dataflow/table-based/mapping.png)

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
| Chargement des données incrémentielles par | Une option avec un ensemble filtré de champs de schéma source de type, date ou heure. Ce champ sert à différencier les données nouvelles des données existantes. Les données incrémentielles seront ingérées en fonction de l’horodatage de la colonne sélectionnée. |

![renvoyer](../../../images/tutorials/dataflow/table-based/backfill.png)

## Vérification du flux de données

Le **[!UICONTROL Réviser]** s’affiche, ce qui vous permet de consulter votre nouveau flux de données avant qu’il ne soit créé. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]**: Affiche le type de source, le chemin d’accès approprié du fichier source choisi et la quantité de colonnes qu’il contient.
* **[!UICONTROL Attribution de champs de jeu de données et de mappage]**: Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.
* **[!UICONTROL Planification]**: Affiche la période, la fréquence et l’intervalle principaux du planning d’ingestion.

Une fois que vous avez examiné votre flux de données, sélectionnez **[!UICONTROL Terminer]** et accorder un certain temps pour la création du flux de données.

![review](../../../images/tutorials/dataflow/table-based/review.png)

## Surveillance de votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les taux d’ingestion, les succès et les erreurs. Pour plus d’informations sur la surveillance du flux de données, consultez le tutoriel sur [surveillance des comptes et des flux de données dans l’interface utilisateur](../monitor.md).

## Suppression de votre flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]** de la fonction **[!UICONTROL Flux de données]** workspace. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur [suppression de flux de données dans l’interface utilisateur](../delete.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour importer des données de votre source publicitaire vers Platform. Les données entrantes peuvent désormais être utilisées par en aval. [!DNL Platform] des services tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, consultez les documents suivants :

* [Présentation de [!DNL Real-time Customer Profile]](../../../../profile/home.md)
* [Présentation de [!DNL Data Science Workspace]](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> L’interface utilisateur de Platform affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation ci-dessus pour connaître les dernières captures d’écran et fonctionnalités de l’interface utilisateur.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)
