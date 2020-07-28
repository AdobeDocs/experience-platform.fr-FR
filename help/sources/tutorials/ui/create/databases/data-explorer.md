---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'un connecteur source de Data Explorer Azure dans l'interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 15%

---


# Create an [!DNL Azure Data Explorer] source connector in the UI

>[!NOTE]
> Le [!DNL Azure Data Explorer] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source dans l’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Azure Data Explorer] (ci-après dénommé &quot;[!DNL Data Explorer]&quot;) à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une [!DNL Data Explorer] connexion valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre [!DNL Data Explorer] compte [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `endpoint` | Point de terminaison du [!DNL Data Explorer] serveur. |
| `database` | Nom de la [!DNL Data Explorer] base de données. |
| `tenant` | ID de client unique utilisé pour la connexion à la [!DNL Data Explorer] base de données. |
| `servicePrincipalId` | ID principal de service unique utilisé pour la connexion à la base de données du Data Explorer. |
| `servicePrincipalKey` | Clé principale de service unique utilisée pour la connexion à la base de données du Data Explorer. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ce document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)Data Explorer.

## Connecter votre [!DNL Azure Data Explorer] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un nouveau [!DNL Data Explorer] compte auquel vous connecter [!DNL Platform].

Connectez-vous à [l’Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant et chaque source affiche le nombre de comptes et de flux de jeux de données existants qui lui sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie *[!UICONTROL Bases de données]* , sélectionnez Data Explorer **** Azure et cliquez sur **l&#39;icône + (+)** pour créer un nouveau connecteur Data Explorer.

![catalogue](../../../../images/tutorials/create/data-explorer/catalog.png)

La page *[!UICONTROL Se connecter à Azure Data Explorer]* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez le nom de la connexion, une description facultative et vos [!DNL Data Explorer] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un certain temps à l’établissement du nouveau compte.

![connecter](../../../../images/tutorials/create/data-explorer/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Data Explorer] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/data-explorer/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre [!DNL Data Explorer] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/databases.md).