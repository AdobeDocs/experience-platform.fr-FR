---
keywords: Experience Platform;accueil;rubriques les plus consultées;flux de données;flux de données
solution: Experience Platform
title: Configuration d’un flux de données pour un connecteur par lots de stockage dans le cloud dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Platform. Ce tutoriel décrit les étapes de configuration d’un nouveau flux de données à l’aide de votre compte de stockage dans le cloud.
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 5478143e681257c6885d99d83380a35de263ed3d
workflow-type: tm+mt
source-wordcount: '1999'
ht-degree: 4%

---

# Configuration d’un flux de données pour une connexion par lots de stockage dans le cloud dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données [!DNL Platform]. Ce tutoriel décrit les étapes de configuration d’un nouveau flux de données à l’aide de votre compte de stockage dans le cloud.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

En outre, ce tutoriel nécessite que vous disposiez d’un compte de stockage dans le cloud établi. Vous trouverez la liste des tutoriels relatifs à la création de différents comptes de stockage dans le cloud dans l’interface utilisateur dans la [présentation des connecteurs source](../../../../home.md).

### Formats de fichiers pris en charge

[!DNL Experience Platform] prend en charge les formats de fichiers suivants à ingérer à partir de stockages externes :

* Valeurs séparées par des délimiteurs (DSV) : N’importe quelle valeur de caractère unique peut être utilisée comme délimiteur pour les fichiers de données au format DSV.
* [!DNL JavaScript Object Notation] (JSON) : Les fichiers de données au format JSON doivent être compatibles avec XDM.
* [!DNL Apache Parquet]: Les fichiers de données au format parquet doivent être compatibles avec XDM.
* Fichiers compressés : Les fichiers JSON et délimités peuvent être compressés comme suit : `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip` et `tar`.

## Sélectionner des données

Une fois votre compte de stockage dans le cloud créé, l’étape **[!UICONTROL Sélectionner les données]** s’affiche, vous permettant ainsi d’explorer la hiérarchie des fichiers de stockage dans le cloud.

* La partie gauche de l’interface est un explorateur de répertoires qui affiche vos fichiers et répertoires de stockage dans le cloud.
* La partie droite de l&#39;interface permet de prévisualiser jusqu&#39;à 100 lignes de données à partir d&#39;un fichier compatible.

![interface](../../../../images/tutorials/dataflow/cloud-storage/batch/interface.png)

La sélection d’un dossier répertorié vous permet de parcourir la hiérarchie de dossiers dans des dossiers plus profonds. Vous pouvez sélectionner un seul dossier pour ingérer tous les fichiers du dossier de manière récursive. Lors de l’ingestion d’un dossier entier, vous devez vous assurer que tous les fichiers du dossier partagent le même schéma.

Une fois qu’un fichier ou un dossier compatible est sélectionné, sélectionnez le format de données correspondant dans le menu déroulant [!UICONTROL Sélectionner le format de données].

Le tableau suivant affiche le format de données approprié pour les types de fichiers pris en charge :

| Type de fichier | Sur le format des données saisies |
| --- | --- |
| CSV | [!UICONTROL Délimité] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL Parquet XDM] |

Sélectionnez **[!UICONTROL JSON]** et attendez quelques secondes que l’interface d’aperçu soit remplie.

