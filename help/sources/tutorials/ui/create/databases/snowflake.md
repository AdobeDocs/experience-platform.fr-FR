---
title: Création d’une connexion source Snowflake dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source de Snowflake à l’aide de l’interface utilisateur de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 17%

---

# Créer une connexion source [!DNL Snowflake] dans l’interface utilisateur

>[!IMPORTANT]
>
>La variable [!DNL Snowflake] source est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-time Customer Data Platform Ultimate.

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Snowflake] connecteur source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [Sources ](../../../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Collecter les informations d’identification requises

Vous devez fournir des valeurs pour les propriétés d’identification suivantes afin d’authentifier votre [!DNL Snowflake] source.

>[!BEGINTABS]

>[!TAB Authentification par clé de compte]

| Informations d’identification | Description |
| ---------- | ----------- |
| Compte | Un nom de compte identifie de manière unique un compte au sein de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte parmi différents [!DNL Snowflake] organisations. Pour ce faire, vous devez ajouter le nom de votre organisation en préfixe sur le nom du compte. Par exemple :`orgname-account_name` Pour plus d’informations sur les noms de compte, consultez la section [!DNL Snowflake] documentation sur [identificateurs de compte](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Entrepôt | La variable [!DNL Snowflake] l’entrepôt gère le processus d’exécution des requêtes de l’application. Chaque [!DNL Snowflake] L’entrepôt est indépendant l’un de l’autre et doit être accessible individuellement lors de l’importation de données vers Platform. |
| Base de données | La variable [!DNL Snowflake] La base de données contient les données que vous souhaitez importer dans Platform. |
| Nom d’utilisateur | Nom d’utilisateur de la variable [!DNL Snowflake] compte . |
| Mot de passe | Le mot de passe du [!DNL Snowflake] compte utilisateur. |
| Rôle | Le rôle de contrôle d’accès par défaut à utiliser dans la variable [!DNL Snowflake] session. Le rôle doit être un rôle existant qui a déjà été attribué à l’utilisateur spécifié. Le rôle par défaut est `PUBLIC`. |
| Chaîne de connexion | Chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Le modèle de chaîne de connexion pour [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Authentification par paire de clés]

Pour utiliser l’authentification par paire de clés, vous devez générer une paire de clés RSA 2 048 bits, puis fournir les valeurs suivantes lors de la création d’un compte pour votre [!DNL Snowflake] source.

| Informations d’identification | Description |
| --- | --- |
| Compte | Un nom de compte identifie de manière unique un compte au sein de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte parmi différents [!DNL Snowflake] organisations. Pour ce faire, vous devez ajouter le nom de votre organisation en préfixe sur le nom du compte. Par exemple :`orgname-account_name` Pour plus d’informations sur les noms de compte, consultez la section [!DNL Snowflake] documentation sur [identificateurs de compte](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Nom d’utilisateur | Le nom d’utilisateur de votre [!DNL Snowflake] compte . |
| Clé privée | La variable [!DNL Base64-]clé privée codée de votre [!DNL Snowflake] compte . Vous pouvez générer des clés privées chiffrées ou non chiffrées. Si vous utilisez une clé privée chiffrée, vous devez également fournir un mot de passe de clé privée lors de l’authentification par rapport à un Experience Platform. |
| Passphrase de clé privée | La phrase secrète de clé privée est une couche supplémentaire de sécurité que vous devez utiliser lors de l’authentification avec une clé privée chiffrée. Vous n’êtes pas tenu de fournir la phrase secrète si vous utilisez une clé privée non chiffrée. |
| Base de données | La variable [!DNL Snowflake] base de données contenant les données que vous souhaitez ingérer à Experience Platform. |
| Entrepôt | La variable [!DNL Snowflake] l’entrepôt gère le processus d’exécution des requêtes de l’application. Chaque [!DNL Snowflake] L’entrepôt est indépendant l’un de l’autre et doit être accessible individuellement lors de l’importation de données vers Platform. |

Pour plus d’informations sur ces valeurs, voir [ce document Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

Pour accéder à votre compte de Snowflake sur Experience Platform, vous devez fournir la valeur d’authentification suivante :

>[!NOTE]
>
>Vous devez définir la variable `PREVENT_UNLOAD_TO_INLINE_URL` indicateur pour `FALSE` pour permettre le déchargement des données de votre [!DNL Snowflake] base de données vers Experience Platform.

## Connexion à votre compte Snowflake

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] workspace.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Sous , [!UICONTROL Bases de données] catégorie, sélectionnez **[!UICONTROL Snowflake]** puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources avec [!DNL Snowflake] surlignée.](../../../../images/tutorials/create/snowflake/catalog.png)

La variable **[!UICONTROL Connexion à Snowflake]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez la variable [!DNL Snowflake] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Interface du compte existant dans le workflow des sources.](../../../../images/tutorials/create/snowflake/existing.png)

### Nouveau compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative de votre nouvelle [!DNL Snowflake] compte .

![Nouvelle interface de compte dans le workflow des sources.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Authentification par clé de compte]

Pour utiliser l’authentification par clé de compte, indiquez votre chaîne de connexion dans le formulaire de saisie, puis sélectionnez **[!UICONTROL Connexion à la source]**.

![Interface d’authentification de la clé de compte.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Authentification par paire de clés]

Pour utiliser l’authentification par paire de clés, indiquez les valeurs de votre compte, nom d’utilisateur, clé privée, mot de passe de clé privée, base de données et entrepôt, puis sélectionnez **[!UICONTROL Connexion à la source]**.

![Interface d’authentification de paire de clés de compte.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte de Snowflake. Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données [!DNL Platform]](../../dataflow/databases.md).
