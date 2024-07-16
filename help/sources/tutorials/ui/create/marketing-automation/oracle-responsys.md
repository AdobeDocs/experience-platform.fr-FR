---
keywords: Experience Platform;accueil;rubriques les plus consultées;sources;connecteurs;oracle;
title: (Version bêta) Créer une connexion source Oracle Responsys à l’aide de l’interface utilisateur de Platform
description: Découvrez comment connecter Adobe Experience Platform à Oracle Responsys à l’aide de l’interface utilisateur de Platform.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 97%

---

# (Version bêta) Créer une connexion source [!DNL Oracle Responsys] à l’aide de l’interface utilisateur de Platform

>[!NOTE]
>
>La source [!DNL Oracle Responsys] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Ce tutoriel vous fournit les étapes à suivre pour créer une connexion source [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) à l’aide de l’interface utilisateur d’Adobe Experience Platform.

## Prise en main

Ce guide nécessite une connaissance pratique des composants suivants de Platform :

* [Sources](../../../../home.md) : Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Si vous disposez déjà d’un compte authentifié [!DNL Oracle Responsys] sur Platform, alors vous pouvez ignorer le reste de ce document et passer au tutoriel sur comment [créer un flux de données pour apporter les données d’automatisation du marketing à Platform](../../dataflow/marketing-automation.md).

### Collecter les informations d’identification requises

Pour connecter [!DNL Oracle Responsys] à Platform, vous devez fournir des valeurs pour les propriétés d’authentification suivantes :

| Informations d’identification | Description |
| --- | --- |
| Point d’entrée | L’URL du point d’entrée d’authentification REST de votre instance [!DNL Oracle Responsys]. |
| Identifiant client | Identifiant client de votre instance [!DNL Oracle Responsys]. |
| Secret client | Secret client de votre instance [!DNL Oracle Responsys]. |

Pour plus d’informations sur les informations d’authentification pour [!DNL Oracle Responsys], consultez le [[!DNL Oracle Responsys] guide sur l’authentification](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL Oracle Responsys] à Platform.

## Connecter votre compte [!DNL Oracle Responsys]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie [!UICONTROL Automatisation du marketing], sélectionnez **[!UICONTROL Oracle Responsys]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources Adobe Experience Platform avec la source Oracle Responsys mise en surbrillance.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

La page **[!UICONTROL Connecter le compte Oracle Responsys]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Oracle Responsys] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![L’écran d’authentification du compte existant pour Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nouveau compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et les valeurs appropriées pour vos informations d’identification [!DNL Oracle Responsys]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![L’écran d’authentification de nouveau compte pour Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez authentifié et avez créé une connexion source entre votre compte [!DNL Oracle Responsys] et Platform. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour apporter les données d’automatisation du marketing à Platform](../../dataflow/marketing-automation.md).
