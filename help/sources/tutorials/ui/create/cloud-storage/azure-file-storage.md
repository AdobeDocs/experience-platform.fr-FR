---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'un connecteur source d'Enregistrement de fichiers Azure dans l'interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: b8ebe57482fdd10ccd8bdcf1a86009a373ea579e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# Création d&#39;un connecteur source d&#39;Enregistrement de fichiers Azure dans l&#39;interface utilisateur

>[!NOTE]
>L&#39;Enregistrement Azure Table est en version bêta. Les fonctionnalités et la documentation peuvent être modifiées.

Les connecteurs source d’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source d&#39;Enregistrement de fichiers Azure à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d&#39;une connexion à l&#39;Enregistrement de fichiers, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source d&#39;Enregistrement de fichiers Azure, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point de terminaison de l&#39;instance d&#39;Enregistrement de fichiers Azure à laquelle vous accédez. |
| `userId` | Utilisateur disposant d&#39;un accès suffisant au point de terminaison de l&#39;Enregistrement de fichiers Azure. |
| `password` | Clé d&#39;accès d&#39;Enregistrement de fichier Azure. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)d&#39;Enregistrement de fichier Azure.

## Connectez votre compte Azure File Enregistrement

Une fois que vous avez rassemblé les informations d&#39;identification requises, vous pouvez suivre les étapes ci-dessous pour créer un nouveau compte d&#39;Enregistrement de fichiers Azure à connecter à la plate-forme.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant et chaque source affiche le nombre de comptes et de flux de données existants qui y sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie *[!UICONTROL Bases de données]* , sélectionnez Enregistrement **[!UICONTROL de fichier]** Azure en cliquant **sur l&#39;icône + (+)** pour créer un nouveau connecteur d&#39;Enregistrement de fichier Azure.

![catalogue](../../../../images/tutorials/create/azure-file-storage/catalog.png)

La page *[!UICONTROL Se connecter à l&#39;Enregistrement]* de fichier Azure s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification d’Enregistrement de fichier pour la connexion. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un certain temps à l’établissement du nouveau compte.

![connecter](../../../../images/tutorials/create/azure-file-storage/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte d&#39;Enregistrement de fichiers Azure avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte Azure File Enregistrement. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données afin d’importer des données de votre enregistrement cloud dans la plate-forme](../../dataflow/batch/cloud-storage.md).