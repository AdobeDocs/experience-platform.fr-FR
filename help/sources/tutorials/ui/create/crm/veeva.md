---
keywords: Experience Platform;accueil;rubriques les plus consultées;Veeva CRM;veeva
solution: Experience Platform
title: Création d’une connexion source CRM Veeva dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source CRM Veeva à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 076e0880c9efd1fe1cbfb4c610c5e15093adf460
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 13%

---

# Création d’une connexion source [!DNL Veeva CRM] dans l’interface utilisateur

Les connecteurs source de Adobe Experience Platform permettent d’ingérer des données CRM externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL Veeva CRM] à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL Veeva CRM] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/crm.md).

### Collecte des informations d’identification requises

| Credential | Description |
| ---------- | ----------- |
| `environmentUrl` | URL de l’instance source [!DNL Veeva CRM]. |
| `username` | Nom d’utilisateur du compte utilisateur [!DNL Veeva CRM]. |
| `password` | Mot de passe du compte utilisateur [!DNL Veeva CRM]. |
| `securityToken` | Jeton de sécurité pour le compte utilisateur [!DNL Veeva CRM]. |

Pour plus d’informations sur la prise en main, reportez-vous à [ce document de Veeva CRM]

## Connectez votre compte [!DNL Veeva CRM]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Veeva CRM] à [!DNL Platform].

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie [!UICONTROL CRM], sélectionnez **[!UICONTROL Veeva CRM]**, puis **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/veeva/catalog.png)

La page **[!UICONTROL Connecter le compte CRM Veeva]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Veeva CRM] avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/veeva/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification [!DNL Veeva CRM]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]**, puis laissez un certain temps pour établir la nouvelle connexion.

![new](../../../../images/tutorials/create/veeva/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Veeva CRM]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/crm.md).
