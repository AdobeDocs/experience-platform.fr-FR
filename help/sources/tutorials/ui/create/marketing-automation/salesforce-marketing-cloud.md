---
title: Connexion de votre compte Salesforce Marketing Cloud à Experience Platform via l’interface utilisateur
description: Découvrez comment connecter votre compte Salesforce Marketing Cloud à Experience Platform via l’interface utilisateur.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 21%

---

# Connecter votre compte [!DNL Salesforce Marketing Cloud] à Experience Platform via l’interface utilisateur

>[!WARNING]
>
>La source [!DNL Salesforce Marketing Cloud] sera abandonnée à la fin du mois de juin 2025.

Ce tutoriel décrit les étapes à suivre pour connecter votre compte [!DNL Salesforce Marketing Cloud] à Adobe Experience Platform via l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL Salesforce Marketing Cloud], vous pouvez ignorer le reste de ce document et passer au tutoriel sur [l’importation de données d’automatisation du marketing dans Experience Platform à l’aide de l’interface utilisateur](../../dataflow/marketing-automation.md).

### Collecter les informations d’identification requises

Pour accéder au compte [!DNL Salesforce Marketing Cloud] sur Experience Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Hôte | Serveur hôte de votre application. Il s’agit souvent de votre sous-domaine. **Remarque :** lors de la saisie de votre valeur de `host`, vous devez spécifier la `{subdomain}.rest.marketingcloudapis.com`. Par exemple, si votre URL hôte est `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, vous devez saisir `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` comme valeur d’hôte. |
| Identifiant client | Identifiant client associé à votre application [!DNL Salesforce Marketing Cloud]. |
| Secret client | Secret client associé à votre application [!DNL Salesforce Marketing Cloud]. |

Pour plus d’informations sur l’authentification pour [!DNL Salesforce Marketing Cloud], consultez la [[!DNL Salesforce] documentation d’authentification](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Connecter votre compte [!DNL Salesforce Marketing Cloud]

>[!IMPORTANT]
>
>L’ingestion d’objets personnalisés n’est actuellement pas prise en charge par l’intégration source [!DNL Salesforce Marketing Cloud].

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Le [!UICONTROL Catalogue] affiche diverses sources prises en charge par Experience Platform.

Vous pouvez sélectionner la catégorie appropriée dans la liste des catégories. Vous pouvez également utiliser la barre de recherche pour filtrer une source spécifique.

Dans la catégorie [!UICONTROL Automatisation du marketing], sélectionnez **[!UICONTROL Salesforce Marketing Cloud]** puis **[!UICONTROL Configurer]**.

![Le catalogue des sources avec la source Salesforce Marketing Cloud sélectionnée.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

La page **[!UICONTROL Connexion à Salesforce Marketing Cloud]** s’affiche. Sur cette page, vous pouvez créer un compte ou utiliser un compte existant.

### Nouveau compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** et indiquez un nom de compte, une description facultative et les informations d’authentification qui correspondent à votre compte [!DNL Salesforce Marketing Cloud].

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte dans laquelle vous pouvez authentifier un nouveau compte pour Salesforce Marketing Cloud.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Compte existant

Si vous disposez déjà d’un compte, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte à utiliser dans la liste qui s’affiche.

![Interface du compte existant dans laquelle vous pouvez effectuer une sélection dans une liste de comptes Salesforce Marketing Cloud existants.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion entre votre compte [!DNL Salesforce Marketing Cloud] et Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour importer vos données d’automatisation du marketing dans Experience Platform](../../dataflow/marketing-automation.md).
