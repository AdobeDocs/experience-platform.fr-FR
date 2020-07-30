---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configuration d’un flux de données pour un connecteur de lot d’enregistrement cloud dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f532bd6393bfad84fa09c2fc753d1d5c5b39d013
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 6%

---


# Configuration d’un flux de données pour un connecteur de lot d’enregistrement cloud dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source dans un [!DNL Platform] jeu de données. Ce didacticiel décrit la procédure à suivre pour configurer un nouveau flux de données à l’aide de votre compte d’enregistrement cloud.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

De plus, ce didacticiel nécessite que vous disposiez d’un compte d’enregistrement cloud établi. Vous trouverez une liste de didacticiels pour la création de différents comptes d’enregistrement cloud dans l’interface utilisateur dans l’aperçu [des connecteurs](../../../../home.md)source.

### Formats de fichiers pris en charge

[!DNL Experience Platform] prend en charge les formats de fichier suivants à ingérer à partir d’enregistrements externes :

* Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules. La valeur des en-têtes de champ des fichiers au format DSV ne doit être composée que de caractères alphanumériques et de traits de soulignement. La prise en charge des fichiers DSV généraux sera assurée à l’avenir.
* [!DNL JavaScript Object Notation] (JSON) : Les fichiers de données au format JSON doivent être compatibles XDM.
* [!DNL Apache Parquet]: Les fichiers de données au format Parquet doivent être compatibles XDM.

## Sélectionner des données

Après avoir créé votre compte d’enregistrement de cloud, l’étape *[!UICONTROL Sélectionner les données]* s’affiche, ce qui vous permet d’explorer la hiérarchie de votre enregistrement de cloud.

* La moitié gauche de l&#39;interface est un navigateur d&#39;annuaire qui affiche les fichiers et répertoires de votre serveur.
* La moitié droite de l&#39;interface vous permet de prévisualisation jusqu&#39;à 100 lignes de données à partir d&#39;un fichier compatible.

La sélection d’un dossier répertorié vous permet de parcourir la hiérarchie de dossiers en dossiers plus profonds. Une fois que vous avez sélectionné un fichier ou un dossier compatible, la liste déroulante **[!UICONTROL Sélectionner le format]** de données s&#39;affiche, dans laquelle vous pouvez choisir un format pour afficher les données dans la fenêtre de prévisualisation.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

Une fois la fenêtre de prévisualisation renseignée, vous pouvez sélectionner **[!UICONTROL Suivant]** pour télécharger tous les fichiers du dossier sélectionné. Si vous souhaitez télécharger un fichier spécifique, sélectionnez-le dans la liste avant de sélectionner **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-preview.png)

### Invitation de fichiers Parquet ou JSON

Les formats de fichier pris en charge pour un compte d’enregistrement cloud incluent également JSON et Parquet. Les fichiers JSON et Parquet doivent être compatibles XDM. Pour importer des fichiers JSON ou Parquet, sélectionnez le format de fichier approprié dans le navigateur d’annuaire et appliquez un format de données compatible à partir de l’interface de droite. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

>[!IMPORTANT]
>
>Contrairement aux types de fichiers délimités, les fichiers au format JSON et Parquet ne sont pas disponibles pour la prévisualisation.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-parquet.png)

## Mappage des champs de données à un schéma XDM

L’étape *[!UICONTROL Mappage]* s’affiche, fournissant une interface interactive permettant de mapper les données source à un [!DNL Platform] jeu de données. Les fichiers source mis en forme dans JSON ou Parquet doivent être compatibles XDM et ne nécessitent pas de configuration manuelle du mappage. Inversement, les fichiers CSV nécessitent de configurer explicitement le mappage, mais vous permettent de sélectionner les champs de données source à mapper.

Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez soit utiliser un jeu de données existant, soit en créer un nouveau.

**Utilisation d’un jeu de données existant**

Pour importer des données dans un jeu de données existant, sélectionnez Jeu de données **** existant, puis sélectionnez l’icône Jeu de données.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

The *[!UICONTROL Select dataset]* dialog appears. Recherchez le jeu de données que vous souhaitez utiliser, sélectionnez-le, puis cliquez sur **[!UICONTROL Continuer]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Utiliser un nouveau jeu de données**

Pour importer des données dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** et entrez un nom et une description pour le jeu de données dans les champs fournis. Pour ajouter un schéma, vous pouvez entrer un nom de schéma existant dans la boîte de dialogue *[!UICONTROL Sélectionner un schéma]* . Vous pouvez également sélectionner le **[!UICONTROL Schéma de recherche]** avancée pour rechercher un schéma approprié.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-new-dataset.png)

The *[!UICONTROL Select schema]* dialog appears. Sélectionnez le schéma à appliquer au nouveau jeu de données, puis sélectionnez **[!UICONTROL Terminé]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Selon vos besoins, vous pouvez choisir de mapper directement les champs ou utiliser les fonctions de mappage pour transformer les données source afin de dériver des valeurs calculées ou calculées. Pour plus d’informations sur les fonctions de mappage et de mappage de données, consultez le didacticiel sur le [mappage des données CSV aux champs](../../../../../ingestion/tutorials/map-a-csv-file.md)de schéma XDM.

Une fois les données source mises en correspondance, sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

## Planifier les exécutions d&#39;assimilation

L&#39;étape *[!UICONTROL Planification]* s&#39;affiche, ce qui vous permet de configurer un programme d&#39;assimilation pour assimiler automatiquement les données source sélectionnées à l&#39;aide des mappages configurés. Le tableau suivant décrit les différents champs configurables pour la planification :

