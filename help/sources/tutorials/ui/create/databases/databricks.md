---
title: Connecter des briques de données Azure à Experience Platform à l’aide de l’interface utilisateur
description: Découvrez comment connecter Azure Databricks à Experience Platform à l’aide de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
source-git-commit: 2bd16d5a55c5bbeedbc6a6012d9f0229eee8433a
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 8%

---

# Connexion d’[!DNL Azure Databricks] à Experience Platform dans l’interface utilisateur

>[!AVAILABILITY]
>
>* La source [!DNL Azure Databricks] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time CDP Ultimate.
>
>* La source [!DNL Azure Databricks] est en version Beta. Lisez les [termes et conditions](../../../../home.md#terms-and-conditions) dans la présentation des sources pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Lisez ce guide pour savoir comment connecter votre compte [!DNL Azure Databricks] à Adobe Experience Platform à l’aide de l’espace de travail des sources dans l’interface utilisateur.

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Collecter les informations d’identification requises

Fournissez des valeurs pour les informations d’identification suivantes afin de [!DNL Azure Databricks] connecter à Experience Platform.

| Informations d’identification | Description |
| --- | --- |
| Domaine | URL de votre espace de travail [!DNL Azure Databricks]. Par exemple : `https://adb-1234567890123456.7.azuredatabricks.net`. |
| Identifiant du cluster | L’identifiant de votre cluster dans [!DNL Azure Databricks]. Ce cluster doit déjà être un cluster existant et doit être un cluster interactif. |
| Jeton d’accès | Jeton d’accès qui authentifie votre compte [!DNL Azure Databricks]. Vous pouvez générer votre jeton d’accès à l’aide de l’espace de travail [!DNL Azure Databricks]. |
| Base de données | Nom de votre base de données dans le lac delta. |

Pour plus d’informations, consultez la [[!DNL Azure Databricks] présentation](../../../../connectors/databases/databricks.md).

## Parcourir le catalogue des sources

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]*. Choisissez une catégorie ou utilisez la barre de recherche pour trouver votre source.

Pour vous connecter à [!DNL Azure Databricks], accédez à la catégorie *[!UICONTROL Bases de données]*, sélectionnez la carte source **[!UICONTROL Azure Databricks]**, puis sélectionnez **[!UICONTROL Configurer]**.

>[!TIP]
>
>Les sources du catalogue affichent l’option **[!UICONTROL Configurer]** lorsqu’une source donnée ne dispose pas encore d’un compte authentifié. Une fois un compte authentifié créé, cette option devient **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources avec la carte source Azure Databricks sélectionnée.](../../../../images/tutorials/create/databricks/catalog.png)

### Utiliser un compte existant

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte [!DNL Azure Databricks] à utiliser.

![Interface des comptes existants dans le workflow des sources avec « Compte existant » sélectionné.](../../../../images/tutorials/create/databricks/existing.png)

### Créer un nouveau compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** puis indiquez un nom et éventuellement une description pour votre compte. Indiquez ensuite des valeurs pour les informations d’authentification suivantes :

* Domaine
* Identifiant du cluster
* Jeton d’accès
* Base de données

![Nouvelle interface de compte dans le workflow des sources avec un nom de compte et une description facultative fournis.](../../../../images/tutorials/create/databricks/new.png)

En outre, vous devez copier et coller vos informations d’identification [!UICONTROL URI SAS d’évaluation] dans votre environnement de [!DNL Azure Databricks]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** et patientez quelques instants le temps que la connexion s’établisse.

![Informations d’identification d’évaluation de l’URI SAS.](../../../../images/tutorials/create/databricks/sas-uri.png)

## Créer un flux de données pour les données [!DNL Azure Databricks]

Maintenant que vous avez correctement connecté votre compte [!DNL Azure Databricks], vous pouvez [créer un flux de données et ingérer les données de votre base de données dans Experience Platform](../../dataflow/databases.md).
