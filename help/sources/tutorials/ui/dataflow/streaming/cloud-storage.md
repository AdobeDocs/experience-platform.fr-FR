---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configuration d’un flux de données pour un connecteur de flux continu d’enregistrement cloud dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---


# Configuration d’un flux de données pour un connecteur de flux continu d’enregistrement cloud dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source dans un [!DNL Platform] jeu de données. Ce didacticiel décrit les étapes à suivre pour configurer un nouveau flux de données à l’aide de votre connecteur de base d’enregistrements de cloud.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de l&#39;Adobe Experience Platform :

- [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

De plus, ce didacticiel nécessite que vous ayez déjà créé un connecteur d’enregistrement de cloud. Vous trouverez une liste de didacticiels pour la création de différents connecteurs d’enregistrement de cloud dans l’interface utilisateur dans l’aperçu [des connecteurs](../../../../home.md)source.

## Sélectionner des données

Après avoir créé votre connecteur d’enregistrement de cloud, l’étape *Sélectionner les données* s’affiche, ce qui vous permet de sélectionner le flux à partir duquel vous diffuserez les données.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Mappage des champs de données à un schéma XDM

L’étape *Mappage* s’affiche, fournissant une interface interactive permettant de mapper les données source à un [!DNL Platform] jeu de données.

Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez soit utiliser un jeu de données existant, soit en créer un nouveau.

**Utiliser un jeu de données existant**

Pour importer des données dans un jeu de données existant, sélectionnez **[!UICONTROL Utiliser un jeu de données]** existant, puis cliquez sur l’icône Jeu de données.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

La boîte de dialogue _Sélectionner un jeu de données_ s&#39;affiche. Recherchez le jeu de données que vous souhaitez utiliser, sélectionnez-le, puis cliquez sur **[!UICONTROL Continuer]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Utiliser un nouveau jeu de données**

Pour importer des données dans un nouveau jeu de données, sélectionnez **[!UICONTROL Créer un jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis. Sélectionnez ensuite le schéma à utiliser dans la liste déroulante.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Nommer votre flux de données

L’étape de détail ** Flux de données s’affiche, vous permettant de nommer et de décrire brièvement votre nouveau flux de données.

Fournissez des valeurs pour le flux de données et cliquez sur **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Vérifier votre flux de données

L’étape *Révision* s’affiche, vous permettant de vérifier votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

- *[!UICONTROL Détails]* de la source : Affiche le type de source et d’autres détails pertinents sur la source.
- *[!UICONTROL Détails]* de la Cible : Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.

Une fois que vous avez passé en revue votre flux de données, cliquez sur **[!UICONTROL Terminer]** et accordez un certain temps à la création du flux de données.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Surveiller votre flux de données

Une fois le flux de données de votre enregistrement cloud créé, vous pouvez surveiller les données qui y sont ingérées. Pour plus d’informations sur la surveillance des jeux de données, voir le didacticiel sur la [surveillance des flux de données](../../../../../ingestion/quality/monitor-data-flows.md)en flux continu.

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer un flux de données pour importer des données à partir d’un enregistrement cloud externe et à mieux comprendre la surveillance des jeux de données. Les données entrantes peuvent désormais être utilisées par [!DNL Platform] les services en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../../../profile/home.md)
- [Présentation de Data Science Workspace](../../../../../data-science-workspace/home.md)

## Annexe

Les sections suivantes fournissent des informations supplémentaires sur l’utilisation des connecteurs source.

### Désactivation d’un flux de données

Lorsqu’un flux de données est créé, il devient immédiatement actif et ingère les données selon le planning qu’il a reçu. Vous pouvez désactiver un flux de données actif à tout moment en suivant les instructions ci-dessous.

Dans l’espace de travail *[!UICONTROL Sources]* , cliquez sur l’onglet **[!UICONTROL Parcourir]** . Cliquez ensuite sur le nom de la connexion de base associée au flux de données actif que vous souhaitez désactiver.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

La page activité ** source s&#39;affiche. Sélectionnez le flux de données actif dans la liste pour ouvrir sa colonne *Propriétés* sur le côté droit de l&#39;écran, qui contient un bouton d&#39;activation **** de la bascule. Cliquez sur la bascule pour désactiver le flux de données. La même bascule peut être utilisée pour réactiver un flux de données après sa désactivation.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Activer les données entrantes pour [!DNL Profile] la population

Les données entrantes provenant de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos [!DNL Real-time Customer Profile] données. Pour plus d&#39;informations sur le remplissage de vos [!DNL Real-time Customer Profile] données, consultez le didacticiel sur la population [](../../profile.md)Profil.
