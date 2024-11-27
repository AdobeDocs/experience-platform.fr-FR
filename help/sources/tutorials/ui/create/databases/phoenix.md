---
title: Connexion de votre compte Phoenix à l’aide de l’interface utilisateur Experience Platform
description: Découvrez comment connecter votre compte Phoenix et importer des données de votre base de données Phoenix vers Experience Platform à l’aide de l’interface utilisateur.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 21%

---

# Connectez votre compte [!DNL Phoenix] à un Experience Platform à l’aide de l’interface utilisateur

>[!WARNING]
>
>La source [!DNL Phoenix] sera abandonnée fin juin 2025.

Ce tutoriel décrit les étapes à suivre pour connecter votre compte [!DNL Phoenix] et importer des données de votre base de données [!DNL Phoenix] vers l’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL Phoenix] authentifié, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données pour une base de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder à votre compte [!DNL Phoenix] sur Experience Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| --- | --- |
| Hôte | Adresse IP ou nom d’hôte du serveur [!DNL Phoenix]. |
| Port | Port TCP utilisé par le serveur [!DNL Phoenix] pour écouter les connexions client. Si vous vous connectez à [!DNL Azure HDInsights], spécifiez le port 443. Si ce paramètre n’est pas fourni, la valeur par défaut est 8765. |
| Chemin HTTP | URL partielle correspondant au serveur [!DNL Phoenix]. Spécifiez /hbasephoenix0 si vous utilisez la grappe [!DNL Azure HDInsights]. |
| Nom d’utilisateur | Nom d’utilisateur que vous utilisez pour accéder au serveur [!DNL Phoenix]. |
| Mot de passe | Mot de passe qui correspond à l’utilisateur. |
| Enable SSL | Bascule qui spécifie si les connexions au serveur sont chiffrées à l’aide de SSL. |

Pour plus d&#39;informations sur la prise en main, consultez [ce [!DNL Phoenix] document](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour connecter votre compte [!DNL Phoenix] à Experience Platform.

## Connecter votre compte [!DNL Phoenix]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail des sources. L’écran *[!UICONTROL Catalogue]* affiche diverses sources disponibles dans le catalogue des sources Experience Platform.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver une source spécifique à l’aide de l’option de recherche.

Sélectionnez **[!UICONTROL Bases de données]** dans la liste des catégories de sources, puis **[!UICONTROL Ajouter des données]** dans la carte [!DNL Phoenix].

>[!TIP]
>
>Les sources du catalogue des sources peuvent afficher différentes invites selon l’état de la source.
> 
>* **[!UICONTROL Ajouter des données]** signifie qu’il existe des comptes authentifiés existants associés à la source sélectionnée.
>
>* **[!UICONTROL Configuration]** signifie que vous devez fournir des informations d’identification et authentifier un nouveau compte pour utiliser la source sélectionnée.

![Catalogue des sources sur l’interface utilisateur Experience Platform avec la carte source Phoenix sélectionnée.](../../../../images/tutorials/create/phoenix/catalog.png)

La page **[!UICONTROL Se connecter à Phoenix]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

>[!BEGINTABS]

>[!TAB Utiliser un compte Phoenix existant]

Pour utiliser un compte existant, sélectionnez [!UICONTROL Compte existant] , puis le compte à utiliser dans la liste qui s&#39;affiche. Lorsque vous avez terminé, sélectionnez [!UICONTROL Suivant] pour continuer.

![Liste des comptes de base de données Phoenix authentifiés qui existent déjà dans votre organisation.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Créer un compte Phoenix]

Pour utiliser un nouveau compte, sélectionnez [!UICONTROL Nouveau compte] et fournissez un nom, une description et vos informations d’authentification [!DNL Phoenix]. Lorsque vous avez terminé, sélectionnez [!UICONTROL Se connecter à la source] et attendez quelques secondes pour établir la nouvelle connexion.

![Nouvelle interface de compte dans laquelle vous pouvez fournir des informations d’authentification et créer un compte Phoenix.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Phoenix]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Experience Platform](../../dataflow/databases.md).
