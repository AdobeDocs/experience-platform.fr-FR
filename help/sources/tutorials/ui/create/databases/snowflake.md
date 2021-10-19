---
keywords: Experience Platform ; accueil ; sujets populaires ; Snowflake
title: Création d’une connexion source Snowflake dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Snowflake à l’aide de l’interface utilisateur Adobe Experience Platform.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 76b3e3e9bcb27eb2bd6981ae6eb109410ae16336
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 7%

---

# Créer un [!DNL Snowflake] connexion source dans l’interface utilisateur

>[!NOTE]
>
> Le [!DNL Snowflake] est en version bêta. Voir la section [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés bêta.

Ce tutoriel explique comment créer une [!DNL Snowflake] connecteur source à l’aide de l’interface utilisateur Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de la plate-forme :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, étiqueter et améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Collecte des informations d’identification requises

Pour accéder à votre compte de Snowflake sur [!DNL Platform], vous devez fournir la valeur d’authentification suivante :

| Informations d&#39;identification | Description |
| ---------- | ----------- |
| Compte | Le nom complet du compte associé à votre [!DNL Snowflake] compte. Une personne pleinement qualifiée [!DNL Snowflake] le nom de compte comprend votre nom de compte, votre région et votre plate-forme cloud. Par exemple : `cj12345.east-us-2.azure`. Pour plus d’informations sur les noms de compte, reportez-vous à [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Entrepôt | Le [!DNL Snowflake] l&#39;entrepôt gère le processus d&#39;exécution de la requête pour l&#39;application. Chacune [!DNL Snowflake] l&#39;entrepôt est indépendant l&#39;un de l&#39;autre et doit être accessible individuellement lors de l&#39;importation de données vers la plate-forme. |
| Base de données | Le [!DNL Snowflake] contient les données que vous souhaitez importer dans la plate-forme. |
| Nom d’utilisateur | Le nom d’utilisateur du [!DNL Snowflake] compte. |
| Mot de passe | Le mot de passe pour le [!DNL Snowflake] compte utilisateur. |
| Chaîne de connexion | La chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Modèle de chaîne de connexion pour [!DNL Snowflake] est `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

Pour plus d’informations sur ces valeurs, voir [ce document Snowflake](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Connexion de votre compte de Snowflake

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Sources]** à partir de la navigation de gauche pour accéder à la [!UICONTROL Sources] espace de travail. Le [!UICONTROL Catalogue] affiche une variété de sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de la barre de recherche.

Sous [!UICONTROL Bases de données] catégorie, sélectionnez **[!UICONTROL Snowflake]** puis sélectionnez **[!UICONTROL Ajout de données]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

Le **[!UICONTROL Se connecter au Snowflake]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte de Snowflake avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Sur le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification de Snowflake. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis laissez un certain temps pour que la nouvelle connexion s&#39;établisse.

![](../../../../images/tutorials/create/snowflake/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte de Snowflake. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Platform]](../../dataflow/databases.md).
