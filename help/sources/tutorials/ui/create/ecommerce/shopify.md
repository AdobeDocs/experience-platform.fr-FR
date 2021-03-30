---
keywords: Experience Platform ; accueil ; sujets populaires ; shopify ; Shopify
solution: Experience Platform
title: Création d’une connexion à la source Shopify dans l’interface utilisateur
topic: aperçu
type: Tutoriel
description: Découvrez comment créer une connexion source Shopify à l’aide de l’interface utilisateur de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cc23228cb410dc4c70a56c5142be00c2ca1c40d3
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 16%

---


# Créer une connexion source [!DNL Shopify] dans l’interface utilisateur

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Shopify] à l&#39;aide de l&#39;interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;une connexion [!DNL Shopify], vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données pour un connecteur de commerce électronique](../../dataflow/ecommerce.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL Shopify] sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point de terminaison de votre serveur [!DNL Shopify]. |
| `accessToken` | Jeton d&#39;accès de votre compte utilisateur [!DNL Shopify]. |

Pour plus d&#39;informations sur la prise en main, consultez ce [[!DNL Shopify] document](https://shopify.dev/concepts/about-apis/authentication).

## Connectez votre compte [!DNL Shopify]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Shopify] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL eCommerce]**, sélectionnez **[!UICONTROL Shopify]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un connecteur [!DNL Shopify].

![catalogue](../../../../images/tutorials/create/shopify/catalog.png)

La page **[!UICONTROL Se connecter à Shopify]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Shopify]. Une fois terminé, sélectionnez **[!UICONTROL Se connecter]**, puis accordez un certain temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/shopify/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Shopify] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/shopify/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte [!DNL Shopify]. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer les données eCommerce dans  [!DNL Platform]](../../dataflow/ecommerce.md).