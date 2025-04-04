---
keywords: Experience Platform;accueil;rubriques populaires;paypal;Paypal
solution: Experience Platform
title: Créer une connexion Source PayPal dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source PayPal à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 38%

---

# Créer une connexion source [!DNL PayPal] dans l’interface utilisateur

>[!WARNING]
>
>La source [!DNL PayPal] sera abandonnée à la fin du mois de juin 2025.

Les connecteurs Source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL PayPal] à l’aide de l’interface utilisateur d’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL PayPal] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur [la configuration d’un flux de données](../../dataflow/payments.md)

### Collecter les informations d’identification requises

Pour accéder à l’Experience Platform de votre compte [!DNL PayPal], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | URL de l’instance de [!DNL PayPal]. |
| `clientID` | Identifiant client associé à votre application [!DNL PayPal]. |
| `clientSecret` | Secret client associé à votre application [!DNL PayPal]. |

Pour plus d’informations sur la prise en main, consultez ce [[!DNL PayPal] document](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Connecter votre compte [!DNL PayPal]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL PayPal] à Experience Platform.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Paiements]**, sélectionnez **[!UICONTROL PayPal]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur [!DNL PayPal].

![catalogue](../../../../images/tutorials/create/paypal/catalog.png)

La page **[!UICONTROL Se connecter à PayPal]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL PayPal]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis patientez quelques instants le temps d’établir la nouvelle connexion.

![connexion](../../../../images/tutorials/create/paypal/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL PayPal] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/paypal/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL PayPal]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de paiement dans Experience Platform](../../dataflow/payments.md).
