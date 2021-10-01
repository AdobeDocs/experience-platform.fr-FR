---
keywords: Experience Platform;accueil;rubriques les plus consultées;Google AdWords;connecteur source Google AdWords;connecteur google adwords
solution: Experience Platform
title: Création d’une connexion source Google AdWords dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Google AdWords à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 11%

---

# Création d’une connexion source [!DNL Google AdWords] dans l’interface utilisateur

>[!NOTE]
>
>Le connecteur [!DNL Google AdWords] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Les connecteurs source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL Google AdWords] à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Google AdWords] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur [la configuration d’un flux de données](../../dataflow/payments.md)

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL Google AdWords] [!DNL Platform], vous devez fournir les valeurs suivantes :

| Credential | Description |
| ---------- | ----------- |
| `clientCustomerId` | Identifiant client du compte [!DNL AdWords]. |
| `developerToken` | Jeton de développeur associé au compte de gestionnaire. |
| `refreshToken` | Jeton d’actualisation obtenu à partir de [!DNL Google] pour autoriser l’accès à [!DNL AdWords]. |
| `clientId` | ID client de l’application [!DNL Google] utilisée pour acquérir le jeton d’actualisation. |
| `clientSecret` | Secret client de l’application [!DNL Google] utilisée pour acquérir le jeton d’actualisation. |

Pour plus d’informations sur la prise en main, consultez ce [[!DNL Google AdWords] document](https://developers.google.com/adwords/api/docs/guides/authentication).

## Connectez votre compte [!DNL Google AdWords]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Google AdWords] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Publicité]** , sélectionnez **[!UICONTROL Google AdWords]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur [!DNL Google AdWords].

![catalogue](../../../../images/tutorials/create/ads/catalog.png)

La page **[!UICONTROL Se connecter à Google AdWords]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Google AdWords]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]**, puis laissez un certain temps pour établir la nouvelle connexion.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Google AdWords] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/ads/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Google AdWords]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données publicitaires dans [!DNL Platform]](../../dataflow/advertising.md).
