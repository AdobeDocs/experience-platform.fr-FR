---
title: Destination d’identité d’entreprise Merkury
description: Découvrez comment créer une connexion de destination d’identité d’entreprise Merkury à l’aide de l’interface utilisateur de Adobe Experience Platform.
last-substantial-update: 2024-07-20T00:00:00Z
exl-id: a5452183-289c-49c3-9574-e09b0153dc00
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 14%

---

# Destination d’identité d’entreprise Merkury

>[!NOTE]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL Merkury]. Pour toute demande ou information, contactez votre représentant de compte [!DNL Merkury].

## Vue d’ensemble

Utilisez la destination [!DNL Merkury Enterprise Identity] pour créer des profils de consommateurs plus précis, complets et informatifs. Grâce à l’amélioration des données de profil, les professionnels du marketing peuvent optimiser les informations, les segments et les modèles, ce qui se traduit par un ciblage et une modélisation prédictive plus précis.

![Diagramme montrant l’interconnexion entre Merkury et Experience Platform, y compris l’ingestion et l’activation](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Suivez les étapes de cette page de documentation pour créer une connexion de destination [!DNL Merkury Identity] et activer les audiences pour identification et enrichissement à l’aide de l’interface utilisateur de Adobe Experience Platform.

>[!NOTE]
>
>Si vous souhaitez activer des audiences vers des destinations multimédias avec votre compte [!DNL Merkury Connect], utilisez plutôt la destination [!DNL Merkury Connections] .

![Carte de destination d’identité d’entreprise Merkury mise en surbrillance dans le catalogue des destinations Experience Platform.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Cas d’utilisation

La destination [!DNL Merkury Enterprise Identity] permet de transférer en toute sécurité les informations d’identification personnelles des clients pour les fonctionnalités [!DNL Merkury] suivantes :

* **Qualité des données** : améliorez la qualité des données de profil client grâce à l’hygiène et à la normalisation des données. [!DNL Merkury] comprend l’hygiène postale aux États-Unis et l’identification des déplacements pour prendre en charge les cas d’utilisation de marketing par publipostage direct les plus avancés.
* **Résolution d’identité** : permet d’obtenir une vue d’ensemble précise et complète du client, grâce aux identifiants d’individu et de ménage [!DNL Merkury]. Les identifiants Merkury offrent un niveau de liaison de profils approfondi optimisé par le graphique d&#39;identité complet des consommateurs américains adultes de [!DNL Merkury], qui représente plus de 268 millions de personnes.
* **Enrichissement** : obtenez de meilleures informations et personnalisez-les avec [!DNL Merkury Data]. [!DNL Merkury Data] comprend plus de 10 000 attributs de données disponibles, allant des données démographiques, de style de vie, financières, d’événements de la vie et d’achats du [!DNL Merkury Data Suite].

>[!NOTE]
>
>Ces cas d’utilisation sont exécutés par le biais d’une combinaison des connecteurs source et de destination. Le ou la client(e) commence par exporter ses enregistrements client existants pour enrichissement à l’aide de ce connecteur de destination. Le service de [!DNL Merkury] recherche le fichier, le récupère, l’enrichit avec les données de [!DNL Merkury] et génère un fichier. Le client utilisera alors la carte source de connecteur Source [!DNL Merkury] correspondante pour réingérer les profils client hydratés dans Adobe Real-Time CDP.

## Conditions préalables

>[!IMPORTANT]
>
>* Pour vous connecter à la destination, vous avez besoin des **Afficher les destinations** et **Gérer les destinations**, **Activer les destinations**, **Afficher les profils** et **Afficher les segments** [[autorisations de contrôle d’accès]](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/home#permissions). Lisez la [[présentation du contrôle d’accès]](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/ui/overview) ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l’**[autorisation de contrôle d’accès]** [&#x200B; Afficher le graphique d’identités](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/home#permissions).\![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Identités prises en charge {#supported-identities}

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| ECID | Experience Cloud ID | Un espace de noms représentant l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Pour plus d’informations, consultez le document suivant sur [ECID](/help/identity-service/features/ecid.md) . |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| extern_id | ID d’utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style="table-layout:auto"}

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


## Type et fréquence d’exportation

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| **Audience** | **Pris en charge** | **Origine de la description** |
|---|---|---|      
| Service de segmentation | Oui | Audiences générées via Experience Platform [[Segmentation Service]](https://experienceleague.adobe.com/fr/docs/experience-platform/segmentation/home). |
| Chargements personnalisés | Non | Les audiences [[importées]](https://experienceleague.adobe.com/fr/docs/experience-platform/segmentation/ui/overview#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Se connecter à la destination

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **&#x200B;**&#x200B;[autorisations de contrôle d’accès]&#x200B;**Afficher les destinations** et [Gérer et activer les destinations du jeu de données](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/home#permissions). Lisez la [[présentation du contrôle d’accès]](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/ui/overview) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [[tutoriel sur la configuration des destinations]](https://experienceleague.adobe.com/fr/docs/experience-platform/destinations/ui/connect-destination). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **Se connecter à la destination**.

Pour accéder à votre compartiment sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

| **Informations d’identification** | **Description** |
|---|---|
| Clé d’accès | Identifiant de clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe Merkury. |
| Clé secret | L’identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe Merkury. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur auprès de l’équipe Merkury. |

{style="table-layout:auto"}

![écran de création d’une nouvelle destination](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Renseigner les détails de la destination

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Capture d’écran des détails de la destination](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Nom (obligatoire)** - Le nom sous lequel la destination sera enregistrée
* **Description** - Brève explication de l’objectif de la destination
* **Nom du compartiment (obligatoire)** - Nom du compartiment Amazon S3 configuré sur S3
* **Chemin du dossier (obligatoire)** - si des sous-répertoires sont utilisés dans un compartiment, un chemin d’accès doit être défini, ou « / » pour référencer le chemin racine.
* **Type de fichier** - Sélectionnez le format qu’Experience Platform doit utiliser pour les fichiers exportés. Consultez votre équipe Merkury pour connaître le type de fichier attendu pour votre compte.

>[!NOTE]
>
>Lors de la sélection de l’option CSV, les options Délimiteur, Citation, Caractère d’échappement, Valeur vide, Valeur nulle, Format de compression et Inclure le fichier manifeste seront présentées. Consultez votre équipe Merkury pour obtenir les paramètres appropriés pour votre compte.

![image de l’option csv](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Compte existant

Les comptes déjà définis à l’aide de la destination Identité d’entreprise Merkury apparaissent dans un pop-up de liste. Lorsque cette option est sélectionnée, les détails du compte s’affichent dans le rail de droite. Affichez l’exemple à partir de l’interface utilisateur, lorsque vous accédez à **Destinations** > **Comptes**;

![Capture d’écran du compte de destination dans la page des comptes de destination](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Activer les alertes

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur [l’abonnement aux alertes des destinations dans l’interface utilisateur](https://experienceleague.adobe.com/fr/docs/experience-platform/destinations/ui/alerts).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **Suivant**.

## Activer des audiences vers cette destination

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **Afficher les destinations**, **Activer les destinations**, **Afficher les profils** et **Afficher les segments**. Lisez la présentation du contrôle d’accès ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter des identités, vous avez besoin de l’autorisation de contrôle d’accès **Afficher le graphique d’identités**.

Lisez [Activer les données d’audience vers des destinations d’exportation de profils par lots](https://experienceleague.adobe.com/fr/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Suggestions de mappage

Le traitement correct des fichiers côté [!DNL Merkury] nécessite des éléments de nom et d’adresse. Bien que tous les éléments ne soient pas nécessaires, fournir autant d’éléments que possible aidera à une mise en correspondance réussie.

Le tableau ci-dessous fournit des suggestions de mappage en répertoriant, du côté de votre destination, les attributs utilisés par le traitement des [!DNL Merkury] vers lesquels les clients peuvent mapper des attributs de profil. Traitez ces éléments comme des suggestions, car tous les éléments ne sont pas requis et les valeurs sources dépendent des besoins du compte.

| Champ cible | Description du Source |
|---|---|
| identifiant | Champ d’identité à utiliser pour mapper les données de [!DNL Merkury] à Experience Platform via le connecteur Source [!DNL Merkury Enterprise Identity] |
| Input_First_Name | Valeur `person.name.firstName` dans Experience Platform. |
| Input_Last_Name | Valeur `person.name.lastName` dans Experience Platform. |
| Input_Address_Line_1 | Valeur `mailingAddress.street` dans Experience Platform. |
| Input_City | Valeur `mailingAddress.city` dans Experience Platform. |
| Input_State_Province_Code | Valeur `mailingAddress.state` dans Experience Platform. Utilisez si l’état se trouve dans le formulaire de code à deux caractères. |
| Input_State_Province_Name | Valeur `mailingAddress.state` dans Experience Platform. Utilisez si l’état est le nom complet de l’état |
| Input_Postal_Code | Valeur `mailingAddress.postalCode` dans Experience Platform. |
| Input_Email_Address | Valeur à mapper en tant qu’adresse e-mail des profils. |
| Input_Phone | Valeur à mapper en tant que numéro de téléphone de profil. |

{style="table-layout:auto"}

## Valider l’exportation des données

Pour vérifier si l’exportation des données a réussi, vérifiez votre compartiment de stockage Amazon S3 et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Utilisation et gouvernance des données

Toutes les destinations Adobe Experience Platform sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la manière dont Adobe Experience Platform applique la gouvernance des données, lisez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/fr/docs/experience-platform/data-governance/home).

## Étapes suivantes

Ce tutoriel vous a permis de créer un flux de données pour exporter les données de profil d’Experience Platform vers votre emplacement S3 géré par [!DNL Merkury]. Ensuite, vous devez contacter votre représentant [!DNL Merkury] avec le nom du compte, les noms de fichier et le chemin d’accès au compartiment afin que le traitement puisse s’installer.
