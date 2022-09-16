---
keywords: Experience Platform;accueil;rubriques les plus consultées;onetrust;OneTrust
solution: Experience Platform
title: (Version bêta) Création d’une connexion à la source OneTrust dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source OneTrust à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 6768b772a983588b36659f42bff5c143a6f625f7
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 37%

---

# (Version bêta) Créez un [!DNL OneTrust Integration] connexion source dans l’interface utilisateur

>[!NOTE]
>
>Le [!DNL OneTrust Integration] La source est en version bêta. Ses fonctionnalités et sa documentation peuvent faire l’objet de modifications. Pour plus d’informations sur l’utilisation de sources marquées d’une version bêta, voir la section [présentation des sources](../../../../home.md#terms-and-conditions).

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
| Hôte | L’environnement à partir duquel la variable [!DNL OneTrust Integration] Les données doivent être extraites. | `https://uat.onetrust.com/` |
| URL de test d’autorisation | (Facultatif) L’URL du test d’autorisation est utilisée pour valider les informations d’identification lors de la création d’une connexion de base. Si elles ne sont pas fournies, les informations d’identification sont automatiquement vérifiées à l’étape de création de la connexion source. |  |
| Jeton d’accès | Le jeton d’accès qui correspond à votre [!DNL OneTrust Integration] compte . | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Pour plus d’informations sur ces informations d’identification, voir [[!DNL OneTrust Integration] documentation d’authentification](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Connecter votre compte [!DNL OneTrust Integration]

>[!NOTE]
>
>Le [!DNL OneTrust Integration] Les spécifications d’API sont partagées avec Adobe pour l’ingestion de données.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , *[!UICONTROL Consentement et préférences]* catégorie, sélectionnez [!DNL OneTrust Integration], puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/onetrust/catalog.png)

Le **[!UICONTROL Connexion au compte d’intégration OneTrust]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL OneTrust Integration] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/onetrust/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**, puis patientez quelques instants le temps que la nouvelle connexion sʼétablisse.

![nouveau](../../../../images/tutorials/create/onetrust/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL OneTrust Integration]. Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données de consentement dans Platform](../../dataflow/consent-and-preferences.md).
