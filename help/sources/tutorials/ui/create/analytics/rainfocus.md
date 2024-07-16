---
title: Connexion de votre compte RainFocus à un Experience Platform à l’aide de l’interface utilisateur
description: Découvrez comment connecter votre compte RainFocus à Experience Platform à l’aide de l’interface utilisateur.
badge: Version bêta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 26%

---

# Connectez votre compte [!DNL RainFocus] à un Experience Platform à l’aide de l’interface utilisateur

>[!NOTE]
>
>La source [!DNL RainFocus] est en version Beta. Pour plus d’informations sur l’utilisation de sources étiquetées bêta, consultez la [présentation des sources](../../../../home.md#terms-and-conditions) .

Ce tutoriel décrit les étapes à suivre pour connecter votre compte [!DNL RainFocus] et diffuser des données d’analyse et de gestion des événements vers Adobe Experience Platform.

>[!IMPORTANT]
>
>Ce connecteur source et cette page de documentation sont créés et gérés par l’équipe [!DNL RainFocus]. Pour toute question ou demande de mise à jour, contactez-les directement à l’adresse clientcare<span>@rainfocus.com ou rendez-vous sur le [[!DNL RainFocus] centre d’aide](https://help.rainfocus.com/hc/en-us)

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

### Conditions préalables

Avant de pouvoir connecter votre compte [!DNL RainFocus] à un Experience Platform, vous devez d’abord effectuer les tâches prérequises suivantes :

* [Collecter les informations d’identification requises](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Créer un schéma XDM et définir le champ d’identité](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Création d’un profil d’intégration dans RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Une fois la configuration prérequise terminée, vous pouvez passer aux étapes décrites ci-dessous.

## Connectez votre compte RainFocus à Experience Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail des sources. L’écran *[!UICONTROL Catalogue]* affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie *[!UICONTROL Analytics]*, sélectionnez **[!UICONTROL RainFocus Experience]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue des sources sur l’interface utilisateur Experience Platform avec la source RainFocus sélectionnée.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Sélectionner les données

L’étape Sélectionner les données s’affiche, vous permettant ainsi de sélectionner les données que vous apportez à Experience Platform.

* La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
* La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

Sélectionnez **[!UICONTROL Télécharger des fichiers]** pour charger un fichier JSON à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier JSON que vous souhaitez charger dans le panneau Glisser-déposer des fichiers .

Téléchargez l’exemple de charge utile JSON téléchargé à partir de **RainFocus**.

![L’étape de sélection des données dans le workflow des sources.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Une fois le fichier chargé, l’interface de prévisualisation se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface d’aperçu vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser l’utilitaire de champ de recherche pour accéder à des éléments spécifiques de votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Étape de prévisualisation des données du workflow des sources.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Détails du flux de données

L’étape **Détails du flux de données** s’affiche, vous fournissant des options permettant d’utiliser un jeu de données existant ou d’établir un nouveau jeu de données pour votre flux de données, ainsi qu’une opportunité de fournir un nom et une description pour votre flux de données. Au cours de cette étape, vous pouvez également configurer des paramètres pour l’ingestion de profils, les diagnostics d’erreur, l’ingestion partielle et les alertes.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de détail du flux de données du flux de sources.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Mappage {#mapping}

L’étape Mappage s’affiche, vous fournissant une interface pour mapper les champs source de votre schéma source à leurs champs XDM cibles appropriés dans le schéma cible.

Experience Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [guide de l’interface utilisateur de la préparation des données](../../../../../data-prep/ui/mapping.md).

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de mappage du workflow des sources.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Révision

L’écran de **Révision** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **Connexion** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **Attribuer des champs de jeu de données et de mappage** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez vérifié votre flux de données, sélectionnez **Terminer** et patientez quelques instants le temps que le flux de données soit créé.

![L’étape de révision du workflow des sources.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Obtention de l’URL de votre point de terminaison de diffusion {#get-your-streaming-endpoint-url}

Une fois votre flux de données de diffusion en continu créé, vous pouvez désormais récupérer l’URL de votre point de terminaison de diffusion en continu. Ce point de terminaison sera utilisé pour s’abonner à votre webhook, ce qui permet à votre source de diffusion en continu de communiquer avec l’Experience Platform.

Pour récupérer votre point de terminaison de diffusion en continu, accédez à la page *[!UICONTROL Activité Flux de données]* du flux de données que vous venez de créer et copiez le point de terminaison depuis le bas du panneau *[!UICONTROL Propriétés]*.

![Page de l’activité de flux de données dans l’espace de travail des sources, avec l’URL du point de terminaison de diffusion en continu mise en surbrillance.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Activation de votre profil d’intégration dans RainFocus

Une fois votre flux de données terminé et que vous avez récupéré l’URL de votre point de terminaison de diffusion en continu, vous pouvez désormais activer le [!DNL Integration Profile] dans [!DNL RainFocus].

* Connectez-vous à la [[!DNL RainFocus] plateforme](https://app.rainfocus.com). Dans la navigation principale, sélectionnez **[!DNL Libraries]** et **[!DNL Integration Profiles]**
* Ouvrez le [!DNL Integration Profile] que vous avez créé précédemment dans le cadre des [conditions préalables](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Collez l’ **identifiant de flux de données** et le **point d’entrée de flux de données** copiés à partir du flux de données dans Experience Platform et sélectionnez **Enregistrer**

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion pour votre source [!DNL RainFocus], ce qui vous permet de diffuser vos données d’analyse et de gestion des événements vers Experience Platform.

## Ressources supplémentaires

Les documents suivants fournissent des conseils supplémentaires sur les nuances entourant la source [!DNL RainFocus].

* [Centre d’aide RainFocus](https://help.rainfocus.com/hc/en-us)
* [Création d’un compte de service Adobe (JWT) dans le portail Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Création d’un schéma dans l’API](../../../../../xdm/tutorials/create-schema-api.md)
* [Créer un schéma dans l’interface utilisateur](../../../../../xdm/tutorials/create-schema-ui.md)
* [Définition des champs d’identité dans l’interface utilisateur](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
