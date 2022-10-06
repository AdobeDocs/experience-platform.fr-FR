---
keywords: Experience Platform;accueil;rubriques les plus consultées;flux de données;flux de données
title: Configuration d’un flux de données pour ingérer des données par lots à partir d’une source de stockage dans le cloud dans l’interface utilisateur
description: Ce tutoriel explique comment configurer un nouveau flux de données pour ingérer des données par lots à partir d’une source de stockage dans le cloud dans l’interface utilisateur.
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 0910de76d817eea7c7c3cb2b988d81268b3e5812
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 28%

---

# Configuration d’un flux de données pour ingérer des données par lots à partir d’une source de stockage dans le cloud dans l’interface utilisateur

Ce tutoriel décrit les étapes de configuration d’un flux de données pour importer des données par lots de votre source de stockage dans le cloud vers Adobe Experience Platform.

## Prise en main

>[!NOTE]
>
>Pour créer un flux de données permettant d’importer des données par lots à partir d’un espace de stockage dans le cloud, vous devez déjà avoir accès à une source de stockage dans le cloud authentifiée. Si vous n’avez pas accès à , accédez au [présentation des sources](../../../../home.md#cloud-storage) pour obtenir la liste des sources de stockage dans le cloud avec lesquelles vous pouvez créer un compte.

Ce tutoriel nécessite une compréhension pratique des composants suivants de l’Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

### Formats de fichiers pris en charge

Les sources de stockage dans le cloud pour les données par lots prennent en charge les formats de fichiers suivants pour l’ingestion :

* Valeurs séparées par des délimiteurs (DSV) : N’importe quelle valeur de caractère unique peut être utilisée comme délimiteur pour les fichiers de données au format DSV.
* [!DNL JavaScript Object Notation] (JSON) : Les fichiers de données au format JSON doivent être compatibles avec XDM.
* [!DNL Apache Parquet]: Les fichiers de données au format parquet doivent être compatibles avec XDM.
* Fichiers compressés : Les fichiers JSON et délimités peuvent être compressés comme suit : `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`, et `tar`.

## Ajout de données

Après avoir créé votre compte de stockage dans le cloud, la variable **[!UICONTROL Ajouter des données]** s’affiche, fournissant une interface vous permettant d’explorer la hiérarchie des fichiers de stockage dans le cloud et de sélectionner le dossier ou le fichier spécifique à importer dans Platform.

* La partie gauche de l’interface est un navigateur de répertoires qui affiche la hiérarchie des fichiers de stockage dans le cloud.
* La partie droite de l&#39;interface permet de prévisualiser jusqu&#39;à 100 lignes de données à partir d&#39;un dossier ou d&#39;un fichier compatible.

![](../../../../images/tutorials/dataflow/cloud-batch/select-data.png)

Sélectionnez le dossier racine pour accéder à la hiérarchie des dossiers. À partir de là, vous pouvez sélectionner un seul dossier pour ingérer tous les fichiers du dossier de manière récursive. Lors de l’ingestion d’un dossier entier, vous devez vous assurer que tous les fichiers de ce dossier partagent le même format de données et le même schéma.

![](../../../../images/tutorials/dataflow/cloud-batch/folder-directory.png)

Une fois que vous avez sélectionné un dossier, l’interface appropriée se met à jour pour obtenir un aperçu du contenu et de la structure du premier fichier du dossier sélectionné.

![](../../../../images/tutorials/dataflow/cloud-batch/select-folder.png)

Au cours de cette étape, vous pouvez effectuer plusieurs configurations sur vos données avant de continuer. Tout d’abord, sélectionnez **[!UICONTROL Format des données]** puis sélectionnez le format de données approprié pour votre fichier dans le panneau déroulant qui s’affiche.

Le tableau suivant affiche les formats de données appropriés pour les types de fichiers pris en charge :

| Type de fichier | Format des données |
| --- | --- |
| CSV | [!UICONTROL Délimité] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL Parquet XDM] |

![](../../../../images/tutorials/dataflow/cloud-batch/data-format.png)

### Sélectionner un délimiteur de colonne

Après avoir configuré le format des données, vous pouvez définir un délimiteur de colonne lors de l’ingestion de fichiers délimités. Sélectionnez la **[!UICONTROL Délimiteur]** puis sélectionnez un délimiteur dans le menu déroulant. Le menu affiche les options de délimiteurs les plus fréquemment utilisées, y compris une virgule (`,`), un onglet (`\t`) et une barre verticale (`|`).

![](../../../../images/tutorials/dataflow/cloud-batch/delimiter.png)

