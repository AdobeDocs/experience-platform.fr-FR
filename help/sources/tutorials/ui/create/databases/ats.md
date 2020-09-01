---
keywords: Experience Platform;home;popular topics;Azure Table Storage;azure table storage;ats;ATS
solution: Experience Platform
title: Création d'un connecteur source d'Enregistrement Azure Table dans l'interface utilisateur
topic: overview
description: Ce didacticiel décrit les étapes à suivre pour créer un connecteur source Azure Table Enregistrement (ci-après dénommé "ATS") à l'aide de l'interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 9%

---


# Create an [!DNL Azure Table Storage] source connector in the UI

>[!NOTE]
>
>Le [!DNL Azure Table Storage] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Azure Table Storage] (ci-après dénommé &quot;ATS&quot;) à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model] (XDM) Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[ !Profil client en temps réel DNL]](../../../../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion ATS valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte ATS sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion à votre [!DNL Azure Table Storage] instance. Chaîne de connexion à l’instance ATS. Le modèle de chaîne de connexion pour ATS est `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ [!DNL Azure Table Storage] ce document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Connecter votre [!DNL Azure Table Storage] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte ATS à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]** , sélectionnez Enregistrement **[!UICONTROL de table]** Azure. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur ATS.

![catalogue](../../../../images/tutorials/create/ats/catalog.png)

La page **[!UICONTROL Se connecter à l&#39;Enregistrement]** de table Azure s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification ATS. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/ats/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte ATS avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/ats/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte ATS. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour y importer [!DNL Platform]](../../dataflow/databases.md)des données.