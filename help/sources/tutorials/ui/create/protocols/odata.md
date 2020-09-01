---
keywords: Experience Platform;home;popular topics;OData;odata;Generic Open Data Protocol
solution: Experience Platform
title: Création d’un connecteur source OData générique dans l’interface utilisateur
topic: overview
description: Ce didacticiel décrit les étapes à suivre pour créer un connecteur source Open Data Protocol générique (ci-après appelé "OData") à l’aide de l’interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 9%

---


# Create a [!DNL Generic OData] source connector in the UI

>[!NOTE]
>
> Le [!DNL Generic OData] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Generic Open Data Protocol] (ci-après dénommé &quot;[!DNL OData]&quot;) à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model] (XDM) Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[ !Profil client en temps réel DNL]](../../../../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une [!DNL OData] connexion valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données.](../../dataflow/protocols.md)

### Collecte des informations d’identification requises

Pour accéder à votre [!DNL OData] compte dans [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | URL racine du [!DNL OData] service. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ [!DNL OData] ce document](https://www.odata.org/getting-started/basic-tutorial/).

## Connecter votre [!DNL OData] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL OData] compte à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Protocoles]** , sélectionnez **[!UICONTROL Générique OData]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau [!DNL OData] connecteur.

![catalogue](../../../../images/tutorials/create/odata/catalog.png)

La page **[!UICONTROL Se connecter à une OData]** générique s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez le nom de la connexion, une description facultative et vos [!DNL OData] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/odata/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL OData] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/odata/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre [!DNL OData] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données de protocole dans [!DNL Platform]](../../dataflow/protocols.md).