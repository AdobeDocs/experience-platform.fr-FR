---
keywords: Experience Platform;accueil;rubriques populaires;Stockage de fichiers Azure;Connecteur Azure File Storage
solution: Experience Platform
title: Créer une connexion Source de stockage de fichiers Azure dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source Azure File Storage à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 46%

---

# Créer une connexion source [!DNL Azure File Storage] dans l’interface utilisateur

Les connecteurs Source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour authentifier un connecteur source [!DNL Azure File Storage] à l’aide de l’interface utilisateur [!DNL Experience Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Azure File Storage] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecter les informations d’identification requises

Pour authentifier votre connecteur source [!DNL Azure File Storage], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point d’entrée de l’instance [!DNL Azure File Storage] à laquelle vous accédez. |
| `userId` | L’utilisateur disposant d’un accès suffisant au point d’entrée [!DNL Azure File Storage]. |
| `password` | La clé d’accès [!DNL Azure File Storage]. |

Pour plus d’informations sur la prise en main, consultez [ce [!DNL Azure File Storage] document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Connecter votre compte [!DNL Azure File Storage]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Azure File Storage] à [!DNL Experience Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Stockage de fichiers Azure]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur [!DNL Azure File Storage].

![catalogue](../../../../images/tutorials/create/azure-file-storage/catalog.png)

La page **[!UICONTROL Se connecter au stockage de fichiers Azure]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Azure File Storage]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis patientez quelques instants le temps d’établir la nouvelle connexion.

![connexion](../../../../images/tutorials/create/azure-file-storage/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Azure File Storage] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Azure File Storage]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de votre espace de stockage dans  [!DNL Experience Platform]](../../dataflow/batch/cloud-storage.md).
