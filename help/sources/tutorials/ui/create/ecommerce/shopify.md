---
keywords: Experience Platform;accueil;rubriques populaires;shopify;Shopify
solution: Experience Platform
title: Création d’une connexion source Shopify dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source Shopify à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 54%

---

# Créer une connexion source [!DNL Shopify] dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’ingérer des données externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL Shopify] à l’aide de l’interface utilisateur de [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une [!DNL Shopify] vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données pour un connecteur eCommerce](../../dataflow/ecommerce.md).

### Collecter les informations d’identification requises

Pour accéder au compte [!DNL Shopify] sur , vous devez fournir les valeurs suivantes :[!DNL Platform]

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Le point de terminaison de votre [!DNL Shopify] serveur. |
| `accessToken` | Jeton d’accès pour votre [!DNL Shopify] compte utilisateur. |

Pour plus d’informations sur la prise en main, reportez-vous à cette section [[!DNL Shopify] document](https://shopify.dev/concepts/about-apis/authentication).

## Connecter votre compte [!DNL Shopify]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Shopify] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au **[!UICONTROL Sources]** workspace. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **[!UICONTROL eCommerce]** catégorie, sélectionnez **[!UICONTROL Shopify]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer [!DNL Shopify] connecteur.

![catalogue](../../../../images/tutorials/create/shopify/catalog.png)

Le **[!UICONTROL Connexion à Shopify]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et [!DNL Shopify] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![connect](../../../../images/tutorials/create/shopify/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Shopify] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/shopify/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Shopify]. Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données eCommerce dans [!DNL Platform]](../../dataflow/ecommerce.md).
