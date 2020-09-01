---
keywords: Experience Platform;home;popular topics;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Création d’un connecteur source Apache HDFS dans l’interface utilisateur
topic: overview
description: Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source Apache Hadoop Distributed File System (ci-après appelé "HDFS") à l’aide de l’interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 6%

---


# Create an [!DNL Apache] HDFS source connector in the UI

>[!NOTE]
>
>Le connecteur [!DNL Apache] HDFS est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source dans [!DNL Adobe Experience Platform] permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source [!DNL Apache Hadoop Distributed File System] (ci-après appelé &quot;HDFS&quot;) à l&#39;aide de l&#39; [!DNL Platform] interface utilisateur.

## Prise en main

This tutorial requires a working understanding of the following components of [!DNL Platform]:

- [[!DNL Experience Data Model] (XDM) Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[ !Profil client en temps réel DNL]](../../../../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d&#39;une connexion HDFS valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source HDFS, vous devez fournir des valeurs pour la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | L’URL définit les paramètres d’authentification requis pour la connexion anonyme à HDFS. Pour plus d&#39;informations sur la façon d&#39;obtenir cette valeur, consultez le document suivant sur l&#39;authentification [HTTPS pour HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Connecter votre compte HDFS

Une fois que vous avez rassemblé les informations d&#39;identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte HDFS à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Cloud enregistrement]** , sélectionnez **[!UICONTROL Apache HDFS]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur HDFS.

![catalogue](../../../../images/tutorials/create/hdfs/catalog.png)

La page **[!UICONTROL Se connecter à HDFS]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d&#39;entrée qui s&#39;affiche, indiquez un nom, une description facultative et vos informations d&#39;identification HDFS. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** , puis accordez un certain temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/hdfs/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte HDFS avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/hdfs/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte HDFS. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer [!DNL Platform]](../../dataflow/batch/cloud-storage.md)les données de votre enregistrement cloud.