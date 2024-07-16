---
title: Création d’une connexion Google Ads Source dans l’interface utilisateur
description: Découvrez comment créer une connexion source Google Ads à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 29%

---

# Créer une connexion source Google Ads dans l’interface utilisateur

>[!WARNING]
>
>La source [!DNL Google Ads] est temporairement indisponible. Adobe s’efforce de résoudre les problèmes liés à cette source.

>[!NOTE]
>
>La source Google Ads est en version bêta. Pour plus d’informations sur l’utilisation de sources bêta étiquetées, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Ce tutoriel décrit les étapes à suivre pour créer une connexion source Google Ads à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion Google Ads valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/advertising.md)

### Collecter les informations d’identification requises

Pour accéder à votre plateforme de compte Google Ads, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| ID du client | L’ID client est le numéro de compte correspondant au compte client Google Ads que vous souhaitez gérer avec l’API Google Ads. Cet identifiant suit le modèle de `123-456-7890`. |
| Identifiant client de connexion | L’ID de client de connexion est le numéro de compte qui correspond à votre compte de gestionnaire de publicités Google et qui est utilisé pour récupérer les données de rapport d’un client opérationnel spécifique. Pour plus d’informations sur l’ID de client de connexion, consultez la [documentation de l’API Google Ads](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| Jeton de développeur | Le jeton de développement vous permet d’accéder à l’API Google Ads. Vous pouvez utiliser le même jeton de développement pour effectuer des requêtes sur tous vos comptes Google Ads. Récupérez votre jeton de développeur en [vous connectant à votre compte de gestionnaire](https://ads.google.com/home/tools/manager-accounts/), puis en accédant à la page du centre d’API. |
| Actualiser le jeton | Le jeton d’actualisation fait partie de l’authentification [!DNL OAuth2]. Ce jeton vous permet de régénérer vos jetons d’accès après leur expiration. |
| Identifiant client | L’ID client est utilisé en tandem avec le secret client dans le cadre de l’authentification [!DNL OAuth2]. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à Google. |
| Secret client | Le secret client est utilisé en tandem avec l’ID client dans le cadre de l’authentification [!DNL OAuth2]. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à Google. |

Lisez le document de présentation de l’API pour [plus d’informations sur la prise en main de Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Connexion à votre compte Google Ads

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Advertising]**, sélectionnez **[!UICONTROL Google Ads]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue des sources dans l’interface utilisateur Experience Platform.](../../../../images/tutorials/create/ads/catalog.png).

La page **[!UICONTROL Se connecter à Google Ads]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Google Ads avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Page de sélection des comptes existants dans le workflow des sources.](../../../../images/tutorials/create/ads/existing.png).

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification Google Ads. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte dans le workflow des sources.](../../../../images/tutorials/create/ads/new.png).

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte Google Ads. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données publicitaires dans Platform](../../dataflow/advertising.md).