Si vous préférez utiliser un délimiteur personnalisé, sélectionnez **[!UICONTROL Personnalisé]** et saisissez un délimiteur à un caractère unique de votre choix dans la barre de saisie contextuelle.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

### Ingestion de fichiers compressés

Vous pouvez également ingérer des fichiers JSON compressés ou délimités en spécifiant leur type de compression.

Dans le [!UICONTROL Sélectionner des données] sélectionnez un fichier compressé à des fins d’ingestion, puis sélectionnez son type de fichier approprié et indiquez s’il est compatible XDM ou non. Ensuite, sélectionnez **[!UICONTROL Type de compression]** puis sélectionnez le type de fichier compressé approprié pour vos données source.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

Pour importer un fichier spécifique dans Platform, sélectionnez un dossier, puis le fichier à ingérer. Au cours de cette étape, vous pouvez également prévisualiser le contenu d’autres fichiers d’un dossier donné à l’aide de l’icône d’aperçu située en regard d’un nom de fichier.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-batch/select-file.png)

## Fournir des détails sur le flux de données

La page [!UICONTROL Détails du flux de données] vous permet de choisir si vous souhaitez utiliser un jeu de données existant ou un nouveau jeu de données. Au cours de ce processus, vous pouvez également configurer vos données à ingérer dans Profile et activer des paramètres tels que [!UICONTROL Diagnostics d’erreur], [!UICONTROL Ingestion partielle], et [!UICONTROL Alertes].

![](../../../../images/tutorials/dataflow/cloud-batch/dataflow-detail.png)

### Utiliser un jeu de données existant

Pour ingérer vos données dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Vous pouvez soit récupérer un jeu de données existant à l’aide de l’option de [!UICONTROL Recherche avancée], soit faire défiler la liste des jeux de données existants dans le menu déroulant. Une fois que vous avez sélectionné un jeu de données, indiquez un nom et une description pour votre flux de données.

![](../../../../images/tutorials/dataflow/cloud-batch/existing.png)

### Utiliser un nouveau jeu de données

Pour procéder à lʼingestion dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**, puis saisissez un nom pour le jeu de données de sortie et une description facultative. Sélectionnez ensuite un schéma à mapper à l’aide de l’option [!UICONTROL Recherche avancée] ou en faisant défiler la liste des schémas existants dans le menu déroulant. Une fois que vous avez sélectionné un schéma, saisissez un nom et une description pour votre flux de données.

![](../../../../images/tutorials/dataflow/cloud-batch/new.png)

### Activation des diagnostics de profil et d’erreur

Sélectionnez ensuite le **[!UICONTROL Jeu de données de profil]** Activez votre jeu de données pour Profile. Cela vous permet de créer une vue holistique des attributs et des comportements d’une entité. Les données de tous les jeux de données activés pour Profile seront incluses dans Profile et les modifications sont appliquées lorsque vous enregistrez votre flux de données.

Le [!UICONTROL diagnostic d’erreur] permet de générer un message d’erreur détaillé pour tout enregistrement erroné survenant dans votre flux de données, tandis que l’[!UICONTROL ingestion partielle] vous permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil que vous définissez manuellement. Pour plus d’informations, consultez la [présentation de l’ingestion par lots partiels](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/dataflow/cloud-batch/ingestion-configs.png)

### Activer les alertes

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des sources dans l’interface utilisateur](../../alerts.md).

Lorsque vous avez terminé de renseigner votre flux de données, sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-batch/alerts.png)

## Mappage des champs de données à un schéma XDM

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, reportez-vous à la section [Guide de l’interface utilisateur de la préparation de données](../../../../../data-prep/ui/mapping.md).

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-batch/mapping.png)

## Planification des exécutions d’ingestion

>[!IMPORTANT]
>
>Il est vivement recommandé de planifier votre flux de données pour une ingestion unique lors de l’utilisation de la variable [Source FTP](../../../../connectors/cloud-storage/ftp.md).

Le [!UICONTROL Planification] s’affiche, ce qui vous permet de configurer un planning d’ingestion pour ingérer automatiquement les données source sélectionnées à l’aide des mappages configurés. Par défaut, la planification est définie sur `Once`. Pour régler la fréquence d’ingestion, sélectionnez **[!UICONTROL Fréquence]** puis sélectionnez une option dans le menu déroulant.

>[!TIP]
>
>L’intervalle et le renvoi ne sont pas visibles lors d’une ingestion unique.

![scheduling](../../../../images/tutorials/dataflow/cloud-batch/scheduling.png)

