---
keywords: Experience Platform ; accueil ; sujets populaires ; Apache HDFS ; HDFS ; hdfs
solution: Experience Platform
title: Création d’une connexion source Apache HDFS dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Apache Hadoop Distributed File System à l'aide de l'interface utilisateur de Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 9%

---

# Créer une connexion source [!DNL Apache] HDFS dans l&#39;interface utilisateur

>[!NOTE]
>
>Le connecteur [!DNL Apache] HDFS est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Les connecteurs source de [!DNL Adobe Experience Platform] permettent d&#39;assimiler des données provenant de l&#39;extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source [!DNL Apache Hadoop Distributed File System] (ci-après dénommé &quot;HDFS&quot;) à l&#39;aide de l&#39;interface utilisateur [!DNL Platform].

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de [!DNL Platform] :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;une connexion HDFS valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source HDFS, vous devez fournir des valeurs pour la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | L’URL définit les paramètres d’authentification requis pour la connexion anonyme à HDFS. Pour plus d&#39;informations sur la façon d&#39;obtenir cette valeur, consultez le document suivant sur l&#39;[authentification HTTPS pour HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Connecter votre compte HDFS

Une fois que vous avez rassemblé les informations d&#39;identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte HDFS à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL enregistrement Cloud]**, sélectionnez **[!UICONTROL Apache HDFS]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un connecteur HDFS.

![catalogue](../../../../images/tutorials/create/hdfs/catalog.png)

La page **[!UICONTROL Se connecter à HDFS]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d&#39;entrée qui s&#39;affiche, indiquez un nom, une description facultative et vos informations d&#39;identification HDFS. Une fois terminé, sélectionnez **[!UICONTROL Se connecter à la source]**, puis attendez un certain temps pour que la nouvelle connexion s&#39;établisse.

![connecter](../../../../images/tutorials/create/hdfs/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte HDFS avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/hdfs/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte HDFS. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer les données de votre enregistrement cloud dans  [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
