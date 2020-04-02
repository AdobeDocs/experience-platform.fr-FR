---
title: Destination Oracle Responsys
seo-title: Destination Oracle Responsys
description: Responsys est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.
seo-description: Responsys est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Oracle Responsys

## Présentation

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.

To send segment data to Oracle Responsys, you must first [connect to the destination](#connect-destination) in Adobe Real-time Customer Data Platform, and then [set up a data import](#import-data-into-responsys) from your storage location into Oracle Responsys.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connections > Destinations]** Oracle Responsys, sélectionnez **[!UICONTROL Connect destination]**.

   ![Connexion à Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. Au cours de l’ **[!UICONTROL Authentication]** étape, si vous aviez précédemment configuré une connexion à votre cloud  destination , sélectionnez **[!UICONTROL Existing Account]** et sélectionnez l’une de vos connexions existantes. Vous pouvez également choisir **[!UICONTROL New Account]** de configurer une nouvelle connexion. Renseignez les informations d’identification d’authentification de votre compte et sélectionnez **[!UICONTROL Connect to destination]**. Pour Oracle Responsys, vous pouvez sélectionner entre **[!UICONTROL SFTP with Password]** et **[!UICONTROL SFTP with SSH Key]**. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   For **[!UICONTROL SFTP with Password]** connections, you must provide Domain, Port, Username, and Password.
Pour **[!UICONTROL SFTP with SSH Key]** les connexions, vous devez fournir Domaine, Port, Nom d’utilisateur et Clé SSH.

   ![Renseignement des informations dans Responsys](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Name]**: Choisissez un nom approprié pour votre destination.
   * **[!UICONTROL Description]** : saisissez une description pour votre destination.
   * **[!UICONTROL Folder Path]**: Indiquez le chemin d’accès dans votre  de  où le CDP en temps réel déposera vos données d’exportation au format CSV ou tabulé.
   * **[!UICONTROL File Format]**: **CSV** ou **TAB_DELIMITED**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base de Responsys](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Cliquez **[!UICONTROL Create destination]** après avoir rempli les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lors de l’[activation de segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Oracle Responsys, il est conseillé de sélectionner un identifiant unique à partir de votre [schéma d’union](../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Configuration de l’importation des données dans Oracle Responsys {#import-data-into-responsys}

Après avoir connecté la plateforme CDP en temps réel à votre stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis votre emplacement de stockage dans Oracle Responsys. Pour savoir comment procéder, consultez [Importation de contacts ou de comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) dans le Centre d’aide Oracle Responsys.