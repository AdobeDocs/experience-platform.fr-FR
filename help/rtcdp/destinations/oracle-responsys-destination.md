---
title: Destination Oracle Responsys
seo-title: Destination Oracle Responsys
description: Responsys est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.
seo-description: Responsys est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 84%

---


# [!DNL Oracle Responsys]

## Présentation

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/)[!DNL Oracle] est un outil de marketing par e-mail d’entreprise proposé par dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.

To send segment data to [!DNL Oracle Responsys], you must first [connect to the destination](#connect-destination) in Adobe Real-time Customer Data Platform, and then [set up a data import](#import-data-into-responsys) from your storage location into [!DNL Oracle Responsys].

## Connexion à la destination {#connect-destination}

1. In **[!UICONTROL Connections > Destinations]**, select [!DNL Oracle Responsys], then select **[!UICONTROL Connect destination]**.

   ![Connexion à Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. À l’étape **[!UICONTROL Authentification]**, si vous avez auparavant configuré une connexion à votre destination de stockage dans le cloud, sélectionnez **[!UICONTROL Compte existant]**, puis l’une de vos connexions existantes. Vous pouvez aussi sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion. Renseignez les informations d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**. For [!DNL Oracle Responsys], you can select between **[!UICONTROL SFTP with Password]** and **[!UICONTROL SFTP with SSH Key]**. Renseignez les informations ci-dessous en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter à la destination]**.

   Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignement des informations dans Responsys](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. À l’étape **[!UICONTROL Configuration]**, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
   * **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
   * **[!UICONTROL Description]** : saisissez une description pour votre destination.
   * **[!UICONTROL Chemin d’accès au dossier]** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme de données clients en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **[!UICONTROL Format du fichier]** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.

   ![Informations de base de Responsys](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Cliquez sur **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lors de l’[activation de segments](/help/rtcdp/destinations/activate-destinations.md)[!DNL Oracle Responsys] vers la destination , il est conseillé de sélectionner un identifiant unique à partir de votre [schéma d’union](../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Set up data import into [!DNL Oracle Responsys] {#import-data-into-responsys}

Après la connexion de la plateforme de données clients en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers [!DNL Oracle Responsys]. To learn how to accomplish this, see [Importing contacts or accounts](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in the [!DNL Oracle Responsys Help Center].