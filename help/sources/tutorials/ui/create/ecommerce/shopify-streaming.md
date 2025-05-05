---
title: Créer Une Connexion En Continu Et Un Flux De Données Shopify Dans L’Interface Utilisateur
description: Découvrez comment créer une connexion source et un flux de données de streaming Shopify à l’aide de l’interface utilisateur d’Experience Platform
badge: Beta
exl-id: d53f4ab5-8bdc-4647-83d5-ee898abda0f2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 32%

---

# Créer une connexion source et un flux de données pour les données [!DNL Shopify Streaming] à l’aide de l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Shopify Streaming] et un flux de données à l’aide de l’interface utilisateur d’Experience Platform.

## Prise en main {#getting-started}

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

>[!IMPORTANT]
>
>Pour suivre ce tutoriel, vous devez avoir terminé la configuration requise pour votre compte [!DNL Shopify Streaming]. Pour obtenir des instructions sur la configuration de votre compte, lisez la [[!DNL Shopify Streaming] présentation](../../../../connectors/ecommerce/shopify-streaming.md).

## Connecter votre compte [!DNL Shopify Streaming]

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **eCommerce**, sélectionnez [!DNL Shopify Streaming], puis **[!UICONTROL Ajouter des données]**.

![Catalogue des sources Experience Platform](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Sélectionner les données

L’étape **[!UICONTROL Sélectionner les données]** s’affiche, fournissant une interface vous permettant de sélectionner les données que vous apportez à Experience Platform.

* La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
* La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

Sélectionnez **[!UICONTROL Télécharger des fichiers]** pour télécharger un fichier JSON à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier JSON que vous souhaitez charger dans le panneau [!UICONTROL Glisser-déposer des fichiers].

![Étape d’ajout de données du workflow des sources.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

Une fois votre fichier chargé, l’interface de prévisualisation se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface de prévisualisation vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser l’utilitaire [!UICONTROL Champ de recherche] pour accéder à des éléments spécifiques à partir de votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Étape de prévisualisation du workflow des sources.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Détails du flux de données

L’étape **Détails du flux de données** s’affiche, vous offrant des options pour utiliser un jeu de données existant ou établir un nouveau jeu de données pour votre flux de données, ainsi que la possibilité de fournir un nom et une description pour votre flux de données. Au cours de cette étape, vous pouvez également configurer les paramètres d’ingestion de profil, de diagnostics d’erreur, d’ingestion partielle et d’alertes.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Étape du flux de données-détail du workflow des sources.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Mappage

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Experience Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous sélectionnez. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [ Guide de l’interface utilisateur de la préparation des données ](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html?lang=fr).

Une fois vos données source mappées, sélectionnez **[!UICONTROL Suivant]**.

![Étape de mappage du workflow des sources.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Révision

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![Étape de révision du workflow des sources.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Obtention de l’URL du point d’entrée de diffusion en continu

Une fois votre flux de données en continu créé, vous pouvez récupérer votre URL de point d’entrée en continu. Ce point d’entrée sera utilisé pour vous abonner à votre webhook, ce qui permettra à votre source de diffusion en continu de communiquer avec Experience Platform.

Pour récupérer votre point d’entrée de flux continu, accédez à la page [!UICONTROL Activité du flux de données] du flux de données que vous venez de créer, puis copiez le point d’entrée au bas du panneau [!UICONTROL Propriétés].

![Point d’entrée de flux continu dans l’activité de flux de données.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion source et un flux de données vers votre compte [!DNL Shopify Streaming]. Pour obtenir des instructions sur la connexion de votre compte [!DNL Shopify Streaming] à l’aide de l’API , consultez le tutoriel sur [la création d’une connexion source et d’un flux de données pour diffuser  [!DNL Shopify]  données à l’aide de l’API Flow Service](../../../api/create/ecommerce/shopify-streaming.md).
