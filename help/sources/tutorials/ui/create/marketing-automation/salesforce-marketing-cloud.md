---
title: Connexion de votre compte de Marketing Cloud Salesforce à un Experience Platform via l’interface utilisateur
description: Découvrez comment connecter votre compte de Marketing Cloud Salesforce à Experience Platform via l’interface utilisateur.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 27%

---

# Connectez-vous à [!DNL Salesforce Marketing Cloud] compte à Experience Platform via l’interface utilisateur

>[!IMPORTANT]
>
>L’ingestion d’objets personnalisés n’est actuellement pas prise en charge par la fonction [!DNL Salesforce Marketing Cloud] intégration de la source.


Ce tutoriel décrit les étapes à suivre pour connecter votre [!DNL Salesforce Marketing Cloud] compte vers Adobe Experience Platform via l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une [!DNL Salesforce Marketing Cloud] , vous pouvez ignorer le reste de ce document et passer au tutoriel sur [apport de données d’automatisation du marketing à Experience Platform à l’aide de l’interface utilisateur](../../dataflow/marketing-automation.md).

### Collecter les informations d’identification requises

Pour accéder au compte [!DNL Salesforce Marketing Cloud] sur Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Hôte | Serveur hôte de votre application. Il s’agit souvent de votre sous-domaine. **Remarque :** Lorsque vous saisissez votre `host` , il vous suffit de spécifier le sous-domaine et non l’URL entière. Par exemple, si l’URL d’hôte est `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, il vous suffit de saisir `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` comme valeur d’hôte. |
| Identifiant client | L’ID client associé à votre [!DNL Salesforce Marketing Cloud] application. |
| Secret client | Le secret client associé à votre [!DNL Salesforce Marketing Cloud] application. |

Pour plus d’informations sur l’authentification pour [!DNL Salesforce Marketing Cloud], rendez-vous sur la page [[!DNL Salesforce] documentation d’authentification](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Connecter votre compte [!DNL Salesforce Marketing Cloud]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Le [!UICONTROL Catalogue] affiche diverses sources prises en charge par Experience Platform.

Vous pouvez sélectionner la catégorie appropriée dans la liste des catégories. Vous pouvez également utiliser la barre de recherche pour filtrer une source spécifique.

Sous , [!UICONTROL Automatisation du marketing] catégorie, sélectionnez **[!UICONTROL Marketing Cloud Salesforce]** puis sélectionnez **[!UICONTROL Configuration]**.

![Catalogue des sources avec la source de Marketing Cloud Salesforce sélectionnée.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Le **[!UICONTROL Connexion au Marketing Cloud Salesforce]** s’affiche. Sur cette page, vous pouvez créer un compte ou utiliser un compte existant.

### Nouveau compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** et indiquez un nom pour votre compte, une description facultative et les informations d’authentification qui correspondent à votre [!DNL Salesforce Marketing Cloud] compte .

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte dans laquelle vous pouvez authentifier un nouveau compte pour le Marketing Cloud Salesforce.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Compte existant

Si vous disposez déjà d’un compte, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte à utiliser dans la liste qui s’affiche.

![Interface de compte existante dans laquelle vous pouvez sélectionner une liste de comptes de Marketing Cloud Salesforce existants.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion entre votre [!DNL Salesforce Marketing Cloud] et Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour importer vos données d’automatisation marketing dans Experience Platform ;](../../dataflow/marketing-automation.md).
