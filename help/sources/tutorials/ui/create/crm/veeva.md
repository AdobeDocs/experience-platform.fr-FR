---
keywords: Experience Platform;accueil;rubriques les plus consultées;Veeva CRM;veeva
solution: Experience Platform
title: Création d’une connexion Source CRM Veeva dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source CRM Veeva à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 79%

---

# Créer une connexion source [!DNL Veeva CRM] dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’ingérer des données CRM externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL Veeva CRM] à l’aide de l’interface utilisateur de [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL Veeva CRM], vous pouvez ignorer le reste de ce document et passer au tutoriel expliquant comment [Configurer un flux de données](../../dataflow/crm.md).

### Collecter les informations d’identification requises

| Informations d’identification | Description |
| ---------- | ----------- |
| `environmentUrl` | URL de l’instance source [!DNL Veeva CRM]. |
| `username` | Nom d’utilisateur du compte utilisateur [!DNL Veeva CRM]. |
| `password` | Mot de passe du compte utilisateur [!DNL Veeva CRM]. |
| `securityToken` | Jeton de sécurité pour le compte utilisateur [!DNL Veeva CRM]. |

Pour plus d&#39;informations sur la prise en main, consultez ce [[!DNL Veeva CRM] document](https://developer.veevacrm.com/doc/Content/rest-api.htm).

## Connecter votre compte [!DNL Veeva CRM]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Veeva CRM] à [!DNL Platform].

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie [!UICONTROL CRM], sélectionnez **[!UICONTROL Veeva CRM]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/veeva/catalog.png)

La page **[!UICONTROL Connecter le compte CRM Veeva]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Veeva CRM] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/veeva/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification [!DNL Veeva CRM]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![nouveau](../../../../images/tutorials/create/veeva/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Veeva CRM]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/crm.md).
