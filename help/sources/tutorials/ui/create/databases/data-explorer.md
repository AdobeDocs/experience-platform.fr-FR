---
keywords: Experience Platform ; accueil ; rubriques populaires ; Data Explorer Azure ; explorateur de données azur ; explorateur de données ; Data Explorer
solution: Experience Platform
title: Création d'une connexion à la source du Data Explorer Azure dans l'interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Azure Data Explorer à l'aide de l'interface utilisateur de Adobe Experience Platform.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 11%

---

# Créer une connexion source [!DNL Azure Data Explorer] dans l’interface utilisateur

>[!NOTE]
>
> Le connecteur [!DNL Azure Data Explorer] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Azure Data Explorer] (ci-après dénommé &quot;[!DNL Data Explorer]&quot;) à l&#39;aide de l&#39;interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;une connexion [!DNL Data Explorer] valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL Data Explorer] sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `endpoint` | Point de terminaison du serveur [!DNL Data Explorer]. |
| `database` | Nom de la base de données [!DNL Data Explorer]. |
| `tenant` | ID de client unique utilisé pour la connexion à la base de données [!DNL Data Explorer]. |
| `servicePrincipalId` | ID principal de service unique utilisé pour la connexion à la base de données [!DNL Data Explorer]. |
| `servicePrincipalKey` | Clé principale de service unique utilisée pour la connexion à la base de données [!DNL Data Explorer]. |

Pour plus d&#39;informations sur la prise en main, consultez [ce [!DNL Data Explorer] document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Connectez votre compte [!DNL Azure Data Explorer]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Data Explorer] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Data Explorer Azure]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un connecteur de Data Explorer.

![catalogue](../../../../images/tutorials/create/data-explorer/catalog.png)

La page **[!UICONTROL Se connecter à Azure Data Explorer]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Data Explorer]. Une fois terminé, sélectionnez **[!UICONTROL Se connecter]**, puis accordez un certain temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/data-explorer/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Data Explorer] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/data-explorer/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte [!DNL Data Explorer]. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans  [!DNL Platform]](../../dataflow/databases.md).
