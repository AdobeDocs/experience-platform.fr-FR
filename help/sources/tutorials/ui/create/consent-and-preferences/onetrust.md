---
keywords: Experience Platform;accueil;rubriques populaires;onetrust;OneTrust
solution: Experience Platform
title: Créer une connexion Source OneTrust dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source OneTrust à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 23%

---

# Créer une connexion source [!DNL OneTrust Integration] dans l’interface utilisateur

>[!NOTE]
>
>La source [!DNL OneTrust Integration] prend uniquement en charge l’ingestion des données de consentement et de préférences, et non des cookies.

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) afin d’ingérer aussi bien les données de consentement historiques que les données de consentement planifiées dans Adobe Experience Platform à l’aide de l’interface utilisateur d’Experience Platform.

## Conditions préalables

>[!IMPORTANT]
>
>Le connecteur source [!DNL OneTrust Integration] et la documentation ont été créés par l’équipe [!DNL OneTrust Integration]. Pour toute demande ou information, contactez directement l&#39;[[!DNL OneTrust] équipe](https://my.onetrust.com/s/contactsupport?language=en_US).

Avant de pouvoir connecter [!DNL OneTrust Integration] à Experience Platform, vous devez d’abord récupérer votre jeton d’accès. Pour obtenir des instructions détaillées sur la recherche de votre jeton d’accès, consultez le guide [[!DNL OneTrust Integration] OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Le jeton d’accès ne s’actualise pas automatiquement après son expiration, car les jetons d’actualisation système à système ne sont pas pris en charge par [!DNL OneTrust]. Par conséquent, il est nécessaire de s’assurer que votre jeton d’accès est mis à jour dans la connexion avant son expiration. La durée de vie configurable maximale d’un jeton d’accès est d’un an. Pour en savoir plus sur la mise à jour de votre jeton d’accès, consultez le document [[!DNL OneTrust]  sur la gestion des informations d’identification de votre client OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Collecter les informations d’identification requises

Pour connecter [!DNL OneTrust Integration] à Experience Platform, vous devez fournir des valeurs pour les informations d’authentification suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Nom de l’hôte | Environnement à partir duquel les données [!DNL OneTrust Integration] doivent être extraites. | `app.onetrust.com` |
| URL du test d’autorisation | (Facultatif) L’URL du test d’autorisation est utilisée pour valider les informations d’identification lors de la création d’une connexion de base. Si elles ne sont pas fournies, les informations d’identification sont automatiquement vérifiées à l’étape de création de la connexion source. | |
| Jeton d’accès | Jeton d’accès correspondant à votre compte [!DNL OneTrust Integration]. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Pour plus d’informations sur ces informations d’identification, consultez la [[!DNL OneTrust Integration] documentation d’authentification](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Connecter votre compte [!DNL OneTrust Integration]

>[!NOTE]
>
>Les spécifications de l’API [!DNL OneTrust Integration] sont partagées avec Adobe pour l’ingestion de données.

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources] pour un catalogue de sources disponibles dans Experience Platform.

Utilisez le menu *[!UICONTROL Catégories]* pour filtrer les sources par catégorie. Vous pouvez également saisir un nom de source dans la barre de recherche pour trouver une source spécifique à partir du catalogue.

Accédez à la catégorie [!UICONTROL Consentement et préférences] pour la carte source [!DNL OneTrust Integration]. Pour commencer, sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources de l’interface utilisateur d’Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

La page **[!UICONTROL Connecter le compte d’intégration OneTrust]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL OneTrust Integration] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Étape d’authentification du compte existant dans le workflow des sources.](../../../../images/tutorials/create/onetrust/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![L’étape d’authentification du nouveau compte dans le workflow des sources.](../../../../images/tutorials/create/onetrust/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL OneTrust Integration]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de consentement dans Experience Platform](../../dataflow/consent-and-preferences.md).
