---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
seo-description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Adobe Campaign

## Présentation

Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne. Pour plus d’informations, consultez [À propos d’Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Pour envoyer des données de segment à Adobe Campaign, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme de données client en temps réel Adobe, puis [configurer une importation de données](#import-data-into-campaign) à partir de l’emplacement de stockage dans Adobe Campaign.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connections > Destinations]**, sélectionnez  Adobe Campaign, puis **[!UICONTROL Connect destination]**.

   ![Se connecter à Adobe Campaign](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. In the Connect destination workflow, select the **[!UICONTROL Connection type]** for your storage location. Pour  Adobe Campaign, vous pouvez choisir entre **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP with Password]** et **[!UICONTROL SFTP with SSH Key]**. Fill in the information below, depending on your connection type, then select **[!UICONTROL Connect]**.

   ![Configuration de l’assistant Campaign](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Pour les connexions **[!UICONTROL Amazon S3]**, vous devez fournir un identifiant de clé d’accès et une clé d’accès secrète.
For **[!UICONTROL SFTP with Password]** connections, you must provide Domain, Port, Username, and Password.
Pour **[!UICONTROL SFTP with SSH Key]** les connexions, vous devez fournir Domaine, Port, Nom d’utilisateur et Clé SSH.

   ![Renseignement des informations sur Campaign](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. In **[!UICONTROL Basic Information]**, fill in the relevant information for your destination, as shown below:
   * **[!UICONTROL Name]**: Choisissez un nom approprié pour votre destination.
   * **[!UICONTROL Description]** : saisissez une description pour votre destination.
   * **[!UICONTROL Bucket Name]**: *Pour les connexions* S3. Indiquez l’emplacement du compartiment S3 où la plateforme CDP en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **[!UICONTROL Folder Path]**: Indiquez le chemin d’accès dans votre  de  où le CDP en temps réel déposera vos données d’exportation au format CSV ou tabulé.
   * **[!UICONTROL File Format]**: **CSV** ou **TAB_DELIMITED**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base sur Campaign](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Cliquez **[!UICONTROL Create]** après avoir rempli les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lors de l’[activation des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Adobe Campaign, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.


## Configurer l’importation des données dans Adobe Campaign {#import-data-into-campaign}

Après la connexion de la plateforme CDP en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers Adobe Campaign. Pour découvrir la procédure à suivre, consultez [Importation de données](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) dans la documentation d’aide d’Adobe Campaign.