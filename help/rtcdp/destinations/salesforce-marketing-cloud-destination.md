---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.
seo-description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Salesforce Marketing Cloud

## Présentation

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.

Pour envoyer des données de segment à Salesforce Marketing Cloud, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme CDP en temps réel Adobe, puis [configurer une importation de données](#import-data-into-salesforce) à partir de l’emplacement de stockage dans Salesforce Marketing Cloud.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connections > Destinations]** Salesforce Marketing Cloud, sélectionnez **[!UICONTROL Connect destination]**.

   ![Connexion à Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. Au cours de l’ **[!UICONTROL Authentication]** étape, si vous aviez précédemment configuré une connexion à votre cloud  destination , sélectionnez **[!UICONTROL Existing Account]** et sélectionnez l’une de vos connexions existantes. Vous pouvez également choisir **[!UICONTROL New Account]** de configurer une nouvelle connexion. Renseignez les informations d’identification d’authentification de votre compte et sélectionnez **[!UICONTROL Connect to destination]**. Pour Salesforce Marketing Cloud, vous pouvez choisir entre **[!UICONTROL SFTP with Password]** et **[!UICONTROL SFTP with SSH Key]**. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   For **[!UICONTROL SFTP with Password]** connections, you must provide Domain, Port, Username, and Password.
Pour **[!UICONTROL SFTP with SSH Key]** les connexions, vous devez fournir Domaine, Port, Nom d’utilisateur et Clé SSH.

   ![Renseignement des informations sur Salesforce](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Name]**: Choisissez un nom approprié pour votre destination.
   * **[!UICONTROL Description]** : saisissez une description pour votre destination.
   * **[!UICONTROL Folder Path]**: Indiquez le chemin d’accès dans votre  de  où le CDP en temps réel déposera vos données d’exportation au format CSV ou tabulé.
   * **[!UICONTROL File Format]**: **[!UICONTROL CSV]** ou **[!UICONTROL TAB_DELIMITED]**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base sur Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Cliquez **[!UICONTROL Create destination]** après avoir rempli les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lors de l’[activation des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Salesforce Marketing Cloud, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Configuration de l’importation des données dans Salesforce Marketing Cloud {#import-data-into-salesforce}

Après la connexion de la plateforme CDP en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers Salesforce Marketing Cloud. Pour découvrir la procédure à suivre, consultez [Importation d’abonnés dans Marketing Cloud à partir d’un fichier](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) dans le centre d’aide de Salesforce.