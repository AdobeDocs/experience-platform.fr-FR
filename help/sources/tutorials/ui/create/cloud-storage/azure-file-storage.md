---
keywords: Experience Platform;home;popular topics;Azure File Storage;Azure File Storage connector
solution: Experience Platform
title: Création d'un connecteur source d'Enregistrement de fichiers Azure dans l'interface utilisateur
topic: overview
type: Tutorial
description: Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source d'Enregistrement de fichiers Azure à l'aide de l'interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 12%

---


# Create an [!DNL Azure File Storage] source connector in the UI

>[!NOTE]
>
>Le [!DNL Azure File Storage] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur [!DNL Azure File Storage] source à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une [!DNL Azure File Storage] connexion valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur [!DNL Azure File Storage] source, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point de terminaison de l’ [!DNL Azure File Storage] instance à laquelle vous accédez. |
| `userId` | Utilisateur disposant d’un accès suffisant au point de [!DNL Azure File Storage] terminaison. |
| `password` | Clé [!DNL Azure File Storage] d’accès. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ [!DNL Azure File Storage] ce document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Connecter votre [!DNL Azure File Storage] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Azure File Storage] compte à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]** , sélectionnez Enregistrement **[!UICONTROL de fichier]** Azure. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau [!DNL Azure File Storage] connecteur.

![catalogue](../../../../images/tutorials/create/azure-file-storage/catalog.png)

La page **[!UICONTROL Se connecter à l&#39;Enregistrement]** de fichier Azure s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos [!DNL Azure File Storage] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/azure-file-storage/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Azure File Storage] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre [!DNL Azure File Storage] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer [!DNL Platform]](../../dataflow/batch/cloud-storage.md)les données de votre enregistrement cloud.