---
title: Connexion de votre compte Phoenix à l’aide de l’interface utilisateur Experience Platform
description: Découvrez comment connecter votre compte Phoenix et importer des données de votre base de données Phoenix vers Experience Platform à l’aide de l’interface utilisateur.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 25%

---

# Connectez-vous à [!DNL Phoenix] compte à Experience Platform à l’aide de l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour connecter votre [!DNL Phoenix] et d’importer des données de votre [!DNL Phoenix] base de données vers Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une authentification [!DNL Phoenix] , vous pouvez ensuite ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données pour une base de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder à [!DNL Phoenix] sur Experience Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| --- | --- |
| Hôte | L’adresse IP ou le nom d’hôte de la variable [!DNL Phoenix] serveur. |
| Port | Le port TCP que la variable [!DNL Phoenix] Le serveur utilise pour écouter les connexions client. Si vous vous connectez à [!DNL Azure HDInsights], puis spécifiez le port 443. Si ce paramètre n’est pas fourni, la valeur par défaut est 8765. |
| Chemin HTTP | L’URL partielle correspondant au [!DNL Phoenix] serveur. Spécifiez /hbasephoenix0 si vous utilisez le paramètre [!DNL Azure HDInsights] grappe. |
| Nom d’utilisateur | Le nom d’utilisateur que vous utilisez pour accéder à la variable [!DNL Phoenix] serveur. |
| Mot de passe | Mot de passe qui correspond à l’utilisateur. |
| Enable SSL | Bascule qui spécifie si les connexions au serveur sont chiffrées à l’aide de SSL. |

Pour plus d’informations sur la prise en main, voir [this [!DNL Phoenix] document](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour connecter votre [!DNL Phoenix] compte à Experience Platform.

## Connecter votre compte [!DNL Phoenix]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail des sources. La variable *[!UICONTROL Catalogue]* écran affiche diverses sources disponibles dans le catalogue des sources Experience Platform.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver une source spécifique à l’aide de l’option de recherche.

Sélectionner **[!UICONTROL Bases de données]** dans la liste des catégories de sources, puis sélectionnez **[!UICONTROL Ajouter des données]** de la [!DNL Phoenix] carte.

>[!TIP]
>
>Les sources du catalogue des sources peuvent afficher différentes invites selon l’état de la source.
> 
>* **[!UICONTROL Ajouter des données]** signifie qu’il existe des comptes authentifiés existants associés à la source sélectionnée.
>
>* **[!UICONTROL Configuration]** signifie que vous devez fournir des informations d’identification et authentifier un nouveau compte pour utiliser la source sélectionnée.

![Catalogue des sources sur l’interface utilisateur de l’Experience Platform avec la carte source Phoenix sélectionnée.](../../../../images/tutorials/create/phoenix/catalog.png)

La variable **[!UICONTROL Connexion à Phoenix]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

>[!BEGINTABS]

>[!TAB Utiliser un compte Phoenix existant]

Pour utiliser un compte existant, sélectionnez [!UICONTROL Compte existant] puis sélectionnez le compte à utiliser dans la liste qui s’affiche. Lorsque vous avez terminé, sélectionnez [!UICONTROL Suivant] pour continuer.

![Liste des comptes de base de données Phoenix authentifiés qui existent déjà dans votre organisation.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Créer un compte Phoenix]

Pour utiliser un nouveau compte, sélectionnez [!UICONTROL Nouveau compte] et indiquez un nom, une description et votre [!DNL Phoenix] informations d’identification d’authentification. Lorsque vous avez terminé, sélectionnez [!UICONTROL Connexion à la source] et attendez quelques secondes pour que la nouvelle connexion soit établie.

![Nouvelle interface de compte dans laquelle vous pouvez fournir des informations d’authentification et créer un compte Phoenix.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Phoenix]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Experience Platform](../../dataflow/databases.md).
