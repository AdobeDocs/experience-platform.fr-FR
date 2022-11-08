---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;oracle;
title: (Version bêta) Création d’une connexion source Responsys Oracle à l’aide de l’interface utilisateur de Platform
description: Découvrez comment connecter Adobe Experience Platform à Oracle Responsys à l’aide de l’interface utilisateur de Platform.
source-git-commit: ff3cac5f18ea49b93b3d76e4cd8fb0d597d02be4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 38%

---

# (Version bêta) Créez une [!DNL Oracle Responsys] Connexion source à l’aide de l’interface utilisateur de Platform

>[!NOTE]
>
>Le [!DNL Oracle Responsys] La source est en version bêta. Voir [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs bêta-étiquetés.

Ce tutoriel décrit les étapes à suivre pour créer une [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) connexion source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants de Platform :

* [Sources](../../../../home.md): Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Si vous disposez déjà d’une authentification [!DNL Oracle Responsys] sur Platform, vous pouvez ignorer le reste de ce document et passer au tutoriel sur [création d’un flux de données pour importer des données d’automatisation du marketing dans Platform](../../dataflow/marketing-automation.md).

### Collecter les informations d’identification requises

Pour vous connecter [!DNL Oracle Responsys] sur Platform, vous devez fournir des valeurs pour les propriétés d’authentification suivantes :

| Informations d’identification | Description |
| --- | --- |
| Point d’entrée | L’URL du point d’entrée de l’authentification REST de votre [!DNL Oracle Responsys] instance. |
| Identifiant client | Identifiant client de l’instance [!DNL Oracle Responsys]. |
| Client secret | Secret client de l’instance [!DNL Oracle Responsys]. |

Pour plus d’informations sur les informations d’authentification pour [!DNL Oracle Responsys], reportez-vous à la section [[!DNL Oracle Responsys] guide sur l&#39;authentification](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL Oracle Responsys] à Platform.

## Connecter votre compte [!DNL Oracle Responsys]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , [!UICONTROL Automatisation du marketing] catégorie, sélectionnez **[!UICONTROL Oracle Responsys]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources Adobe Experience Platform avec l’Oracle source Responsys mis en surbrillance.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

Le **[!UICONTROL Connexion au compte Responsys Oracle]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Oracle Responsys] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Écran d’authentification de compte existant pour Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nouveau compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et les valeurs appropriées pour votre [!DNL Oracle Responsys] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvel écran d’authentification de compte pour Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez authentifié et créé une connexion source entre vos [!DNL Oracle Responsys] compte et plateforme. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour importer des données d’automatisation du marketing dans Platform ;](../../dataflow/marketing-automation.md).