| Champ | Description |
| --- | --- |
| Fréquence | Les fréquences sélectionnables sont `Once`, `Minute`, `Hour`, `Day`et `Week`. |
| Intervalle | Entier qui définit l’intervalle pour la fréquence sélectionnée. |
| Début | Horodatage UTC indiquant à quel moment la première importation est prévue. |
| Renvoi | Valeur booléenne qui détermine quelles données sont initialement ingérées. Si le *[!UICONTROL renvoi]* est activé, tous les fichiers actuels du chemin d’accès spécifié seront ingérés lors de la première assimilation planifiée. Si le *renvoi* est désactivé, seuls les fichiers chargés entre la première exécution de l’assimilation et le délai *[!UICONTROL de]* Début seront ingérés. Les fichiers chargés avant l&#39;heure *[!UICONTROL de]* Début ne seront pas ingérés. |

Les flux de données sont conçus pour intégrer automatiquement les données sur une base planifiée. Début en sélectionnant la fréquence d&#39;ingestion. Ensuite, définissez l’intervalle pour désigner la période entre deux exécutions de flux. La valeur de l’intervalle doit être un entier non nul et doit être définie sur supérieur ou égal à 15.

Pour définir l’heure de début d’assimilation, ajustez la date et l’heure affichées dans la zone début d’heure. Vous pouvez également sélectionner l’icône de calendrier pour modifier la valeur de début. L&#39;heure du Début doit être supérieure ou égale à l&#39;heure actuelle en UTC.

Indiquez les valeurs de la planification et sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Configuration d’un flux de données d’assimilation unique

Pour configurer l’assimilation unique, sélectionnez la flèche de la liste déroulante des fréquences et sélectionnez **[!UICONTROL Une fois]**. Vous pouvez continuer à apporter des modifications à un jeu de flux de données pour une assimilation de fréquence unique, tant que le début de temps restera dans le futur. Une fois l’heure du début écoulée, la valeur de fréquence unique ne peut plus être modifiée.

>[!TIP] **[!UICONTROL L’intervalle]** et la **[!UICONTROL Renvoi]** ne sont pas visibles lors d’une assimilation unique.

Une fois que vous avez fourni les valeurs appropriées à la planification, sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Fournir des détails sur le flux de données

L’étape de détail ** Flux de données s’affiche, vous permettant de nommer et de décrire brièvement votre nouveau flux de données.

Au cours de ce processus, vous pouvez également activer les tests de diagnostic *[!UICONTROL d&#39;assimilation]* *[!UICONTROL partielle et d&#39;]* erreur. L&#39;activation de l&#39;assimilation ** partielle permet d&#39;assimiler des données contenant des erreurs, jusqu&#39;à un certain seuil que vous pouvez définir. L’activation des diagnostics *[!UICONTROL d’]* erreur fournit des détails sur les données incorrectes mises en lots séparément. Pour plus d&#39;informations, consultez la présentation [de l&#39;assimilation](../../../../../ingestion/batch-ingestion/partial.md)partielle des lots.

Fournissez des valeurs pour le flux de données et sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Vérifier votre flux de données

L’étape *[!UICONTROL Révision]* s’affiche, vous permettant de vérifier votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* *[!UICONTROL Connexion]*: Indique le type de source, le chemin d’accès approprié du fichier source choisi et le nombre de colonnes qu’il contient.
* *[!UICONTROL Attribuer des champs]* de jeu de données et de mappage : Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.
* *[!UICONTROL Planification]*: Affiche la période active, la fréquence et l&#39;intervalle du programme d&#39;assimilation.

Une fois que vous avez passé en revue votre flux de données, cliquez sur **[!UICONTROL Terminer]** et accordez un certain temps à la création du flux de données.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Surveiller et supprimer votre flux de données

Une fois le flux de données de votre enregistrement cloud créé, vous pouvez surveiller les données qui y sont ingérées. Pour plus d&#39;informations sur la surveillance et la suppression des flux de données, consultez le didacticiel sur la [surveillance des flux de données](../../../../../ingestion/quality/monitor-data-flows.md).

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer un flux de données pour importer des données à partir d’un enregistrement cloud externe et à mieux comprendre la surveillance des jeux de données. Pour en savoir plus sur la création de flux de données, vous pouvez compléter votre apprentissage en regardant la vidéo ci-dessous. En outre, les données entrantes peuvent désormais être utilisées par [!DNL Platform] les services en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

* [Présentation du profil client en temps réel](../../../../../profile/home.md)
* [Présentation de Data Science Workspace](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> L’ [!DNL Platform] interface utilisateur affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation ci-dessus pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Annexe

Les sections suivantes fournissent des informations supplémentaires sur l’utilisation des connecteurs source.

### Désactivation d’un flux de données

Lorsqu’un flux de données est créé, il devient immédiatement actif et ingère les données selon le planning qu’il a reçu. Vous pouvez désactiver un flux de données actif à tout moment en suivant les instructions ci-dessous.

Dans l’espace de travail *[!UICONTROL Sources]* , cliquez sur l’onglet **[!UICONTROL Parcourir]** . Cliquez ensuite sur le nom du compte associé au flux de données actif que vous souhaitez désactiver.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

La page activité ** source s&#39;affiche. Sélectionnez le flux de données actif dans la liste pour ouvrir sa colonne *[!UICONTROL Propriétés]* sur le côté droit de l&#39;écran, qui contient un bouton d&#39;activation **** de la bascule. Cliquez sur la bascule pour désactiver le flux de données. La même bascule peut être utilisée pour réactiver un flux de données après sa désactivation.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Activer les données entrantes pour [!DNL Profile] la population

Les données entrantes provenant de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos [!DNL Real-time Customer Profile] données. Pour plus d’informations sur le renseignement de vos [!DNL Profile] données client réel, voir le didacticiel sur la population [de](../../profile.md)Profils.
