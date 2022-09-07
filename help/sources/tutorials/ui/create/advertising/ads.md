---
keywords: Experience Platform;accueil;rubriques les plus consultées;Google Ads;connecteur source Google Ads;connecteur google ads
title: Création d’une connexion source Google Ads dans l’interface utilisateur
description: Découvrez comment créer une connexion source Google Ads à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 25%

---

# Création d’une connexion source Google Ads dans l’interface utilisateur

>[!NOTE]
>
>La source Google Ads est en version bêta. Voir [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Ce tutoriel décrit les étapes de création d’un connecteur source Google Ads à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de l’Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion Google Ads valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données](../../dataflow/advertising.md)

### Collecter les informations d’identification requises

Pour accéder à votre plateforme de compte Google Ads, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| ID client client | L’ID client est le numéro de compte correspondant au compte client Google Ads que vous souhaitez gérer avec l’API Google Ads. Cet identifiant suit le modèle de `123-456-7890`. |
| Jeton de développeur | Le jeton de développement vous permet d’accéder à l’API Google Ads. Vous pouvez utiliser le même jeton de développement pour effectuer des requêtes sur tous vos comptes Google Ads. Récupération du jeton de développement par [connexion à votre compte de gestionnaire](https://ads.google.com/home/tools/manager-accounts/) puis accédez à la page Centre d’API. |
| Jeton d’actualisation | Le jeton d’actualisation fait partie de [!DNL OAuth2] authentification. Ce jeton vous permet de régénérer vos jetons d’accès après leur expiration. |
| Identifiant client | L’ID client est utilisé en tandem avec le secret client dans le cadre de [!DNL OAuth2] authentification. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à Google. |
| Client secret | Le secret client est utilisé en tandem avec l’ID client dans le cadre de [!DNL OAuth2] authentification. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à Google. |

Lisez le document de présentation de l’API pour [en savoir plus sur la prise en main de Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Connexion à votre compte Google Ads

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **[!UICONTROL Publicité]** catégorie, sélectionnez **[!UICONTROL Publicités Google]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Image de la source Google Ads dans le catalogue des sources de l’interface utilisateur Experience Platform](../../../../images/tutorials/create/ads/catalog.png).

Le **[!UICONTROL Connexion à Google Ads]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Google Ads auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Image d’une liste de comptes existants que vous pouvez utiliser pour créer un flux de données Google Ads avec](../../../../images/tutorials/create/ads/existing.png).

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification Google Ads. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Image du nouvel écran de connexion au compte de l’interface utilisateur Experience Platform](../../../../images/tutorials/create/ads/connect.png).

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte Google Ads. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données publicitaires dans Platform ;](../../dataflow/advertising.md).
