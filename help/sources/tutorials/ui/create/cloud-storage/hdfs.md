---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Apache HDFS dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 12%

---


# Create an [!DNL Apache] HDFS source connector in the UI

>[!NOTE]
>Le connecteur [!DNL Apache] HDFS est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source dans [!DNL Adobe Experience Platform] permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source [!DNL Apache Hadoop Distributed File System] (ci-après appelé &quot;HDFS&quot;) à l&#39;aide de l&#39; [!DNL Platform] interface utilisateur.

## Prise en main

This tutorial requires a working understanding of the following components of [!DNL Platform]:

- [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;une connexion HDFS, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source HDFS, vous devez fournir des valeurs pour la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | L’URL définit les paramètres d’authentification requis pour la connexion anonyme à HDFS. Pour plus d&#39;informations sur la façon d&#39;obtenir cette valeur, consultez le document suivant sur l&#39;authentification [HTTPS pour HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Connecter votre compte HDFS

Une fois que vous avez rassemblé les informations d&#39;identification requises, vous pouvez suivre les étapes ci-dessous pour créer un compte HDFS auquel vous connecter [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant et chaque source affiche le nombre de comptes et de flux de données existants qui y sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous *[!UICONTROL Cloud enregistrement]* catégorie, sélectionnez **[!UICONTROL Apache HDFS]** , puis **[!UICONTROL Ajoutez les données]** pour créer un nouveau connecteur HDFS.

![catalogue](../../../../images/tutorials/create/hdfs/catalog.png)

La page *[!UICONTROL Se connecter à HDFS]* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification d’Enregistrement de fichier pour la connexion. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** , puis accordez du temps au nouveau compte pour établir.

![connecter](../../../../images/tutorials/create/hdfs/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte HDFS avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/hdfs/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte HDFS. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données afin d’importer des données de votre enregistrement cloud dans la plate-forme](../../dataflow/batch/cloud-storage.md).