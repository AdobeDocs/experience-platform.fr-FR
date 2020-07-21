---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.
seo-description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 84%

---


# [!DNL Salesforce Marketing Cloud]

## Présentation

[!DNL Salesforce Marketing Cloud](https://www.salesforce.com/fr/products/marketing-cloud/email-marketing/) est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.

To send segment data to [!DNL Salesforce Marketing Cloud], you must first [connect the destination](#connect-destination) in Adobe Real-time CDP, and then [set up a data import](#import-data-into-salesforce) from your storage location into [!DNL Salesforce Marketing Cloud].

## Connexion à la destination {#connect-destination}

1. In **[!UICONTROL Connections > Destinations]**, select [!DNL Salesforce Marketing Cloud], then select **[!UICONTROL Connect destination]**.

   ![Connexion à Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. À l’étape **[!UICONTROL Authentification]**, si vous avez auparavant configuré une connexion à votre destination de stockage dans le cloud, sélectionnez **[!UICONTROL Compte existant]**, puis l’une de vos connexions existantes. Vous pouvez aussi sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion. Renseignez les informations d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**. For [!DNL Salesforce Marketing Cloud], you can select between **[!UICONTROL SFTP with Password]** and **[!UICONTROL SFTP with SSH Key]**. Renseignez les informations ci-dessous en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter à la destination]**.

   Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignement des informations sur Salesforce](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. À l’étape **[!UICONTROL Configuration]**, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
   * **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
   * **[!UICONTROL Description]** : saisissez une description pour votre destination.
   * **[!UICONTROL Chemin d’accès au dossier]** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme de données clients en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **[!UICONTROL Format du fichier]** : **[!UICONTROL CSV]** ou **[!UICONTROL séparé par des tabulations]**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.

   ![Informations de base sur Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Cliquez sur **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lors de l’[activation de segments](/help/rtcdp/destinations/activate-destinations.md)[!DNL Salesforce Marketing Cloud] vers la destination , il est conseillé de sélectionner un identifiant unique à partir de votre [schéma d’union](../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Set up data import into [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Après la connexion de la plateforme de données clients en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers [!DNL Salesforce Marketing Cloud]. To learn how to accomplish this, see [Importing Subscribers into Marketing Cloud from a File](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in the [!DNL Salesforce Help Center].