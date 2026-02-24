---
title: Amélioration des données Acxiom
description: Utilisez ce connecteur pour activer les profils Adobe propriétaires dans Real-Time CDP vers Acxiom pour l’enrichissement des données et leur utilisation sur les canaux marketing. Vous pouvez ensuite utiliser la source Acxiom pour importer les profils avec des données améliorées et les utiliser dans Real-Time CDP.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 24%

---

# [!DNL Acxiom Data Enhancement] la connexion de destination

>[!NOTE]
>
>La destination [!DNL Acxiom Data Enhancement] est en version bêta.  Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe d’Acxiom. Pour toute demande ou information, contactez directement l&#39;équipe à l&#39;adresse acxiom-adobe-help@acxiom.com.

## Vue d’ensemble {#overview}

Utilisez le connecteur [!DNL Acxiom Data Enhancement] pour fournir des données descriptives supplémentaires à vos profils client, à utiliser dans les applications d’analyse, de segmentation et de ciblage. Avec des centaines d’éléments disponibles, vous pouvez mieux segmenter et modéliser les données, ce qui se traduit par un ciblage et une modélisation prédictive plus précis.

![Diagramme marketing pour exporter des données propriétaires vers Acxiom, puis importer des données enrichies dans Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

Ce tutoriel décrit les étapes à suivre pour créer une connexion de destination et un flux de données [!DNL Acxiom Data Enhancement] à l’aide de l’interface utilisateur de Adobe Experience Platform. Ce connecteur est utilisé pour diffuser des données au service d’amélioration d’Acxiom à l’aide d’Amazon S3 comme point de dépôt.

![Le catalogue de destination avec la destination Acxiom sélectionnée.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Acxiom Data Enhancement], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Améliorer les données client {#enhance-customer-data}

Ce connecteur doit être utilisé par les professionnels du marketing afin d’améliorer l’efficacité de leurs stratégies de sensibilisation en ajoutant des éléments descriptifs sélectionnés à leurs profils client et en les utilisant pour mieux cibler les campagnes.

Par exemple, en tant que spécialiste marketing, vous pouvez souhaiter approfondir votre compréhension de vos audiences existantes en enrichissant leurs profils avec des données supplémentaires. Cela permet d’améliorer vos stratégies de segmentation et de ciblage, ce qui donne un coup de pouce à la personnalisation et à la conversion des campagnes.

Le cas d’utilisation est exécuté à l’aide d’une combinaison des connecteurs source et de destination.

Commencez par exporter les enregistrements de vos clients existants pour les enrichir à l’aide de ce connecteur de destination. Le service d’Acxiom recherchait le fichier, le récupérait, l’enrichissait avec les données d’Acxiom et générait un fichier.

Le client utilisera alors la carte source [Acxiom Data Ingestion](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) correspondante pour réingérer les profils client hydratés dans Adobe Real-Time CDP.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>* Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Non | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}




Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Type d’exportation | **[!UICONTROL Profile-based]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Batch]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage and Activate Dataset Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

Pour accéder à votre compartiment sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

| Informations d’identification | Description |
|---------------|----------------------------------------------------------------------------------------------------------|
| Clé d’accès S3 | Identifiant de clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Clé secrète S3 | L’identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |

### Nouveau compte

Pour définir un nouvel emplacement Acxiom Managed S3 :

![Nouveau compte](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Compte existant

Les comptes déjà définis à l’aide de la destination [!DNL Acxiom Data Enhancement] apparaissent dans un pop-up de liste. Lorsque cette option est sélectionnée, les détails du compte s’affichent dans le rail de droite. Affichez l’exemple à partir de l’interface utilisateur, lorsque vous accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** ;

![Compte existant](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Détails de la destination](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Nom (obligatoire)** - Le nom sous lequel la destination sera enregistrée
* **Description** - Brève explication de l’objectif de la destination
* **Nom du compartiment (obligatoire)** - Nom du compartiment Amazon S3 configuré sur S3
* **Chemin du dossier (obligatoire)** - si des sous-répertoires sont utilisés dans un compartiment, un chemin d’accès doit être défini, ou « / » pour référencer le chemin racine.
* **Type de fichier** - Sélectionnez le format qu’Experience Platform doit utiliser pour les fichiers exportés. Actuellement, le seul type de fichier attendu pour le traitement d’Acxiom est CSV

>[!IMPORTANT]
>
>Lors de la sélection de l’option CSV, les options *Délimiteur*, *Citation*, *Caractère d’échappement*, *Valeur vide*, *Valeur nulle*, *Format de compression* et *Inclure le fichier manifeste* sont présentées. Le document suivant explique ces paramètres de manière plus détaillée [configurer les options de formatage](../../ui/batch-destinations-file-formatting-options.md).

![&#x200B; Options CSV &#x200B;](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

### Suggestions de mappage

Le traitement correct des fichiers côté Acxiom nécessite des éléments de nom et d’adresse. Bien que tous les éléments ne soient pas nécessaires, fournir autant d’éléments que possible aidera à une mise en correspondance réussie.

Le tableau ci-dessous fournit des suggestions de mappage. Il répertorie les attributs de votre côté de destination utilisés par le traitement Acxiom auquel les clients peuvent mapper des attributs de profil. Traitez ces éléments comme des suggestions, car tous les éléments ne sont pas nécessaires et les valeurs sources dépendent des besoins du compte.

| Champ cible | Description du Source |
|--------------|-------------------------------------------------------------|
| nom | Valeur `person.name.fullName` dans Experience Platform. |
| Prénom | Valeur `person.name.firstName` dans Experience Platform. |
| Nom | Valeur `person.name.lastName` dans Experience Platform. |
| address1 | Valeur `mailingAddress.street1` dans Experience Platform. |
| address2 | Valeur `mailingAddress.street2` dans Experience Platform. |
| ville | Valeur `mailingAddress.city` dans Experience Platform. |
| state | Valeur `mailingAddress.state` dans Experience Platform. |
| fermeture éclair | Valeur `mailingAddress.postalCode` dans Experience Platform. |

>[!NOTE]
>
>Si vous mappez des champs supplémentaires qui ne sont pas répertoriés ci-dessus dans le flux de données, ils seront inclus dans l’exportation des données, mais seront ignorés par le traitement Acxiom.

## Valider l’exportation des données {#exported-data}

Pour contrôler que l’exportation des données a bien réussi, vérifiez votre compartiment [!DNL Amazon S3 Storage] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Étapes suivantes

Ce tutoriel vous a permis de créer un flux de données pour exporter les données de profil d’Experience Platform vers votre emplacement S3 géré par [!DNL Acxiom]. Ensuite, vous devez contacter votre représentant Acxiom avec le nom du compte, les noms de fichier et le chemin d’accès au compartiment afin que le traitement puisse s’installer.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

*Acxiom Infobase:* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
