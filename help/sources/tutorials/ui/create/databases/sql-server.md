---
title: Création d’une connexion source Microsoft SQL Server dans l’interface utilisateur
description: Découvrez comment créer une connexion source Microsoft SQL Server à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 45%

---

# Créer une connexion source [!DNL Microsoft SQL Server] dans l’interface utilisateur

Lisez ce tutoriel pour apprendre à connecter votre [!DNL Microsoft SQL Server] à Adobe Experience Platform à l’aide de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL SQL Server] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour vous connecter à [!DNL SQL Server] on [!DNL Platform], vous devez fournir la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| Chaîne de connexion | La chaîne de connexion associée à votre [!DNL Microsoft SQL Server] compte . Le modèle de chaîne de connexion varie selon que vous utilisez le nom de serveur ou d’instance pour votre source de données :<ul><li>Chaîne de connexion utilisant le nom du serveur : `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Chaîne de connexion utilisant le nom de l’instance :`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

Pour plus d’informations sur la prise en main, voir [this [!DNL SQL Server] document](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Connecter votre compte [!DNL SQL Server]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , *Bases de données* catégorie, sélectionnez **[!DNL Microsoft SQL Server]**, puis sélectionnez **[!UICONTROL Configuration]**.

>[!TIP]
>
>Les sources dans le catalogue des sources affichent la variable **[!UICONTROL Configuration]** lorsqu’une source donnée ne dispose pas encore d’un compte authentifié. Une fois qu’un compte authentifié existe, cette option devient **[!UICONTROL Ajouter des données]**.

![Catalogue des sources avec la source SQL Server Microsoft sélectionnée.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

La variable **[!UICONTROL Connexion à Microsoft SQL Server]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

>[!BEGINTABS]

>[!TAB Création d’un compte]

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** et indiquez un nom, une description facultative et vos informations d’identification.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![La nouvelle interface du compte avec les détails de connexion source saisis et mis en surbrillance.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Utiliser un compte existant]

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte à utiliser dans le catalogue de comptes existant.

Cliquez sur **[!UICONTROL Suivant]** pour continuer.

![Interface du compte existant qui affiche la liste des comptes existants.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL SQL Server]. Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données [!DNL Platform]](../../dataflow/databases.md).
