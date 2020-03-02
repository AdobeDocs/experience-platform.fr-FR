---
title: Destination Oracle Eloqua
seo-title: Destination Oracle Eloqua
description: Oracle Eloqua est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
seo-description: Oracle Eloqua est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
translation-type: ht
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Eloqua

## Présentation

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.

Pour envoyer des données de segment à Oracle Eloqua, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme de données client en temps réel Adobe, puis [configurer une importation de données](#import-data-into-eloqua) à partir de l’emplacement de stockage dans Oracle Eloqua.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez Oracle Eloqua, puis **[!UICONTROL Se connecter à la destination]**.

   ![Se connecter à Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

1. Dans l’assistant de connexion à la destination, sélectionnez le **[!UICONTROL Type de connexion]** de votre emplacement de stockage. Pour Oracle Eloqua, vous pouvez choisir parmi **le protocole SFTP avec mot de passe** et **le protocole SFTP avec clé SSH**. Renseignez les informations ci-dessous en fonction du type de connexion, puis sélectionnez **[!UICONTROL Connexion]**.

   ![Configurer l’assistant Oracle Eloqua](/help/rtcdp/destinations/assets/eloqua-wizard.png)

   Pour les connexions **SFTP avec mot de passe**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
Pour les connexions **SFTP avec clé SSH**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignement des informations sur Eloqua](/help/rtcdp/destinations/assets/eloqua-step2.png)

1. Dans **Informations de base**, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
   * **Nom** : choisissez un nom pertinent pour votre destination.
   * **Description** : saisissez une description pour votre destination.
   * **Chemin d’accès au dossier** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme CDP en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **Format du fichier** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base sur Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

1. Cliquez sur **Créer** après avoir renseigné les champs dans **Informations de base**. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination

Lors de l’[activation des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Oracle Eloqua, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Configurer l’importation des données dans Oracle Eloqua {#import-data-into-eloqua}

Après la connexion de la plateforme CDP en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers Oracle Eloqua. Pour découvrir la procédure à suivre, consultez [Importation de contacts ou comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) du centre d’aide d’Oracle Eloqua.