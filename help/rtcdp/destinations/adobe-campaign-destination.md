---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
seo-description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 92%

---


# Adobe Campaign

## Présentation

Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne. Pour plus d’informations, consultez [À propos d’Adobe Campaign Classic](https://docs.adobe.com/content/help/fr-FR/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Pour envoyer des données de segment à Adobe Campaign, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme de données client en temps réel Adobe, puis [configurer une importation de données](#import-data-into-campaign) à partir de l’emplacement de stockage dans Adobe Campaign.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez Adobe Campaign, puis **[!UICONTROL Se connecter à la destination]**.

   ![Se connecter à Adobe Campaign](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. In the Connect destination workflow, select the **[!UICONTROL Connection type]** for your storage location. Pour Adobe Campaign, vous pouvez choisir parmi **[!UICONTROL Amazon S3]**, **[!UICONTROL le protocole SFTP avec mot de passe]** et **[!UICONTROL le protocole SFTP avec clé SSH]**. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter]**.

   ![Configuration de l’assistant Campaign](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   For **[!UICONTROL Amazon S3]** connections, you must provide your Access Key ID and Secret Access Key.
Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignement des informations sur Campaign](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Dans **[!UICONTROL Informations de base]**, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
   * **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
   * **[!UICONTROL Description]** : saisissez une description pour votre destination.
   * **[!UICONTROL Nom du compartiment]** : *pour les connexions S3*. Indiquez l’emplacement du compartiment S3 où la plateforme CDP en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **[!UICONTROL Chemin d’accès au dossier]** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme CDP en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **[!UICONTROL Format du fichier]** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
   ![Informations de base sur Campaign](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Cliquez sur **[!UICONTROL Créer]** après avoir rempli les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Attributs de destination {#destination-attributes}

Lors de l’[activation des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Adobe Campaign, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, consultez [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) dans les destinations de marketing par e-mail.


## Configurer l’importation des données dans Adobe Campaign {#import-data-into-campaign}

Après la connexion de la plateforme CDP en temps réel au stockage Amazon S3 ou SFTP, vous devez configurer l’importation des données depuis l’emplacement de stockage vers Adobe Campaign. Pour découvrir la procédure à suivre, consultez [Importation de données](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) dans la documentation d’aide d’Adobe Campaign.