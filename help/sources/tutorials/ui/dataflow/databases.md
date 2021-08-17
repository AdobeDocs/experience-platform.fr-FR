---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteur de base de données
solution: Experience Platform
title: Configuration d’un flux de données pour une connexion à la source de base de données dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Platform. Ce tutoriel décrit les étapes de configuration d’un nouveau flux de données à l’aide de votre compte de base de données.
exl-id: 9fd8a7ec-bbd8-4890-9860-e6defc6cade3
source-git-commit: 46fb08a10bc05dc758bdcb025693f819b980b41a
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 4%

---

# Configuration d’un flux de données pour une connexion à la base de données dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Platform. Ce tutoriel décrit les étapes de configuration d’un nouveau flux de données à l’aide de votre compte de base de données.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel](../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

En outre, ce tutoriel nécessite que vous ayez déjà créé un compte de base de données. Vous trouverez une liste des tutoriels de création de différents connecteurs de base de données dans l’interface utilisateur dans la [présentation des connecteurs source](../../../home.md).

## Sélectionner des données

Une fois le compte de base de données créé, l’étape **[!UICONTROL Sélectionner les données]** s’affiche, vous permettant ainsi d’explorer la hiérarchie de votre base de données dans une interface interactive.

- La moitié gauche de l&#39;interface est un navigateur qui affiche la liste des bases de données de votre compte.
- La moitié droite de l&#39;interface permet de prévisualiser jusqu&#39;à 100 lignes de données.

Vous pouvez utiliser l’option **[!UICONTROL Rechercher]** en haut de la page pour identifier rapidement les données source que vous prévoyez d’utiliser.

>[!NOTE]
>
>L’option de données de source de recherche est disponible pour tous les connecteurs source tabulaires, à l’exception des connecteurs Analytics, Classifications, Hubs d’événements et Kinesis.

Une fois que vous avez trouvé les données source, sélectionnez le répertoire, puis cliquez sur **[!UICONTROL Suivant]**.

![select-data](../../../images/tutorials/dataflow/databases/select-data.png)


## Mappage des champs de données à un schéma XDM

L’étape *Mappage* s’affiche, fournissant une interface interactive pour mapper les données source à un jeu de données Platform.

Sélectionnez un jeu de données dans lequel ingérer les données entrantes. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

### Utilisation d’un jeu de données existant

Pour ingérer des données dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**, puis cliquez sur l’icône du jeu de données.

![](../../../images/tutorials/dataflow/databases/existing-dataset.png)

La boîte de dialogue **[!UICONTROL Sélectionner un jeu de données]** s’affiche. Recherchez le jeu de données que vous souhaitez utiliser, sélectionnez-le, puis cliquez sur **[!UICONTROL Continuer]**.

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### Utilisation d’un nouveau jeu de données

Pour ingérer des données dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis.

Vous pouvez joindre un champ de schéma en entrant un nom de schéma dans la barre de recherche **[!UICONTROL Sélectionner le schéma]**. Vous pouvez également sélectionner l’icône déroulante pour afficher la liste des schémas existants. Vous pouvez également sélectionner **[!UICONTROL Recherche avancée]** pour accéder à l’écran des schémas existants, y compris leurs détails respectifs.

Au cours de cette étape, vous pouvez activer votre jeu de données pour [!DNL Real-time Customer Profile] et créer une vue holistique des attributs et des comportements d’une entité. Les données de tous les jeux de données activés seront incluses dans [!DNL Profile] et des modifications sont appliquées lorsque vous enregistrez votre flux de données.

Active/désactive le bouton **[!UICONTROL Jeu de données de profil]** pour activer votre jeu de données cible pour [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/databases/new-dataset.png)

La boîte de dialogue **[!UICONTROL Sélectionner le schéma]** s’affiche. Sélectionnez le schéma que vous souhaitez appliquer au nouveau jeu de données, puis cliquez sur **[!UICONTROL Terminé]**.

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs calculées ou calculées. Pour plus d’informations sur les fonctions du mappeur et les champs calculés, consultez le [guide des fonctions de préparation de données](../../../../data-prep/functions.md) ou le [guide des champs calculés](../../../../data-prep/calculated-fields.md).

>[!TIP]
>
>[!DNL Platform] fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Sélectionnez **[!UICONTROL Aperçu des données]** pour afficher les résultats de mappage de 100 lignes maximum de données d’exemple du jeu de données sélectionné.

Lors de la prévisualisation, la colonne d’identité est considérée comme le premier champ, car il s’agit des informations clés nécessaires à la validation des résultats du mapping.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

Une fois les données source mises en correspondance, sélectionnez **[!UICONTROL Fermer]**.

## Planification des exécutions d’ingestion

L’étape **[!UICONTROL Planification]** s’affiche, ce qui vous permet de configurer un planning d’ingestion pour ingérer automatiquement les données source sélectionnées à l’aide des mappages configurés. Le tableau suivant décrit les différents champs configurables pour la planification :

| Champ | Description |
| --- | --- |
| Fréquence | Les fréquences sélectionnées sont `Once`, `Minute`, `Hour`, `Day` et `Week`. |
| Intervalle | Entier qui définit l’intervalle pour la fréquence sélectionnée. |
| Heure de début | Horodatage UTC indiquant quand la toute première ingestion est configurée pour se produire. |
| Renvoi | Valeur boolean qui détermine les données ingérées initialement. Si **[!UICONTROL Renvoi]** est activé, tous les fichiers actuels du chemin spécifié seront ingérés lors de la première ingestion planifiée. Si **[!UICONTROL Renvoi]** est désactivé, seuls les fichiers chargés entre la première exécution de l’ingestion et l’heure de début seront ingérés. Les fichiers chargés avant l’heure de début ne seront pas ingérés. |
| Colonne delta | Une option avec un ensemble filtré de champs de schéma source de type, date ou heure. Ce champ sert à différencier les données nouvelles des données existantes. Les données incrémentielles seront ingérées en fonction de l’horodatage de la colonne sélectionnée. |

