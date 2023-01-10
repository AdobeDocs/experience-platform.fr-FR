---
keywords: Experience Platform;accueil;rubriques les plus consultées;Salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Création d’une connexion source de Marketing Cloud Salesforce dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source de Marketing Cloud Salesforce à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 49%

---

# Créer une connexion source [!DNL Salesforce Marketing Cloud] dans l’interface utilisateur

>[!NOTE]
>
> La source [!DNL Salesforce Marketing Cloud] est en version Beta. Voir la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta. 

Les connecteurs source d’Adobe Experience Platform permettent d’ingérer des données externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Salesforce Marketing Cloud] connecteur source à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une [!DNL Salesforce Marketing Cloud] vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données](../../dataflow/marketing-automation.md).

### Collecter les informations d’identification requises

Pour accéder au compte [!DNL Salesforce Marketing Cloud] sur Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Serveur hôte de votre application. Il s’agit souvent de votre sous-domaine. **Remarque :** Lorsque vous saisissez votre `host` , il vous suffit de spécifier le sous-domaine et non l’URL entière. Par exemple, si l’URL d’hôte est `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, il vous suffit de saisir `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` comme valeur d’hôte. |
| `clientId` | L’ID client associé à votre [!DNL Salesforce Marketing Cloud] application. |
| `clientSecret` | Le secret client associé à votre [!DNL Salesforce Marketing Cloud] application. |

Pour plus d’informations sur la prise en main, reportez-vous à cette section [[!DNL Salesforce Marketing Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Connecter votre compte [!DNL Salesforce Marketing Cloud]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL Salesforce Marketing Cloud] à Platform.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également utiliser la barre de recherche pour affiner les connecteurs affichés.

Sous , [!UICONTROL Automatisation du marketing] catégorie, sélectionnez **[!UICONTROL Marketing Cloud Salesforce]** puis sélectionnez **[!UICONTROL Configuration]**.

![catalogue](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Le **[!UICONTROL Connexion au Marketing Cloud Salesforce]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et [!DNL Salesforce Marketing Cloud] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![nouveau](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Salesforce Marketing Cloud] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Salesforce Marketing Cloud]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données du système d’automatisation du marketing dans Platform ;](../../dataflow/marketing-automation.md).
