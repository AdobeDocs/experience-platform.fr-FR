---
keywords: Experience Platform ; accueil ; rubriques populaires ; Microsoft SQL Server ; SQL Server ; sql server
solution: Experience Platform
title: Création d’une connexion à la source Microsoft SQL Server dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Microsoft SQL Server à l’aide de l’interface utilisateur Adobe Experience Platform.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 12%

---

# Créer une connexion source [!DNL Microsoft SQL Server] dans l’interface utilisateur

>[!NOTE]
>
> Le connecteur [!DNL Microsoft SQL Server] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Microsoft SQL Server] (ci-après dénommé &quot;[!DNL SQL Server]&quot;) à l&#39;aide de l&#39;interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;une connexion [!DNL SQL Server] valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour vous connecter à [!DNL SQL Server] sur [!DNL Platform], vous devez fournir la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion associée à votre compte [!DNL SQL Server]. Le modèle de chaîne de connexion [!DNL SQL Server] est le suivant : `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |

Pour plus d&#39;informations sur la prise en main, consultez [ce [!DNL SQL Server] document](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Connectez votre compte [!DNL SQL Server]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL SQL Server] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Microsoft SQL Server]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un connecteur [!DNL SQL Server].

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

La page **[!UICONTROL Se connecter à Microsoft SQL Server]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL SQL Server]. Une fois terminé, sélectionnez **[!UICONTROL Se connecter]**, puis accordez un certain temps à la nouvelle connexion pour établir.

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL SQL Server] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte [!DNL SQL Server]. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans  [!DNL Platform]](../../dataflow/databases.md).
