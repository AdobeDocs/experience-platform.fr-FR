---
keywords: Experience Platform;accueil;rubriques populaires;connecteur d’automatisation du marketing
solution: Experience Platform
title: Créer un flux de données à l’aide d’un Source d’automatisation du marketing dans l’interface utilisateur
type: Tutorial
description: Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Experience Platform. Ce tutoriel décrit les étapes à suivre pour créer un flux de données pour une source d’automatisation marketing à l’aide de l’interface utilisateur d’Experience Platform.
exl-id: 8d31fc2d-b952-44f7-98e7-f51b0acc19ed
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 40%

---

# Créer un flux de données à l’aide d’une source d’automatisation marketing dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données dans Adobe Experience Platform. Ce tutoriel décrit les étapes à suivre pour créer un flux de données pour une source d’automatisation marketing à l’aide de l’interface utilisateur d’Experience Platform.

>[!NOTE]
>
>* Pour créer un flux de données, vous devez déjà disposer d’un compte authentifié avec une source d’automatisation du marketing. Vous trouverez une liste de tutoriels sur la création de différents comptes sources d’automatisation marketing dans l’interface utilisateur dans la [présentation des sources](../../../home.md#marketing-automation).
>* Pour qu’Experience Platform ingère des données, les fuseaux horaires de toutes les sources de lots basées sur un tableau doivent être configurés au format UTC.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [Sources](../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM)] Système](../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Data Prep]](../../../../data-prep/home.md) : permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

## Ajouter des données

Une fois votre compte source d’automatisation marketing créé, l’étape **[!UICONTROL Ajouter des données]** s’affiche, vous permettant d’explorer la hiérarchie des tableaux de votre compte source d’automatisation marketing.

* La moitié gauche de l’interface est un navigateur, qui affiche une liste des tableaux de données contenus dans votre compte. L’interface comprend également une option de recherche qui vous permet d’identifier rapidement les données sources que vous avez l’intention d’utiliser.
* La moitié droite de l’interface est un panneau de prévisualisation, qui vous permet de prévisualiser jusqu’à 100 lignes de données.

>[!NOTE]
>
>L’option Rechercher les données sources est disponible pour toutes les sources basées sur des tableaux, à l’exclusion d’Adobe Analytics, de [!DNL Amazon Kinesis] et de [!DNL Azure Event Hubs].

Une fois les données sources trouvées, sélectionnez la table, puis sélectionnez **[!UICONTROL Suivant]**.

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

Experience Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [ Guide de l’interface utilisateur de la préparation des données ](../../../../data-prep/ui/mapping.md).

Une fois vos données source mappées, sélectionnez **[!UICONTROL Suivant]**.

![mappage](../../../images/tutorials/dataflow/table-based/mapping.png)

## Planifier des exécutions d’ingestion

L’étape [!UICONTROL Planification] s’affiche et vous permet de configurer un planning d’ingestion pour ingérer automatiquement les données source sélectionnées à l’aide des mappages configurés. Par défaut, la planification est définie sur `Once`. Pour ajuster la fréquence d’ingestion, sélectionnez **[!UICONTROL Fréquence]** puis sélectionnez une option dans le menu déroulant.

>[!TIP]
>
>L’intervalle et le renvoi ne sont pas visibles lors d’une ingestion unique.

![planification](../../../images/tutorials/dataflow/table-based/scheduling.png)

Si vous définissez la fréquence d’ingestion sur `Minute`, `Hour`, `Day` ou `Week`, vous devez définir un intervalle pour établir un intervalle défini entre chaque ingestion. Par exemple, une fréquence d’ingestion définie sur `Day` et un intervalle défini sur `15` signifie que votre flux de données est planifié pour ingérer des données tous les 15 jours.

Au cours de cette étape, vous pouvez également activer le **renvoi** et définir une colonne pour l’ingestion incrémentielle des données. Le renvoi est utilisé pour ingérer des données historiques, tandis que la colonne que vous définissez pour l’ingestion incrémentielle permet de différencier les nouvelles données des données existantes.

Pour plus d’informations sur les configurations de planification, consultez le tableau ci-dessous.