Les flux de données sont conçus pour ingérer automatiquement des données selon un calendrier précis. Sélectionnez tout d’abord la fréquence d’ingestion. Définissez ensuite l’intervalle pour désigner la période entre deux exécutions de flux. La valeur de l’intervalle doit être un entier non nul et doit être définie sur supérieur ou égal à 15.

Pour définir l’heure de début de l’ingestion, ajustez la date et l’heure affichées dans la zone d’heure de début. Vous pouvez également sélectionner l’icône de calendrier pour modifier la valeur de l’heure de début. L’heure de début doit être supérieure ou égale à l’heure UTC actuelle.

Sélectionnez **[!UICONTROL Charger les données incrémentielles par]** pour affecter la colonne delta. Ce champ établit une distinction entre les données nouvelles et existantes.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Configuration d’un flux de données d’ingestion unique

Pour configurer l’ingestion unique, sélectionnez la flèche de liste déroulante Fréquence et sélectionnez **[!UICONTROL Une fois]**.

>[!TIP]
>
>**** Intervalle et  **** renvoi ne sont pas visibles lors d’une ingestion unique.

Une fois que vous avez fourni les valeurs appropriées au planning, sélectionnez **[!UICONTROL Suivant]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Fournir des détails sur les flux de données

L’étape **[!UICONTROL Détails du flux de données]** s’affiche, ce qui vous permet de nommer et de décrire brièvement votre nouveau flux de données.

Au cours de ce processus, vous pouvez également activer **[!UICONTROL l’ingestion partielle]** et **[!UICONTROL les diagnostics d’erreur]**. L’activation de **[!UICONTROL l’ingestion partielle]** permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Une fois l’**[!UICONTROL ingestion partielle]** activée, faites glisser la touche **[!UICONTROL Seuil d’erreur %]** pour ajuster le seuil d’erreur du lot. Vous pouvez également régler manuellement le seuil en sélectionnant la zone de saisie. Pour plus d’informations, consultez la [présentation de l’ingestion par lots partielle](../../../../ingestion/batch-ingestion/partial.md).
Indiquez les valeurs du flux de données et sélectionnez **[!UICONTROL Suivant]**.

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## Vérification du flux de données

L’étape **[!UICONTROL Réviser]** s’affiche, ce qui vous permet de passer en revue votre nouveau flux de données avant qu’il ne soit créé. Les détails sont regroupés dans les catégories suivantes :

- **[!UICONTROL Connexion]** : Affiche le type de source, le chemin d’accès approprié du fichier source choisi et la quantité de colonnes qu’il contient.
- **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.
- **[!UICONTROL Planification]** : Affiche la période, la fréquence et l’intervalle principaux du planning d’ingestion.

Une fois que vous avez examiné votre flux de données, cliquez sur **[!UICONTROL Terminer]** et laissez un certain temps pour que le flux de données soit créé.

![](../../../images/tutorials/dataflow/databases/review.png)

## Surveillance de votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les taux d’ingestion, les succès et les erreurs. Pour plus d’informations sur la surveillance du flux de données, consultez le tutoriel sur la [surveillance des comptes et des flux de données dans l’interface utilisateur](../monitor.md).

## Suppression de votre flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]** disponible dans l’espace de travail **[!UICONTROL Flux de données]**. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur la [suppression des flux de données dans l’interface utilisateur](../delete.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour importer des données d’une base de données externe et vous avez obtenu des informations sur la surveillance des jeux de données. Les données entrantes peuvent désormais être utilisées par les services [!DNL Platform] en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, consultez les documents suivants :

- [Présentation d’[!DNL Real-time Customer Profile]](../../../../profile/home.md)
- [Présentation d’[!DNL Data Science Workspace]](../../../../data-science-workspace/home.md)

## Annexe

Les sections suivantes apportent des informations supplémentaires sur l’utilisation des connecteurs source.

### Désactivation d’un flux de données

Lorsqu’un flux de données est créé, il devient immédiatement principal et ingère des données selon le planning qu’il a été donné. Vous pouvez désactiver un principal flux de données à tout moment en suivant les instructions ci-dessous.

Dans l’espace de travail **[!UICONTROL Sources]**, sélectionnez l’onglet **[!UICONTROL Flux de données]**. Sélectionnez ensuite le flux de données que vous souhaitez désactiver.

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

La colonne **[!UICONTROL Propriétés]** s’affiche sur le côté droit de l’écran, y compris un bouton d’activation/désactivation **[!UICONTROL activé]**. Sélectionnez le bouton d’activation/désactivation pour désactiver le flux de données. Le même bouton peut être utilisé pour réactiver un flux de données une fois qu’il a été désactivé.

![](../../../images/tutorials/dataflow/databases/disable.png)

### Activation des données entrantes pour la population [!DNL Profile]

Les données entrantes provenant de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos [!DNL Real-time Customer Profile] données. Pour plus d’informations sur le remplissage de vos données [!DNL Real-time Customer Profile], consultez le tutoriel sur [Population de profils](../profile.md).
