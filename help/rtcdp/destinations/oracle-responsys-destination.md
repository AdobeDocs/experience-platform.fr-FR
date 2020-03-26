---
title: Destination Oracle Responsys
seo-title: Destination Oracle Responsys
description: Responsys est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.
seo-description: Responsys est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.
translation-type: tm+mt
source-git-commit: c3fe5753fb23f99076f9c85b4e07af2d25a121a9

---


# Oracle Responsys

## Présentation

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.

To send segment data to Oracle Responsys, you must first [connect to the destination](#connect-destination) in Adobe Real-time Customer Data Platform, and then [set up a data import](#import-data-into-responsys) from your storage location into Oracle Responsys.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connections > Destinations]** Oracle Responsys, sélectionnez **[!UICONTROL Connect destination]**.

   ![Connexion à Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. À l’étape **Authentification** , si vous aviez précédemment configuré une connexion à votre cloud  destination , sélectionnez **[!UICONTROL Existing Account]** et sélectionnez l’une de vos connexions existantes. Vous pouvez également choisir **[!UICONTROL New Account]** de configurer une nouvelle connexion. Renseignez les informations d’identification d’authentification de votre compte et sélectionnez **[!UICONTROL Connect to destination]**. Pour Oracle Responsys, vous pouvez choisir entre **SFTP avec mot de passe** et **SFTP avec clé SSH**. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   Pour les connexions **SFTP avec mot de passe**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
Pour les connexions **SFTP avec clé SSH**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignement des informations dans Responsys](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. In the **Setup** step, fill in the relevant information for your destination as shown below:
   * **Nom** : choisissez un nom pertinent pour votre destination.
   * **Description** : saisissez une description pour votre destination.
   * **Chemin d’accès au dossier** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme CDP en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **Format du fichier** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base de Responsys](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Cliquez sur **Créer une destination** après avoir rempli les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lors de l’[activation de segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Oracle Responsys, il est conseillé de sélectionner un identifiant unique à partir de votre [schéma d’union](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Configuration de l’importation des données dans Oracle Responsys {#import-data-into-responsys}

Après avoir connecté la plateforme CDP en temps réel à votre stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis votre emplacement de stockage dans Oracle Responsys. Pour savoir comment procéder, consultez [Importation de contacts ou de comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) dans le Centre d’aide Oracle Responsys.