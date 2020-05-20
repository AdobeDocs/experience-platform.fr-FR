---
title: Destination Oracle Eloqua
seo-title: Destination Oracle Eloqua
description: Oracle Eloqua est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
seo-description: Oracle Eloqua est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 81%

---


# Oracle Eloqua

## Présentation

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.

Pour envoyer des données de segment à Oracle Eloqua, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme de données client en temps réel Adobe, puis [configurer une importation de données](#import-data-into-eloqua) à partir de l’emplacement de stockage dans Oracle Eloqua.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez Oracle Eloqua, puis **[!UICONTROL Se connecter à la destination]**.

   ![Se connecter à Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. In the **[!UICONTROL Authentication]** step, if you had previously set up a connection to your cloud storage destination, select **[!UICONTROL Existing Account]** and select one of your existing connections. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion. Renseignez les informations d’identification d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**. Pour Oracle Eloqua, vous pouvez choisir parmi **[!UICONTROL le protocole SFTP avec mot de passe]** et **[!UICONTROL le protocole SFTP avec clé SSH]**. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Configurer l’assistant Oracle Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
   * **[!UICONTROL Description]** : saisissez une description pour votre destination.
   * **[!UICONTROL Chemin d’accès au dossier]** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme CDP en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **[!UICONTROL Format du fichier]** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base sur Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Cliquez sur **[!UICONTROL Créer une destination]** après avoir rempli les champs ci-dessus. Your destination is now created and you can [activate segments](/help/rtcdp/destinations/activate-destinations.md) to the destination.

## Attributs de destination

Lors de l’[activation des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Oracle Eloqua, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.

## Configurer l’importation des données dans Oracle Eloqua {#import-data-into-eloqua}

Après la connexion de la plateforme CDP en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers Oracle Eloqua. Pour découvrir la procédure à suivre, consultez [Importation de contacts ou comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) du centre d’aide d’Oracle Eloqua.