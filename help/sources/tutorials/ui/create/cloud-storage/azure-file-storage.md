---
keywords: Experience Platform ; accueil ; rubriques populaires ; Enregistrement de fichiers Azure ; connecteur d'Enregistrement de fichiers Azure
solution: Experience Platform
title: Créer une connexion à la source d'Enregistrement de fichiers Azure dans l'interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source d'Enregistrement de fichiers Azure à l'aide de l'interface utilisateur de Adobe Experience Platform.
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 12%

---

# Créer une connexion source [!DNL Azure File Storage] dans l’interface utilisateur

>[!NOTE]
>
>Le connecteur [!DNL Azure File Storage] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source [!DNL Azure File Storage] à l&#39;aide de l&#39;interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;une connexion [!DNL Azure File Storage] valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source [!DNL Azure File Storage], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point de terminaison de l&#39;instance [!DNL Azure File Storage] à laquelle vous accédez. |
| `userId` | Utilisateur disposant d’un accès suffisant au point de terminaison [!DNL Azure File Storage]. |
| `password` | Clé d&#39;accès [!DNL Azure File Storage]. |

Pour plus d&#39;informations sur la prise en main, consultez [ce [!DNL Azure File Storage] document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Connectez votre compte [!DNL Azure File Storage]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Azure File Storage] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Enregistrement de fichier Azure]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un connecteur [!DNL Azure File Storage].

![catalogue](../../../../images/tutorials/create/azure-file-storage/catalog.png)

La page **[!UICONTROL Se connecter à l&#39;Enregistrement de fichier Azure]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Azure File Storage]. Une fois terminé, sélectionnez **[!UICONTROL Se connecter]**, puis accordez un certain temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/azure-file-storage/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Azure File Storage] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte [!DNL Azure File Storage]. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer les données de votre enregistrement cloud dans  [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