| Configuration de la planification | Description |
| --- | --- |
| Fréquence | Configurez la fréquence pour indiquer la fréquence d’exécution du flux de données. Vous pouvez définir la fréquence sur : <ul><li>**Une fois** : définissez votre fréquence sur `once` pour créer une ingestion unique. Les configurations d’intervalle et de renvoi ne sont pas disponibles lors de la création d’un flux de données d’ingestion unique. Par défaut, la fréquence de planification est définie sur une seule fois.</li><li>**Minute** : définissez la fréquence sur `minute` pour planifier le flux de données afin d’ingérer les données par minute.</li><li>**Heure** : définissez la fréquence sur `hour` pour planifier l’ingestion des données par flux et par heure.</li><li>**Jour** : définissez la fréquence sur `day` pour planifier l’ingestion de données par jour dans le flux de données.</li><li>**Semaine** : définissez la fréquence sur `week` pour planifier l’ingestion de données par semaine dans le flux de données.</li></ul> |
| Intervalle | Une fois que vous avez sélectionné une fréquence, vous pouvez configurer le paramètre d’intervalle afin d’établir la période entre chaque ingestion. Par exemple, si vous définissez la fréquence sur jour et configurez l’intervalle sur 15, votre flux de données s’exécutera tous les 15 jours. Vous ne pouvez pas définir l’intervalle sur zéro. La valeur d’intervalle minimale acceptée pour chaque fréquence est la suivante :<ul><li>**Une fois** : s.o.</li><li>**Minute** : 15</li><li>**Heure** : 1</li><li>**Jour** : 1</li><li>**Semaine** : 1</li></ul> |
| Heure de début | Date et heure de l’exécution projetée, présentées dans le fuseau horaire UTC. |
| Renvoyer | Le renvoi détermine les données initialement ingérées. Si le renvoi est activé, tous les fichiers actuels du chemin spécifié seront ingérés lors de la première ingestion planifiée. Si le renvoi est désactivé, seuls les fichiers chargés entre la première exécution de l’ingestion et l’heure de début sont ingérés. Les fichiers chargés avant l’heure de début ne seront pas ingérés. |
| Charger les données incrémentielles par | Une option avec un ensemble filtré de champs de schéma source de type, date ou heure. Le champ que vous sélectionnez pour **[!UICONTROL Charger les données incrémentielles par]** doit avoir ses valeurs de date et d’heure dans le fuseau horaire UTC pour charger correctement les données incrémentielles. Toutes les sources de lots basées sur une table prélèvent des données incrémentielles en comparant une valeur d’horodatage de colonne delta à l’heure UTC de la fenêtre d’exécution de flux correspondante, puis en copiant les données de la source, si de nouvelles données sont trouvées dans la fenêtre temporelle UTC. |

![renvoi](../../../images/tutorials/dataflow/table-based/backfill.png)

## Vérifier le flux de données

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.
* **[!UICONTROL Planification]** : affiche la période active, la fréquence et l’intervalle du planning d’ingestion.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![review](../../../images/tutorials/dataflow/table-based/review.png)

## Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées et afficher les informations relatives au taux d’ingestion, aux succès et aux erreurs. Pour plus d’informations sur la surveillance des flux de données, consultez le tutoriel sur la [surveillance des comptes et des flux de données dans l’interface utilisateur](../monitor.md).

## Supprimer le flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]**, disponible dans l’espace de travail **[!UICONTROL Flux de données]**. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur la [suppression de flux de données dans l’interface utilisateur](../delete.md).

## Étapes suivantes

Ce tutoriel vous a permis de créer un flux de données pour importer les données de votre source d’automatisation marketing dans Experience Platform. Les données entrantes peuvent désormais être utilisées par les services [!DNL Experience Platform] en aval tels que [!DNL Real-Time Customer Profile] et [!DNL Data Science Workspace]. Consultez les documents suivants pour plus d’informations :

* [Présentation de [!DNL Real-Time Customer Profile]](../../../../profile/home.md)
* [Présentation de [!DNL Data Science Workspace]](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> L’interface utilisateur d’Experience Platform affichée dans la vidéo suivante est obsolète. Consultez la documentation pour découvrir les dernières captures dʼécran et fonctionnalités de lʼinterface utilisateur.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)