![select-data](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

>[!NOTE]
>
>Contrairement aux types de fichiers JSON et délimités, les fichiers au format Parquet ne sont pas disponibles pour l’aperçu.

L’interface d’aperçu vous permet d’examiner le contenu et la structure d’un fichier. Par défaut, l’interface d’aperçu affiche le premier fichier du dossier que vous avez sélectionné.

Pour prévisualiser un autre fichier, cliquez sur l’icône d’aperçu située en regard du nom du fichier à inspecter.

![default-preview](../../../../images/tutorials/dataflow/cloud-storage/batch/default-preview.png)

Une fois que vous avez examiné le contenu et la structure des fichiers de votre dossier, sélectionnez **[!UICONTROL Suivant]** pour ingérer tous les fichiers du dossier de manière récursive.

![select-folder](../../../../images/tutorials/dataflow/cloud-storage/batch/select-folder.png)

Si vous préférez sélectionner un fichier spécifique, sélectionnez le fichier à ingérer, puis choisissez **[!UICONTROL Suivant]**.

![select-file](../../../../images/tutorials/dataflow/cloud-storage/batch/select-file.png)

### Définition d’un délimiteur personnalisé pour les fichiers délimités

Vous pouvez définir un délimiteur personnalisé lors de l’ingestion de fichiers délimités. Sélectionnez l’option **[!UICONTROL Délimiteur]** , puis sélectionnez un délimiteur dans le menu déroulant. Le menu affiche les options de délimiteurs les plus fréquemment utilisées, notamment une virgule (`,`), un onglet (`\t`) et une barre verticale (`|`). Si vous préférez utiliser un délimiteur personnalisé, sélectionnez **[!UICONTROL Personnalisé]** et saisissez un délimiteur à un seul caractère de votre choix dans la barre de saisie contextuelle.

Une fois que vous avez sélectionné le format de données et défini votre délimiteur, sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

### Ingestion de fichiers compressés

Vous pouvez ingérer des fichiers JSON compressés ou délimités en spécifiant leur type de compression.

À l’étape [!UICONTROL Sélectionner les données] , sélectionnez un fichier compressé à des fins d’ingestion, puis sélectionnez son type de fichier approprié et indiquez s’il est compatible XDM ou non. Ensuite, sélectionnez **[!UICONTROL Type de compression]**, puis le type de fichier compressé approprié pour vos données source.

Une fois un type de fichier compressé identifié, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/compressed-files.png)

## Mappage des champs de données à un schéma XDM

L’étape **[!UICONTROL Mappage]** s’affiche, fournissant une interface interactive pour mapper les données source à un jeu de données [!DNL Platform]. Les fichiers source formatés dans Parquet doivent être conformes à XDM et ne nécessitent pas de configurer manuellement le mappage, tandis que les fichiers CSV nécessitent de configurer explicitement le mappage, mais vous permettent de choisir les champs de données source à mapper. Les fichiers JSON, s’ils sont marqués comme une plainte XDM, ne nécessitent pas de configuration manuelle. Cependant, s’il n’est pas marqué comme compatible avec XDM, il vous faudra configurer explicitement le mappage.

Sélectionnez un jeu de données dans lequel ingérer les données entrantes. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

**Utilisation d’un jeu de données existant**

Pour ingérer des données dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**, puis sélectionnez l’icône du jeu de données.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

La boîte de dialogue **[!UICONTROL Sélectionner un jeu de données]** s’affiche. Recherchez le jeu de données que vous souhaitez utiliser, sélectionnez-le, puis cliquez sur **[!UICONTROL Continuer]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Utilisation d’un nouveau jeu de données**

Pour ingérer des données dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis. Pour ajouter un schéma, vous pouvez saisir un nom de schéma existant dans la boîte de dialogue **[!UICONTROL Sélectionner le schéma]**. Vous pouvez également sélectionner la **[!UICONTROL recherche avancée de schéma]** pour rechercher un schéma approprié.

Au cours de cette étape, vous pouvez activer votre jeu de données pour [!DNL Real-time Customer Profile] et créer une vue holistique des attributs et des comportements d’une entité. Les données de tous les jeux de données activés seront incluses dans [!DNL Profile] et des modifications sont appliquées lorsque vous enregistrez votre flux de données.

Active/désactive le bouton **[!UICONTROL Jeu de données de profil]** pour activer votre jeu de données cible pour [!DNL Profile].

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