Si vous définissez votre fréquence d’ingestion sur `Minute`, `Hour`, `Day`ou `Week`, vous devez ensuite définir un intervalle pour établir une période définie entre chaque ingestion. Par exemple, une fréquence d’ingestion définie sur `Day` et un intervalle défini sur `15` signifie que votre flux de données est planifié pour ingérer des données tous les 15 jours.

Au cours de cette étape, vous pouvez également activer **renvoyer** et définissez une colonne pour l’ingestion incrémentielle des données. Le renvoi est utilisé pour ingérer des données historiques, tandis que la colonne que vous définissez pour l’ingestion incrémentielle permet de différencier les nouvelles données des données existantes.

Consultez le tableau ci-dessous pour plus d’informations sur les configurations de planification.

| Champ | Description |
| --- | --- |
| Fréquence | Fréquence d’ingestion. Les fréquences sélectionnées incluent `Once`, `Minute`, `Hour`, `Day`, et `Week`. |
| Intervalle | Entier qui définit l’intervalle pour la fréquence sélectionnée. La valeur de l’intervalle doit être un entier non nul et doit être définie sur supérieur ou égal à 15. |
| Heure de début | Horodatage UTC indiquant quand la toute première ingestion est configurée pour se produire. L’heure de début doit être supérieure ou égale à l’heure UTC actuelle. |
| Renvoi | Valeur boolean qui détermine les données ingérées initialement. Si le renvoi est activé, tous les fichiers actuels du chemin spécifié seront ingérés lors de la première ingestion planifiée. Si le renvoi est désactivé, seuls les fichiers chargés entre la première exécution de l’ingestion et l’heure de début seront ingérés. Les fichiers chargés avant l’heure de début ne seront pas ingérés. |

>[!NOTE]
>
>Pour l’ingestion par lots, chaque flux de données qui s’ensuit sélectionne les fichiers à ingérer à partir de votre source en fonction de la date et heure de leur **dernière modification**. Cela signifie que les flux de données par lot sélectionnent les fichiers de la source qui sont nouveaux ou qui ont été modifiés depuis la dernière exécution du flux. En outre, vous devez vous assurer qu’il existe une période suffisante entre le chargement de fichiers et l’exécution d’un flux planifié, car les fichiers qui ne sont pas entièrement chargés sur votre compte de stockage dans le cloud avant l’heure d’exécution planifiée du flux peuvent ne pas être sélectionnés pour ingestion.

Lorsque vous avez terminé de configurer votre planning d’ingestion, sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-batch/scheduling-configs.png)

## Vérifier le flux de données

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]**: Affiche le type de source, le chemin d’accès approprié du fichier source choisi et la quantité de colonnes qu’il contient.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.
* **[!UICONTROL Planification]**: Affiche la période, la fréquence et l’intervalle principaux du planning d’ingestion.

Une fois que vous avez examiné votre flux de données, cliquez sur **[!UICONTROL Terminer]** et accorder un certain temps pour la création du flux de données.

![](../../../../images/tutorials/dataflow/cloud-batch/review.png)


## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour importer des données d’un espace de stockage cloud externe et vous avez obtenu des informations sur la surveillance des jeux de données. Pour en savoir plus sur la création de flux de données, vous pouvez compléter votre apprentissage en regardant la vidéo ci-dessous. En outre, les données entrantes peuvent désormais être utilisées par les utilisateurs en aval. [!DNL Platform] des services tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Consultez les documents suivants pour plus d’informations :

* [Présentation de [!DNL Real-time Customer Profile]](../../../../../profile/home.md)
* [Présentation de [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> Lʼinterface utilisateur de [!DNL Platform] affichée dans la vidéo suivante est obsolète. Consultez la documentation pour découvrir les dernières captures dʼécran et fonctionnalités de lʼinterface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Annexe

Les sections suivantes apportent des informations supplémentaires sur l’utilisation des connecteurs source.

## Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les taux d’ingestion, les succès et les erreurs. Pour plus d’informations sur la surveillance du flux de données, consultez le tutoriel sur [surveillance des comptes et des flux de données dans l’interface utilisateur](../../monitor.md).

## Mettre à jour votre flux de données

Pour mettre à jour les configurations de la planification, du mappage et des informations générales de vos flux de données, consultez le tutoriel sur [mise à jour des flux de données de sources dans l’interface utilisateur](../../update-dataflows.md)

## Supprimer le flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]**, disponible dans l’espace de travail **[!UICONTROL Flux de données]**. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur [suppression de flux de données dans l’interface utilisateur](../../delete.md).