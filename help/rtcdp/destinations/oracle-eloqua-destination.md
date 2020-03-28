---
title: Destination Oracle Eloqua
seo-title: Destination Oracle Eloqua
description: Oracle Eloqua est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
seo-description: Oracle Eloqua est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Oracle Eloqua

## Présentation

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.

Pour envoyer des données de segment à Oracle Eloqua, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme de données client en temps réel Adobe, puis [configurer une importation de données](#import-data-into-eloqua) à partir de l’emplacement de stockage dans Oracle Eloqua.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connections > Destinations]** Oracle Eloqua, sélectionnez **[!UICONTROL Connect destination]**.

   ![Se connecter à Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Au cours de l’ **[!UICONTROL Authentication]** étape, si vous aviez précédemment configuré une connexion à votre cloud  destination , sélectionnez **[!UICONTROL Existing Account]** et sélectionnez l’une de vos connexions existantes. Vous pouvez également choisir **[!UICONTROL New Account]** de configurer une nouvelle connexion. Renseignez les informations d’identification d’authentification de votre compte et sélectionnez **[!UICONTROL Connect to destination]**. Pour Oracle Eloqua, vous pouvez sélectionner entre **[!UICONTROL SFTP with Password]** et **[!UICONTROL SFTP with SSH Key]**. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   For **[!UICONTROL SFTP with Password]** connections, you must provide Domain, Port, Username, and Password.
Pour **[!UICONTROL SFTP with SSH Key]** les connexions, vous devez fournir Domaine, Port, Nom d’utilisateur et Clé SSH.

   ![Configurer l’assistant Oracle Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Name]**: Choisissez un nom approprié pour votre destination.
   * **[!UICONTROL Description]** : saisissez une description pour votre destination.
   * **[!UICONTROL Folder Path]**: Indiquez le chemin d’accès dans votre  de  où le CDP en temps réel déposera vos données d’exportation au format CSV ou tabulé.
   * **[!UICONTROL File Format]**: **CSV** ou **TAB_DELIMITED**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base sur Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Cliquez **[!UICONTROL Create destination]** après avoir rempli les champs ci-dessus. Your destination is now created and you can [activate segments](/help/rtcdp/destinations/activate-destinations.md) to the destination.

## Attributs de destination

Lors de l’[activation des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Oracle Eloqua, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Configurer l’importation des données dans Oracle Eloqua {#import-data-into-eloqua}

Après la connexion de la plateforme CDP en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers Oracle Eloqua. Pour découvrir la procédure à suivre, consultez [Importation de contacts ou comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) du centre d’aide d’Oracle Eloqua.