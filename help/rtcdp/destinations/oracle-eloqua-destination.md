---
title: Destination Oracle Eloqua
seo-title: Destination Oracle Eloqua
description: Oracle Eloqua est une plate-forme SaaS (Software as a service) pour l'automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes du marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
seo-description: Oracle Eloqua est une plate-forme SaaS (Software as a service) pour l'automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes du marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Eloqua

## Aperçu

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) est une plate-forme SaaS (logiciel en tant que service) pour l&#39;automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes du marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.

Pour envoyer des données de segment à Oracle Eloqua, vous devez d’abord [connecter la destination](#connect-destination) dans Adobe Real-time Customer Data Platform, puis [configurer une importation](#import-data-into-eloqua) de données à partir de votre emplacement de stockage dans Oracle Eloqua.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez Oracle Eloqua, puis **[!UICONTROL Connect destination]**.

   ![Connexion à Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

1. Dans l’assistant de destination de la connexion, sélectionnez le type **[!UICONTROL de]** connexion correspondant à votre emplacement de stockage. Pour Oracle Eloqua, vous pouvez choisir entre **SFTP avec mot de passe** et **SFTP avec clé** SSH. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Connexion]**.

   ![Assistant Configuration d’Eloqua](/help/rtcdp/destinations/assets/eloqua-wizard.png)

   Pour le **protocole SFTP avec les connexions Mot de passe** , vous devez fournir Domaine, Port, Nom d’utilisateur et Mot de passe.
Pour **SFTP avec des connexions de clé** SSH, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignez les informations sur Eloqua.](/help/rtcdp/destinations/assets/eloqua-step2.png)

1. Dans Informations **** de base, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
   * **Nom**: Choisissez un nom approprié pour votre destination.
   * **Description**: Entrez une description pour votre destination.
   * **Chemin** du dossier : Indiquez le chemin d’accès dans votre emplacement de stockage où le CDP en temps réel dépose vos données d’exportation au format CSV ou tabulé.
   * **Format** de fichier : **CSV** ou **TAB_DELIMITED**. Sélectionnez le format de fichier à exporter vers votre emplacement de stockage.
   ![Informations de base sur Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

1. Cliquez sur **Créer** après avoir rempli les champs dans Informations **de** base. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination

Lorsque vous [activez des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Oracle Eloqua, nous vous recommandons de sélectionner un identifiant unique dans votre schéma [d&#39;](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)union. Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [Sélection des champs de schéma à utiliser comme attributs de destination dans vos fichiers](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportés dans Destinations marketing par courrier électronique.

## Configurer l&#39;importation des données dans Oracle Eloqua {#import-data-into-eloqua}

Après avoir connecté le CDP en temps réel à votre stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis votre emplacement de stockage dans Oracle Eloqua. Pour savoir comment effectuer cette opération, voir [Importation de contacts ou de comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) dans le Centre d&#39;aide Oracle Eloqua.