La boîte de dialogue **[!UICONTROL Sélectionner le schéma]** s’affiche. Sélectionnez le schéma que vous souhaitez appliquer au nouveau jeu de données, puis sélectionnez **[!UICONTROL Terminé]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Selon vos besoins, vous pouvez choisir de mapper directement les champs ou utiliser les fonctions de mappeur pour transformer les données sources afin d’obtenir des valeurs calculées ou calculées. Pour plus d’informations sur le mappage des données et les fonctions du mappeur, reportez-vous au tutoriel sur le [mappage des données CSV aux champs de schéma XDM](../../../../../ingestion/tutorials/map-a-csv-file.md).

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

Pour les fichiers JSON, en plus de mapper directement les champs à d’autres champs, vous pouvez directement mapper des objets à d’autres objets et tableaux à d’autres tableaux. Vous pouvez également prévisualiser et mapper des types de données complexes tels que des tableaux dans des fichiers JSON à l’aide d’un connecteur source de stockage dans le cloud.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

Notez que vous ne pouvez pas effectuer de mappage sur différents types. Par exemple, vous ne pouvez pas mapper un objet à un tableau ou un champ à un objet.

>[!TIP]
>
>[!DNL Platform] fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation.

Sélectionnez **[!UICONTROL Aperçu des données]** pour afficher les résultats de mappage de 100 lignes maximum de données d’exemple du jeu de données sélectionné.

Lors de la prévisualisation, la colonne d’identité est considérée comme le premier champ, car il s’agit des informations clés nécessaires à la validation des résultats du mapping.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

Une fois les données source mises en correspondance, sélectionnez **[!UICONTROL Fermer]**.

## Planification des exécutions d’ingestion

L’étape **[!UICONTROL Planification]** s’affiche, ce qui vous permet de configurer un planning d’ingestion pour ingérer automatiquement les données source sélectionnées à l’aide des mappages configurés. Le tableau suivant décrit les différents champs configurables pour la planification :

| Champ | Description |
| --- | --- |
| Fréquence | Les fréquences sélectionnées sont `Once`, `Minute`, `Hour`, `Day` et `Week`. |
| Intervalle | Entier qui définit l’intervalle pour la fréquence sélectionnée. |
| Heure de début | Horodatage UTC indiquant quand la toute première ingestion est configurée pour se produire. |
| Renvoi | Valeur boolean qui détermine les données ingérées initialement. Si **[!UICONTROL Renvoi]** est activé, tous les fichiers actuels du chemin spécifié seront ingérés lors de la première ingestion planifiée. Si **[!UICONTROL Renvoi]** est désactivé, seuls les fichiers chargés entre la première exécution de l’ingestion et l’heure de début seront ingérés. Les fichiers chargés avant l’heure de début ne seront pas ingérés. |

Les flux de données sont conçus pour ingérer automatiquement des données selon un calendrier précis. Sélectionnez tout d’abord la fréquence d’ingestion. Définissez ensuite l’intervalle pour désigner la période entre deux exécutions de flux. La valeur de l’intervalle doit être un entier non nul et doit être définie sur supérieur ou égal à 15.

Pour définir l’heure de début de l’ingestion, ajustez la date et l’heure affichées dans la zone d’heure de début. Vous pouvez également sélectionner l’icône de calendrier pour modifier la valeur de l’heure de début. L’heure de début doit être supérieure ou égale à l’heure actuelle en UTC.

Indiquez les valeurs du planning et sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Configuration d’un flux de données d’ingestion unique

Pour configurer l’ingestion unique, sélectionnez la flèche de liste déroulante Fréquence et sélectionnez **[!UICONTROL Une fois]**. Vous pouvez continuer à apporter des modifications à un jeu de flux de données pour une ingestion de fréquence unique, tant que l’heure de début reste dans le futur. Une fois l’heure de début écoulée, la valeur de la fréquence ponctuelle ne peut plus être modifiée. **** Intervalle et  **** le renvoi ne sont pas visibles lors de la configuration d’un flux de données d’ingestion unique.

>[!IMPORTANT]
>
>Il est vivement recommandé de planifier votre flux de données pour une ingestion unique lors de l’utilisation du [connecteur FTP](../../../../connectors/cloud-storage/ftp.md).

