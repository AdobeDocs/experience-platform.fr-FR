---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui vous aident à personnaliser et à diffuser des campagnes sur tous vos canaux en ligne et hors ligne.
seo-description: Adobe Campaign est un ensemble de solutions qui vous aident à personnaliser et à diffuser des campagnes sur tous vos canaux en ligne et hors ligne.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Adobe Campaign

## Aperçu

Adobe Campaign est un ensemble de solutions qui vous aident à personnaliser et à diffuser des campagnes sur tous vos canaux en ligne et hors ligne. Voir [A propos d’Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) pour plus d’informations.

Pour envoyer des données de segment à Adobe Campaign, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme de données clientes Adobe en temps réel, puis [configurer une importation](#import-data-into-campaign) de données à partir de votre emplacement de stockage dans Adobe Campaign.

## Connecter la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez Adobe Campaign, puis **[!UICONTROL Connect destination]**.

   ![Se connecter à Adobe Campaign](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. Dans l’assistant de destination de la connexion, sélectionnez le type **[!UICONTROL de]** connexion correspondant à votre emplacement de stockage. Pour Adobe Campaign, vous pouvez choisir entre **Amazon S3**, **SFTP avec mot de passe** et **SFTP avec clé** SSH. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Connexion]**.

   ![Assistant Configuration d’une campagne](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Pour les connexions **S3** , vous devez fournir votre ID de clé d&#39;accès et votre clé d&#39;accès secrète.
Pour le **protocole SFTP avec les connexions Mot de passe** , vous devez fournir Domaine, Port, Nom d’utilisateur et Mot de passe.
Pour **SFTP avec des connexions de clé** SSH, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignez les informations de campagne.](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Dans Informations **de** base, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
   * **Nom**: Choisissez un nom approprié pour votre destination.
   * **Description**: Entrez une description pour votre destination.
   * **Nom** du compartiment : *Pour les connexions* S3. Entrez l’emplacement du compartiment S3 où le CDP en temps réel dépose vos données d’exportation au format CSV ou tabulé.
   * **Chemin** du dossier : Indiquez le chemin d’accès dans votre emplacement de stockage où le CDP en temps réel dépose vos données d’exportation au format CSV ou tabulé.
   * **Format** de fichier : **CSV** ou **TAB_DELIMITED**. Sélectionnez le format de fichier à exporter vers votre emplacement de stockage.
   ![Informations de base sur la campagne](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Cliquez sur **Créer** après avoir rempli les champs dans Informations **de** base. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lorsque vous [activez des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Adobe Campaign, nous vous recommandons de sélectionner un identifiant unique dans votre schéma [](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)d’union. Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [Sélection des champs de schéma à utiliser comme attributs de destination dans vos fichiers](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportés dans Destinations marketing par courrier électronique.


## Configuration de l’importation des données dans Adobe Campaign {#import-data-into-campaign}

Après avoir connecté le CDP en temps réel à votre stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis votre emplacement de stockage dans Adobe Campaign. Pour savoir comment effectuer cette opération, voir [Importation de données](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) dans la documentation d’aide d’Adobe Campaign.