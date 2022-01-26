---
keywords: Experience Platform;accueil;rubriques les plus consultées;Snowflake
title: Création d’une connexion à la source du Snowflake dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source de Snowflake à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 0928da0ad15ce23d3677fec7b9866d079f3db407
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 7%

---

# Créez un [!DNL Snowflake] connexion source dans l’interface utilisateur

>[!NOTE]
>
> Le [!DNL Snowflake] Le connecteur est en version bêta. Voir [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs bêta-étiquetés.

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Snowflake] connecteur source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Collecte des informations d’identification requises

Pour accéder à votre compte de Snowflake sur [!DNL Platform], vous devez fournir la valeur d’authentification suivante :

| Credential | Description |
| ---------- | ----------- |
| Compte | Le nom complet du compte associé à votre [!DNL Snowflake] compte . Une personne entièrement qualifiée [!DNL Snowflake] nom du compte inclut le nom de votre compte, votre région et votre plateforme cloud. Par exemple : `cj12345.east-us-2.azure`. Pour plus d&#39;informations sur les noms de compte, reportez-vous à cette section [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Entrepôt | Le [!DNL Snowflake] l’entrepôt gère le processus d’exécution des requêtes de l’application. Chaque [!DNL Snowflake] L’entrepôt est indépendant l’un de l’autre et doit être accessible individuellement lors de l’importation de données vers Platform. |
| Base de données | Le [!DNL Snowflake] La base de données contient les données que vous souhaitez importer dans Platform. |
| Nom d’utilisateur | Nom d’utilisateur de la variable [!DNL Snowflake] compte . |
| Mot de passe | Le mot de passe du [!DNL Snowflake] compte utilisateur. |
| Chaîne de connexion | Chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Le modèle de chaîne de connexion pour [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

Pour plus d’informations sur ces valeurs, reportez-vous à la section [ce document Snowflake](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Connexion à votre compte Snowflake

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de la barre de recherche.

Sous , [!UICONTROL Bases de données] catégorie, sélectionnez **[!UICONTROL Snowflake]** puis sélectionnez **[!UICONTROL Ajouter des données]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

Le **[!UICONTROL Connexion à Snowflake]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Snowflake auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification de Snowflake. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![](../../../../images/tutorials/create/snowflake/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte de Snowflake. Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données dans [!DNL Platform]](../../dataflow/databases.md).
