---
keywords: Experience Platform;accueil;rubriques les plus consultées;Oracle Service Cloud;oracle service cloud
title: Créer une connexion source Oracle Service Cloud dans l’interface utilisateur.
description: Découvrez comment créer une connexion source Oracle Service Cloud à l’aide de l’interface utilisateur d’Adobe Experience Platform.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 90%

---

# Créer une connexion source Oracle Service Cloud dans l’interface utilisateur.

>[!WARNING]
>
>La source [!DNL Oracle Service Cloud] sera abandonnée à la fin du mois de juin 2025.

Ce tutoriel décrit les étapes à suivre pour créer une connexion source Oracle Service Cloud à l’aide de l’interface utilisateur d’Adobe Experience Platform. 

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion à la source Oracle Service Cloud valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/customer-success.md)

### Collecter les informations d’identification requises

Pour accéder au compte Oracle Service Cloud sur [!DNL Experience Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Hôte | URL d’hôte de votre instance Oracle Service Cloud.  |
| Nom d’utilisateur | Nom d’utilisateur de votre compte d’utilisateur Oracle Service Cloud.  |
| Mot de passe | Mot de passe de votre compte Oracle Service Cloud.  |

Pour plus d’informations sur l’authentification de votre compte Oracle Service Cloud, reportez-vous au guide [[!DNL Oracle]  sur l’authentification](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html ).

## Se connecter à votre compte Oracle Service Cloud 

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pouvant être utilisées pour créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Succès clients], sélectionnez **[!UICONTROL Oracle Service Cloud]** puis sélectionnez **[!UICONTROL Ajouter des données]**. 

![Le catalogue des sources avec la source Oracle Service Cloud mise en surbrillance.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png) 

La page **[!UICONTROL Connexion à Oracle Service Cloud]** s’affiche.  Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Oracle Service Cloud auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer. 

![Interface du compte existant.](../../../../images/tutorials/create/oracle-service-cloud/existing.png) 

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification Oracle Service Cloud.  Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte avec des valeurs d’espace réservé pour.](../../../../images/tutorials/create/oracle-service-cloud/new.png) 

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte Oracle Service Cloud.  Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de succès client dans Experience Platform](../../dataflow/crm.md).
