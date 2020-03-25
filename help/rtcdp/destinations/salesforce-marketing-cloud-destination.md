---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.
seo-description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.
translation-type: tm+mt
source-git-commit: afe8032be1d96a63a3d43c5a552a0d6152e14552

---


# Salesforce Marketing Cloud

## Présentation

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.

Pour envoyer des données de segment à Salesforce Marketing Cloud, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme CDP en temps réel Adobe, puis [configurer une importation de données](#import-data-into-salesforce) à partir de l’emplacement de stockage dans Salesforce Marketing Cloud.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connections > Destinations]** Salesforce Marketing Cloud, sélectionnez **[!UICONTROL Connect destination]**.

   ![Connexion à Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. À l’étape **Authentification** , si vous aviez précédemment configuré une connexion à votre cloud  destination , sélectionnez **[!UICONTROL Existing Account]** et sélectionnez votre connexion existante. Vous pouvez également choisir **[!UICONTROL New Account]** de configurer une nouvelle connexion. Renseignez les informations d’identification d’authentification de votre compte et sélectionnez **[!UICONTROL Connect to destination]**. Pour Salesforce Marketing Cloud, vous pouvez choisir parmi **le protocole SFTP avec mot de passe** et **le protocole SFTP avec clé SSH**. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   Pour les connexions **SFTP avec mot de passe**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
Pour les connexions **SFTP avec clé SSH**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignement des informations sur Salesforce](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

1. In the **Setup** step, fill in the relevant information for your destination as shown below:
   * **Nom** : choisissez un nom pertinent pour votre destination.
   * **Description** : saisissez une description pour votre destination.
   * **Chemin d’accès au dossier** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme CDP en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **Format du fichier** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base sur Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Click **Create destination** after filling in the fields in **Basic Information**. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lors de l’[activation des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Salesforce Marketing Cloud, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Configuration de l’importation des données dans Salesforce Marketing Cloud {#import-data-into-salesforce}

Après la connexion de la plateforme CDP en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers Salesforce Marketing Cloud. Pour découvrir la procédure à suivre, consultez [Importation d’abonnés dans Marketing Cloud à partir d’un fichier](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) dans le centre d’aide de Salesforce.