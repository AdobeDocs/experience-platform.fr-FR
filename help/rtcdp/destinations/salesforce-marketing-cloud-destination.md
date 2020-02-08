---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser des voyages pour les visiteurs et les clients afin de personnaliser leur expérience.
seo-description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser des voyages pour les visiteurs et les clients afin de personnaliser leur expérience.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## Aperçu

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser des voyages pour les visiteurs et les clients afin de personnaliser leur expérience.

Pour envoyer des données de segment à Salesforce Marketing Cloud, vous devez d’abord [connecter la destination](#connect-destination) dans le CDP en temps réel d’Adobe, puis [configurer une importation](#import-data-into-salesforce) de données à partir de votre emplacement de stockage dans Salesforce Marketing Cloud.

## Connecter la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez Salesforce Marketing Cloud, puis **[!UICONTROL Connect destination]**.

   ![Connexion à Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. Dans l’assistant de destination de la connexion, sélectionnez le type **[!UICONTROL de]** connexion correspondant à votre emplacement de stockage. Pour Salesforce Marketing Cloud, vous pouvez choisir entre **SFTP avec mot de passe** et **SFTP avec clé** SSH. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Connexion]**.

   ![Assistant Configuration de Salesforce](/help/rtcdp/destinations/assets/salesforce-step1.png)

   Pour le **protocole SFTP avec les connexions Mot de passe** , vous devez fournir Domaine, Port, Nom d’utilisateur et Mot de passe.
Pour **SFTP avec des connexions de clé** SSH, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignez les informations de Salesforce.](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. Dans Informations **de** base, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
   * **Nom**: Choisissez un nom approprié pour votre destination.
   * **Description**: Entrez une description pour votre destination.
   * **Chemin** du dossier : Indiquez le chemin d’accès dans votre emplacement de stockage où le CDP en temps réel dépose vos données d’exportation au format CSV ou tabulé.
   * **Format** de fichier : **CSV** ou **TAB_DELIMITED**. Sélectionnez le format de fichier à exporter vers votre emplacement de stockage.
   ![Informations de base Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Cliquez sur **Créer** après avoir rempli les champs dans Informations **de** base. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lorsque vous [activez des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Marketing Cloud Salesforce, nous vous recommandons de sélectionner un identifiant unique dans votre schéma [](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)d’union. Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [Sélection des champs de schéma à utiliser comme attributs de destination dans vos fichiers](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportés dans Destinations marketing par courrier électronique.

## Configuration de l’importation des données dans Salesforce Marketing Cloud {#import-data-into-salesforce}

Après avoir connecté le CDP en temps réel à votre stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis votre emplacement de stockage dans Salesforce Marketing Cloud. Pour savoir comment effectuer cette opération, voir [Importation d’abonnés dans Marketing Cloud à partir d’un fichier](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) dans le Centre d’aide Salesforce.