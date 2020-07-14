---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configuration d’un flux de données pour un connecteur de succès client dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 168ac3a3ab9f475cb26dc8138cbc90a3e35c836d
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 8%

---


# Configuration d’un flux de données pour un connecteur de succès client dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source dans un [!DNL Platform] jeu de données. Ce didacticiel décrit les étapes à suivre pour configurer un nouveau flux de données à l’aide de votre compte de réussite client.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Système de modèle de données d’expérience (XDM)](../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Real-time Customer Profile](../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

En outre, ce didacticiel nécessite que vous ayez déjà créé un compte de réussite client. Vous trouverez une liste de didacticiels pour la création de différents connecteurs de succès client dans l’interface utilisateur dans l’aperçu [des connecteurs](../../../home.md)source.

## Sélectionner des données

Après avoir créé votre connecteur de succès client, l’étape *[!UICONTROL Sélectionner les données]* s’affiche, ce qui vous permet d’explorer la hiérarchie des fichiers dans une interface interactive.

- La moitié gauche de l&#39;interface est un navigateur d&#39;annuaire qui affiche les fichiers et répertoires de votre serveur.
- La moitié droite de l&#39;interface vous permet de prévisualisation jusqu&#39;à 100 lignes de données à partir d&#39;un fichier compatible.

Sélectionnez le répertoire à utiliser, puis cliquez sur **[!UICONTROL Suivant]**.

![select-data](../../../images/tutorials/dataflow/customer-success/select-data.png)

## Mappage des champs de données à un schéma XDM

L’étape *[!UICONTROL Mappage]* s’affiche, fournissant une interface interactive permettant de mapper les données source à un [!DNL Platform] jeu de données.

Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

### Utilisation d’un jeu de données existant

Pour importer des données dans un jeu de données existant, sélectionnez **[!UICONTROL Utiliser un jeu de données]** existant, puis cliquez sur l’icône Jeu de données.

![use-existing-dataset](../../../images/tutorials/dataflow/customer-success/use-existing-dataset.png)

The *[!UICONTROL Select dataset]* dialog appears. Recherchez le jeu de données que vous souhaitez utiliser, sélectionnez-le, puis cliquez sur **[!UICONTROL Continuer]**.

![select-existing-dataset](../../../images/tutorials/dataflow/customer-success/select-dataset.png)

### Utiliser un nouveau jeu de données

