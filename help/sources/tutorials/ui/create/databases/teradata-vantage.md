---
keywords: Experience Platform;accueil;rubriques les plus consultées;Teradata Vantage
title: Création d’une connexion à la source de l’offre Teradata dans l’interface utilisateur
description: Découvrez comment créer une connexion source Teradata Vantage à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 625a7959f48a0b16c3228d4555e046b5f67c51b7
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 32%

---

# Créer une connexion source [!DNL Teradata Vantage] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Teradata Vantage] connecteur source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de Platform :

* [Sources](../../../../home.md): Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Collecter les informations d’identification requises

Pour accéder à [!DNL Teradata Vantage] sur Platform, vous devez fournir la valeur d’authentification suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| Chaîne de connexion | Une chaîne de connexion est une chaîne qui fournit des informations sur une source de données et sur la manière dont vous pouvez vous y connecter. Le modèle de chaîne de connexion pour [!DNL Teradata Vantage] is `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Pour plus d’informations sur la prise en main, reportez-vous à cette section [[!DNL Teradata Vantage] document](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Connecter votre compte [!DNL Teradata Vantage]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , [!UICONTROL Bases de données] catégorie, sélectionnez **[!UICONTROL Teradata Vantage]** puis sélectionnez **[!UICONTROL Configuration]**.

>[!TIP]
>
>Les sources dans le catalogue des sources affichent la variable **[!UICONTROL Configuration]** lorsqu’une source donnée ne dispose pas encore d’un compte authentifié. Une fois qu’un compte authentifié existe, cette option devient **[!UICONTROL Ajouter des données]**.

![Catalogue des sources avec la source Vantage en Teradata sélectionnée.](../../../../images/tutorials/create/teradata/catalog.png)

La variable **[!UICONTROL Connexion à Teradata Vantage]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Teradata Vantage] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Page des comptes existants dans l’espace de travail des sources.](../../../../images/tutorials/create/teradata/existing.png)

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et votre [!DNL Teradata Vantage] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![Nouvelle interface de création de compte dans l’espace de travail des sources.](../../../../images/tutorials/create/teradata/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte Teradata Vantage. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/databases.md).
