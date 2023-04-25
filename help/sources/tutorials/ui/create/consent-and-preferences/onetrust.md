---
keywords: Experience Platform;accueil;rubriques les plus consultées;onetrust;OneTrust
solution: Experience Platform
title: Création d’une connexion à la source OneTrust dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source OneTrust à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 26%

---

# Créer une connexion source [!DNL OneTrust Integration] dans l’interface utilisateur

>[!NOTE]
>
>Le [!DNL OneTrust Integration] source ne prend en charge que l’ingestion des données de consentement et de préférences, et non les cookies.

Ce tutoriel décrit les étapes à suivre pour créer une [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) connexion source pour ingérer des données de consentement historiques et planifiées dans Adobe Experience Platform à l’aide de l’interface utilisateur de Platform.

## Conditions préalables

>[!IMPORTANT]
>
>Le [!DNL OneTrust Integration] le connecteur source et la documentation ont été créés par [!DNL OneTrust Integration] l&#39;équipe. Pour toute question ou demande de mise à jour, veuillez contacter la [[!DNL OneTrust] équipe](https://my.onetrust.com/s/contactsupport?language=en_US) directement.

Avant de vous connecter [!DNL OneTrust Integration] sur Platform, vous devez d’abord récupérer votre jeton d’accès. Pour obtenir des instructions détaillées sur la recherche de votre jeton d’accès, reportez-vous à la section [[!DNL OneTrust Integration] Guide OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Le jeton d’accès n’est pas actualisé automatiquement après son expiration, car les jetons d’actualisation système à système ne sont pas pris en charge par [!DNL OneTrust]. Par conséquent, il est nécessaire de s’assurer que votre jeton d’accès est mis à jour dans la connexion avant son expiration. La durée de vie maximale configurable d’un jeton d’accès est d’un an. Pour en savoir plus sur la mise à jour de votre jeton d’accès, reportez-vous à la section [[!DNL OneTrust] document sur la gestion de vos informations d’identification client OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Collecter les informations d’identification requises

Pour vous connecter [!DNL OneTrust Integration] sur Platform, vous devez fournir des valeurs pour les informations d’authentification suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Nom de l’hôte. | L’environnement à partir duquel la variable [!DNL OneTrust Integration] Les données doivent être extraites. | `app.onetrust.com` |
| URL de test d’autorisation | (Facultatif) L’URL du test d’autorisation est utilisée pour valider les informations d’identification lors de la création d’une connexion de base. Si elles ne sont pas fournies, les informations d’identification sont automatiquement vérifiées à l’étape de création de la connexion source. |  |
| Jeton d’accès | Le jeton d’accès qui correspond à votre [!DNL OneTrust Integration] compte . | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Pour plus d’informations sur ces informations d’identification, voir [[!DNL OneTrust Integration] documentation d’authentification](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Connecter votre compte [!DNL OneTrust Integration]

>[!NOTE]
>
>Le [!DNL OneTrust Integration] Les spécifications d’API sont partagées avec Adobe pour l’ingestion de données.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] espace de travail pour un catalogue de sources disponible dans Experience Platform.

Utilisez la variable *[!UICONTROL Catégories]* pour filtrer les sources par catégorie. Vous pouvez également saisir un nom de source dans la barre de recherche pour trouver une source spécifique dans le catalogue.

Accédez au [!UICONTROL Consentement et préférences] de la catégorie [!DNL OneTrust Integration] carte source. Pour commencer, sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue des sources de l’interface utilisateur Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

Le **[!UICONTROL Connexion au compte d’intégration OneTrust]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL OneTrust Integration] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![L’étape d’authentification du compte existant dans le workflow des sources.](../../../../images/tutorials/create/onetrust/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle étape d’authentification du compte dans le workflow des sources.](../../../../images/tutorials/create/onetrust/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL OneTrust Integration]. Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données de consentement dans Platform](../../dataflow/consent-and-preferences.md).