Une fois que vous avez fourni les valeurs appropriées au planning, sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Fournir des détails sur les flux de données

L’étape **[!UICONTROL Détails du flux de données]** s’affiche, ce qui vous permet de nommer et de décrire brièvement votre nouveau flux de données.

Au cours de ce processus, vous pouvez également activer **[!UICONTROL l’ingestion partielle]** et **[!UICONTROL les diagnostics d’erreur]**. L’activation de **[!UICONTROL l’ingestion partielle]** permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil que vous pouvez définir. L’activation de **[!UICONTROL diagnostics d’erreur]** fournit des détails sur toutes les données incorrectes traitées séparément par lots. Pour plus d’informations, consultez la [présentation de l’ingestion par lots partielle](../../../../../ingestion/batch-ingestion/partial.md).

Indiquez les valeurs du flux de données et sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Vérification du flux de données

L’étape **[!UICONTROL Réviser]** s’affiche, ce qui vous permet de passer en revue votre nouveau flux de données avant qu’il ne soit créé. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : Affiche le type de source, le chemin d’accès approprié du fichier source choisi et la quantité de colonnes qu’il contient.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.
* **[!UICONTROL Planification]** : Affiche la période, la fréquence et l’intervalle principaux du planning d’ingestion.

Une fois que vous avez examiné votre flux de données, cliquez sur **[!UICONTROL Terminer]** et laissez un certain temps pour que le flux de données soit créé.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Surveillance de votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les taux d’ingestion, les succès et les erreurs. Pour plus d’informations sur la surveillance du flux de données, consultez le tutoriel sur la [surveillance des comptes et des flux de données dans l’interface utilisateur](../../monitor.md).

## Suppression de votre flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]** disponible dans l’espace de travail **[!UICONTROL Flux de données]**. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur la [suppression des flux de données dans l’interface utilisateur](../../delete.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour importer des données d’un espace de stockage cloud externe et vous avez obtenu des informations sur la surveillance des jeux de données. Pour en savoir plus sur la création de flux de données, vous pouvez compléter votre apprentissage en regardant la vidéo ci-dessous. En outre, les données entrantes peuvent désormais être utilisées par les services [!DNL Platform] en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, consultez les documents suivants :

* [Présentation d’[!DNL Real-time Customer Profile]](../../../../../profile/home.md)
* [Présentation d’[!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> Lʼinterface utilisateur de [!DNL Platform] affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation ci-dessus pour connaître les dernières captures d’écran et fonctionnalités de l’interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Annexe

Les sections suivantes apportent des informations supplémentaires sur l’utilisation des connecteurs source.

### Désactivation d’un flux de données

Lorsqu’un flux de données est créé, il devient immédiatement principal et ingère des données selon le planning qu’il a été donné. Vous pouvez désactiver un principal flux de données à tout moment en suivant les instructions ci-dessous.

Dans l’espace de travail **[!UICONTROL Sources]**, cliquez sur l’onglet **[!UICONTROL Parcourir]** . Cliquez ensuite sur le nom du compte associé au principal flux de données que vous souhaitez désactiver.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

La page **[!UICONTROL Activité source]** s’affiche. Sélectionnez le principal flux de données dans la liste pour ouvrir sa colonne **[!UICONTROL Propriétés]** sur le côté droit de l’écran, qui contient un bouton d’activation **[!UICONTROL activé]**. Cliquez sur le bouton bascule pour désactiver le flux de données. Le même bouton peut être utilisé pour réactiver un flux de données une fois qu’il a été désactivé.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Activation des données entrantes pour la population [!DNL Profile]

Les données entrantes provenant de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos [!DNL Real-time Customer Profile] données. Pour plus d’informations sur le remplissage de vos données [!DNL Real-time Customer Profile], consultez le tutoriel sur [Population de profils](../../profile.md).
