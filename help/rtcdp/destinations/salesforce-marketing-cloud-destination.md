---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.
seo-description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.
translation-type: ht
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## Présentation

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.

Pour envoyer des données de segment à Salesforce Marketing Cloud, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme CDP en temps réel Adobe, puis [configurer une importation de données](#import-data-into-salesforce) à partir de l’emplacement de stockage dans Salesforce Marketing Cloud.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez Salesforce Marketing Cloud, puis **[!UICONTROL Se connecter à la destination]**.

   ![Connexion à Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. Dans l’assistant de connexion à la destination, sélectionnez le **[!UICONTROL Type de connexion]** de votre emplacement de stockage. Pour Salesforce Marketing Cloud, vous pouvez choisir parmi **le protocole SFTP avec mot de passe** et **le protocole SFTP avec clé SSH**. Renseignez les informations ci-dessous en fonction du type de connexion, puis sélectionnez **[!UICONTROL Connexion]**.

   ![Configuration de l’assistant Salesforce](/help/rtcdp/destinations/assets/salesforce-step1.png)

   Pour les connexions **SFTP avec mot de passe**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
Pour les connexions **SFTP avec clé SSH**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignement des informations sur Salesforce](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. Dans **Informations de base**, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
   * **Nom** : choisissez un nom pertinent pour votre destination.
   * **Description** : saisissez une description pour votre destination.
   * **Chemin d’accès au dossier** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme CDP en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **Format du fichier** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base sur Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Cliquez sur **Créer** après avoir renseigné les champs dans **Informations de base**. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lors de l’[activation des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Salesforce Marketing Cloud, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Configuration de l’importation des données dans Salesforce Marketing Cloud {#import-data-into-salesforce}

Après la connexion de la plateforme CDP en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers Salesforce Marketing Cloud. Pour découvrir la procédure à suivre, consultez [Importation d’abonnés dans Marketing Cloud à partir d’un fichier](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) dans le centre d’aide de Salesforce.