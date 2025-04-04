---
keywords: Experience Platform;accueil;rubriques populaires;shopify;Shopify
solution: Experience Platform
title: Créer une connexion Shopify Source dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source Shopify à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 45%

---

# Créer une connexion source [!DNL Shopify] dans l’interface utilisateur

Les connecteurs Source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL Shopify] à l’aide de l’interface utilisateur de [!DNL Experience Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Shopify], vous pouvez ignorer le reste de ce document et passer au tutoriel sur [la configuration d’un flux de données pour un connecteur eCommerce](../../dataflow/ecommerce.md).

### Collecter les informations d’identification requises

Pour accéder à votre compte [!DNL Shopify] sur [!DNL Experience Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point d’entrée de votre serveur [!DNL Shopify]. |
| `accessToken` | Jeton d’accès de votre compte utilisateur [!DNL Shopify]. |

Pour plus d’informations sur la prise en main, reportez-vous à ce [[!DNL Shopify] document](https://shopify.dev/concepts/about-apis/authentication).

## Connecter votre compte [!DNL Shopify]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Shopify] à [!DNL Experience Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL eCommerce]**, sélectionnez **[!UICONTROL Shopify]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur [!DNL Shopify].

![catalogue](../../../../images/tutorials/create/shopify/catalog.png)

La page **[!UICONTROL Se connecter à Shopify]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Shopify]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis patientez quelques instants le temps d’établir la nouvelle connexion.

![connexion](../../../../images/tutorials/create/shopify/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Shopify] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/shopify/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Shopify]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données d’e-commerce dans [!DNL Experience Platform]](../../dataflow/ecommerce.md).
