---
title: Connexion Salesforce Marketing Cloud
description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement appelée ExactTarget que vous pouvez utiliser pour créer et personnaliser des parcours afin que les visiteurs et les clients puissent personnaliser leur expérience.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
TQID: https://experienceleague.adobe.com/urBKagixPmCpK0vb2-Y-aXtTsHv2UGe59elXSSKrzOs
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: beb7a3c1-66ab-4786-b879-7621375b3c40
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 947
ht-degree: 29%

---

# Connexion [!DNL (Files) Salesforce Marketing Cloud]

## Vue d’ensemble {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/fr/products/marketing-cloud/email-marketing/) est une suite de marketing numérique anciennement appelée ExactTarget que vous pouvez utiliser pour créer et personnaliser des parcours afin que les visiteurs et les clients puissent personnaliser leur expérience.

Pour envoyer des données d’audience à [!DNL Salesforce Marketing Cloud], vous devez d’abord [vous connecter à la destination](#connect-destination) dans Experience Platform, puis [configurer une importation de données](#import-data-into-salesforce) à partir de l’emplacement de stockage vers [!DNL Salesforce Marketing Cloud].

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform, telles que [!DNL Adobe Journey Optimizer], </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données [!DNL Adobe Experience Platform]. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Consultez le tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Liste autorisée d’adresses IP {#allow-list}

Lors de la configuration de destinations de marketing par e-mail avec stockage SFTP, Adobe vous recommande d’ajouter certaines plages d’adresses IP à votre place sur la liste autorisée.

Consultez la section place sur la liste autorisée des adresses IP pour les destinations SFTP](../cloud-storage/ip-address-allow-list.md) si vous devez ajouter des adresses IP Adobe à votre place sur la liste autorisée.[

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Cette destination prend en charge les types de connexion suivants :

* **[!UICONTROL SFTP avec mot de passe]**
* **[!UICONTROL SFTP avec clé SSH]**

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir :
   * **[!UICONTROL Domain]** : l’adresse IP ou le nom de domaine de votre compte SFTP ;
   * **[!UICONTROL Port]** : port utilisé par votre emplacement de stockage SFTP ;
   * **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur pour la connexion à l’emplacement de stockage de votre SFTP ;
   * **[!UICONTROL Mot de passe]** : mot de passe pour se connecter à l’emplacement de stockage de votre SFTP.
* Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir :
   * **[!UICONTROL Domain]** : l’adresse IP ou le nom de domaine de votre compte SFTP ;
   * **[!UICONTROL Port]** : port utilisé par votre emplacement de stockage SFTP ;
   * **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur pour la connexion à l’emplacement de stockage de votre SFTP ;
   * **[!UICONTROL Clé SSH]** : clé SSH privée utilisée pour se connecter à l’emplacement de stockage de votre SFTP. La clé privée doit être mise en forme sous la forme d’une chaîne codée en Base64 et ne doit pas être protégée par un mot de passe.

* Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Clé]**. Votre clé publique doit être écrite en tant que chaîne codée en [!DNL Base64].
* **[!UICONTROL Nom]** : choisissez un nom approprié pour votre destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination.
* **[!UICONTROL Chemin du dossier]** : indiquez le chemin d’accès à l’emplacement de stockage où Experience Platform déposera vos données d’exportation au format CSV.
* **[!UICONTROL Format de fichier]** : sélectionnez **CSV** pour exporter des fichiers CSV vers votre emplacement de stockage.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [ Activer les données d’audience vers des destinations d’exportation de profils par lots ](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Attributs de destination {#destination-attributes}

Lors de l’activation des audiences vers cette destination, Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [ Bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail](overview.md#best-practices).

## Données exportées {#exported-data}

Pour les destinations [!DNL Salesforce Marketing Cloud], Experience Platform crée un fichier `.csv` à l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez [vérifier l’activation de l’audience](../../ui/activate-batch-profile-destinations.md#verify) dans le tutoriel sur l’activation des audiences.

## Configurer l’importation des données dans [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Après la connexion de [!DNL Experience Platform] à votre espace de stockage [!DNL SFTP], vous devez configurer l’importation des données depuis l’emplacement de stockage vers [!DNL Salesforce Marketing Cloud]. Pour découvrir la procédure à suivre, reportez-vous à la section [Importation d’abonnés dans Marketing Cloud à partir d’un fichier](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) de la [!DNL Salesforce Help Center].
