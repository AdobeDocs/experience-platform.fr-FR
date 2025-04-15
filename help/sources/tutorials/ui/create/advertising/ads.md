---
title: Connexion de Google Ads à Experience Platform à l’aide de l’interface utilisateur
description: Découvrez comment connecter votre compte Google Ads à Adobe Experience Platform dans l’interface utilisateur.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 009866abc39b06c22b7bea758ce9fdfba8c72b00
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 10%

---

# Connexion d’[!DNL Google Ads] à Experience Platform à l’aide de l’interface utilisateur

>[!WARNING]
>
>La source [!DNL Google Ads] n’est actuellement pas disponible dans l’interface utilisateur. Vous pouvez continuer à ingérer vos données [!DNL Google Ads] dans Experience Platform [à l’aide de l’API](../../../api/create/advertising/ads.md).

>[!NOTE]
>
>La source [!DNL Google Ads] est en version Beta. Consultez la [ Présentation des sources ](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Lisez ce guide pour savoir comment connecter votre compte [!DNL Google Ads] à Adobe Experience Platform à l’aide de l’espace de travail des sources dans l’interface utilisateur d’Experience Platform.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Google Ads] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur [la configuration d’un flux de données](../../dataflow/advertising.md)

### Collecter les informations d’identification requises

Pour plus d’informations sur l’authentification, consultez la [[!DNL Google Ads] présentation de la source](../../../../connectors/advertising/ads.md).

## Connecter votre compte Google Ads

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]*. Vous pouvez sélectionner la catégorie appropriée dans le panneau *[!UICONTROL Catégories]*. Vous pouvez également utiliser la barre de recherche pour accéder à la source spécifique que vous souhaitez utiliser.

Pour utiliser [!DNL Google Ads], sélectionnez la carte source **[!UICONTROL Google Ads]** sous *[!UICONTROL Advertising]* puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue de sources dans l’interface utilisateur d’Experience Platform.](../../../../images/tutorials/create/ads/catalog.png).

### Compte existant

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte à utiliser dans la liste des comptes de l’interface.

Une fois votre compte sélectionné, sélectionnez **[!UICONTROL Suivant]** pour passer à l’étape suivante.

![Page de sélection des comptes existants dans le workflow des sources.](../../../../images/tutorials/create/ads/existing.png).

### Nouveau compte

Si vous ne disposez pas d’un compte existant, vous devez créer un compte en fournissant les informations d’authentification nécessaires qui correspondent à votre source.

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** puis indiquez un nom de compte et éventuellement une description pour les détails de votre compte. Ensuite, fournissez les valeurs d’authentification appropriées pour authentifier votre source par rapport à Experience Platform :

* **Identifiant client** : l’identifiant client est le numéro de compte qui correspond au compte client [!DNL Google Ads] que vous souhaitez gérer avec l’API [!DNL Google Ads]. Cet identifiant suit le modèle de `123-456-7890`.
* **ID de client de connexion** : l’ID de client de connexion est le numéro de compte qui correspond à votre compte [!DNL Google Ads] Manager et qui est utilisé pour récupérer les données de rapport d’un client opérationnel spécifique. Pour plus d’informations sur l’ID de client de connexion, consultez la documentation de l’API [[!DNL Google Ads] ](https://developers.google.com/search-ads/reporting/concepts/login-customer-id).
* **Jeton de développeur** : le jeton de développeur vous permet d’accéder à l’API [!DNL Google Ads]. Vous pouvez utiliser le même jeton de développement pour effectuer des requêtes sur tous vos comptes [!DNL Google Ads]. Récupérez votre jeton de développeur en [vous connectant à votre compte Manager](https://ads.google.com/home/tools/manager-accounts/) puis en accédant à la page du Centre API.
* **Jeton d’actualisation** : le jeton d’actualisation fait partie de l’authentification [!DNL OAuth2]. Ce jeton vous permet de régénérer vos jetons d’accès après leur expiration.
* **Identifiant client** : l’identifiant client est utilisé conjointement avec le secret client dans le cadre de l’authentification [!DNL OAuth2]. Ensemble, l’identifiant client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à [!DNL Google].
* **Secret client** : le secret client est utilisé conjointement avec l’identifiant client dans le cadre de l’authentification [!DNL OAuth2]. Ensemble, l’identifiant client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à [!DNL Google].
* Version de l’API **[!DNL Google Ads]** : version actuelle de l’API prise en charge par [!DNL Google Ads]. Bien que la dernière version soit `v18`, la dernière version prise en charge sur Experience Platform est `v17`.

Une fois vos informations d’identification saisies, sélectionnez **[!UICONTROL Se connecter à la source]** et patientez quelques instants le temps que la connexion soit traitée. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Nouvelle interface de compte dans le workflow des sources.](../../../../images/tutorials/create/ads/new.png).

## Sélectionner les données {#select-data}

Avec [!DNL Google Ads], vous devez fournir la liste des attributs à ingérer pendant la phase de sélection des données du workflow. Pour récupérer ces attributs, vous devez utiliser l’[[!DNL Google Ads Query Builder]](https://developers.google.com/google-ads/api/fields/v17/overview_query_builder) .

Dans la [!DNL Google Ads Query Builder], accédez au type de ressource que vous souhaitez utiliser, puis utilisez le sélecteur d’attributs pour sélectionner vos attributs, segments et mesures.

![Sélecteur d’attributs dans le Query Builder Google Ads.](../../../../images/tutorials/create/ads/attributes.png)

Les attributs que vous sélectionnez renseignent le panneau [!DNL Google Ads Query Language]. Veillez à utiliser le mode [!DNL Standard], puis sélectionnez **[!DNL Enter or edit a query]**.

![Attributs sélectionnés, regroupés dans une requête.](../../../../images/tutorials/create/ads/enter-query.png)

Sélectionnez ensuite **[!DNL Validate Query]** pour valider votre requête [!DNL Google Ads].

![Programme de validation du Query Builder de Google Ads.](../../../../images/tutorials/create/ads/validate-query.png)

En cas de réussite, le [!DNL Google Ads Query Builder] renvoie un message indiquant que votre requête est valide. Copiez ensuite **uniquement les attributs** à partir de la requête.

![Requête validée avec succès.](../../../../images/tutorials/create/ads/copy-query.png)

Revenez à la phase de sélection des données du workflow des sources dans l’interface utilisateur d’Experience Platform, puis collez les attributs dans le panneau *[!UICONTROL Attributs de liste]*.

Sélectionnez **[!UICONTROL Aperçu]** pour prévisualiser les données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Panneau Attributs de liste dans le workflow des sources.](../../../../images/tutorials/create/ads/list-attributes.png)

## Créer un flux de données pour ingérer des données publicitaires

En suivant ce tutoriel, vous avez établi une connexion à votre compte Google Ads. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données publicitaires dans Experience Platform](../../dataflow/advertising.md).