Pour importer des données dans un nouveau jeu de données, sélectionnez **[!UICONTROL Créer un jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis.

Au cours de ce processus, vous pouvez également activer les tests de diagnostic *[!UICONTROL d&#39;assimilation]* *[!UICONTROL partielle et d&#39;]* erreur. L&#39;activation de l&#39;assimilation ** partielle permet d&#39;assimiler des données contenant des erreurs, jusqu&#39;à un certain seuil que vous pouvez définir. L’activation des diagnostics *[!UICONTROL d’]* erreur fournit des détails sur les données incorrectes mises en lots séparément. Pour plus d&#39;informations, consultez la présentation [de l&#39;assimilation](../../../../ingestion/batch-ingestion/partial.md)partielle des lots.

Cliquez ensuite sur l’icône schéma.

![use-new-dataset](../../../images/tutorials/dataflow/customer-success/use-new-dataset.png)

The *[!UICONTROL Select schema]* dialog appears. Sélectionnez le schéma à appliquer au nouveau jeu de données, puis cliquez sur **[!UICONTROL Terminé]**.

![sélection-schéma](../../../images/tutorials/dataflow/customer-success/select-schema.png)

Selon vos besoins, vous pouvez choisir de mapper directement les champs ou utiliser les fonctions de mappage pour transformer les données source afin de dériver des valeurs calculées ou calculées. Pour plus d’informations sur les fonctions de mappage et de mappage de données, consultez le didacticiel sur le [mappage des données CSV aux champs](../../../../ingestion/tutorials/map-a-csv-file.md)de schéma XDM.

Une fois les données source mises en correspondance, cliquez sur **[!UICONTROL Suivant]**.

![mappage](../../../images/tutorials/dataflow/customer-success/mapping.png)

## Planifier les exécutions d&#39;assimilation

L&#39;étape *[!UICONTROL Planification]* s&#39;affiche, ce qui vous permet de configurer un programme d&#39;assimilation pour assimiler automatiquement les données source sélectionnées à l&#39;aide des mappages configurés. Le tableau suivant décrit les différents champs configurables pour la planification :

| Champ | Description |
| --- | --- |
| Fréquence | Les fréquences sélectionnées sont les suivantes : Minute, Heure, Jour et Semaine. |
| Intervalle | Entier qui définit l’intervalle pour la fréquence sélectionnée. |
| Début | Horodatage UTC pour lequel la toute première importation aura lieu. |
| Renvoi | Valeur booléenne qui détermine quelles données sont initialement ingérées. Si le *[!UICONTROL renvoi]* est activé, tous les fichiers actuels du chemin d’accès spécifié seront ingérés lors de la première assimilation planifiée. Si le *[!UICONTROL renvoi]* est désactivé, seuls les fichiers chargés entre la première exécution de l’assimilation et le délai *[!UICONTROL de]* Début seront ingérés. Les fichiers chargés avant l&#39;heure *[!UICONTROL de]* Début ne seront pas ingérés. |

Les flux de données sont conçus pour intégrer automatiquement les données sur une base planifiée. Si vous souhaitez effectuer une seule assimilation via ce flux de travail, vous pouvez le faire en configurant la **[!UICONTROL fréquence]** sur &quot;Jour&quot; et en appliquant un nombre très élevé pour l’ **[!UICONTROL intervalle]**, tel que 10000 ou un nombre similaire.

Indiquez les valeurs de la planification et cliquez sur **[!UICONTROL Suivant]**.

![scheduling](../../../images/tutorials/dataflow/customer-success/scheduling.png)


## Vérifier votre flux de données

L’étape *[!UICONTROL Révision]* s’affiche, vous permettant de vérifier votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

- *[!UICONTROL Détails]* de la connexion : Indique le type de source, le chemin d’accès approprié du fichier source choisi et le nombre de colonnes qu’il contient.
- *[!UICONTROL Détails]* du mappage : Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.
- *[!UICONTROL Détails]* de la planification : Affiche la période active, la fréquence et l&#39;intervalle du programme d&#39;assimilation.

Une fois que vous avez passé en revue votre flux de données, cliquez sur **[!UICONTROL Terminer]** et accordez un certain temps à la création du flux de données.

![examiner](../../../images/tutorials/dataflow/customer-success/review.png)

## Surveiller et supprimer votre flux de données

Une fois que votre flux de données a été créé, vous pouvez surveiller les données qui y sont ingérées. Pour plus d&#39;informations sur la surveillance et la suppression de votre flux de données, consultez le didacticiel sur la [surveillance et la suppression des flux de données](../monitor.md).

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer un flux de données afin d’importer des données d’une source de succès client et d’obtenir des informations sur la surveillance des jeux de données. Les données entrantes peuvent désormais être utilisées par [!DNL Platform] les services en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../../profile/home.md)
- [Présentation de Data Science Workspace](../../../../data-science-workspace/home.md)

## Annexe

Les sections suivantes fournissent des informations supplémentaires sur l’utilisation des connecteurs source.

### Désactivation d’un flux de données

Lorsqu’un flux de données est créé, il devient immédiatement actif et ingère les données selon le planning qu’il a reçu. Vous pouvez désactiver un flux de données actif à tout moment en suivant les instructions ci-dessous.

Dans l’écran *[!UICONTROL d’authentification]* , sélectionnez le nom du compte associé au flux de données que vous souhaitez désactiver.

![](../../../images/tutorials/dataflow/customer-success/monitor.png)

La page activité __ source s&#39;affiche. Sélectionnez le flux de données actif dans la liste pour ouvrir sa colonne *[!UICONTROL Propriétés]* sur le côté droit de l&#39;écran, qui contient un bouton d&#39;activation **** de la bascule. Cliquez sur la bascule pour désactiver le flux de données. La même bascule peut être utilisée pour réactiver un flux de données après sa désactivation.

![disable](../../../images/tutorials/dataflow/customer-success/disable.png)

### Activer les données entrantes pour [!DNL Profile] la population

Les données entrantes provenant de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos [!DNL Real-time Customer Profile] données. Pour plus d&#39;informations sur le remplissage de vos [!DNL Real-time Customer Profile] données, consultez le didacticiel sur la population [](../profile.md)Profil.