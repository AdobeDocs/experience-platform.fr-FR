---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Oracle DB dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 9%

---


# Create an [!DNL Oracle DB] source connector in the UI

>[!NOTE]
>
> Le [!DNL Oracle DB] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur [!DNL Oracle DB] source à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model] (XDM) Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[ !Profil client en temps réel DNL]](../../../../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une [!DNL Oracle DB] connexion valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre [!DNL Oracle DB] compte [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour la connexion à [!DNL Oracle DB]. Le modèle de chaîne de [!DNL Oracle DB] connexion est le suivant : `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour [!DNL Oracle DB] est `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ce document](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199)Oracle.

## Connecter votre [!DNL Oracle DB] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Oracle DB] compte à [!DNL Platform]lequel vous connecter.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]** , sélectionnez **[!UICONTROL Oracle DB]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau [!DNL Oracle DB] connecteur.

![catalogue](../../../../images/tutorials/create/oracle/catalog.png)

La page **[!UICONTROL Se connecter à Oracle DB]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos [!DNL Oracle DB] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/oracle/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Oracle DB] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/oracle/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre [!DNL Oracle DB] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour y importer [!DNL Platform]](../../dataflow/databases.md)des données.