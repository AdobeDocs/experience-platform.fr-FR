---
keywords: email;Email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
seo-description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 67%

---


# Adobe Campaign

## Présentation

Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne. Pour plus d’informations, consultez [À propos d’Adobe Campaign Classic](https://docs.adobe.com/content/help/fr-FR/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Pour envoyer des données de segment à Adobe Campaign, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme de données clients en temps réel d’Adobe, puis [configurer une importation de données](#import-data-into-campaign) à partir de l’emplacement de stockage dans Adobe Campaign.

## Type d’exportation {#export-type}

**Exportation** de profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [d’activation de](/help/rtcdp/destinations/activate-destinations.md#select-attributes)destination.

## Connexion à la destination {#connect-destination}

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select Adobe Campaign, then select **[!UICONTROL Connect destination]**.

   ![Se connecter à Adobe Campaign](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. Dans le workflow Se connecter à la destination, sélectionnez le **[!UICONTROL Type de connexion]** de votre emplacement de stockage. Pour Adobe Campaign, vous pouvez choisir parmi **[!UICONTROL Amazon S3]**, **[!UICONTROL le protocole SFTP avec mot de passe]** et **[!UICONTROL le protocole SFTP avec clé SSH]**. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter]**.

   ![Configuration de l’assistant Campaign](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Pour les connexions **[!UICONTROL Amazon S3]**, vous devez fournir un identifiant de clé d’accès et une clé d’accès secrète.
Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

   ![Renseignement des informations sur Campaign](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Dans **[!UICONTROL Informations de base]**, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
   * **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
   * **[!UICONTROL Description]** : saisissez une description pour votre destination.
   * **[!UICONTROL Nom du compartiment]** : *pour les connexions S3*. Indiquez l’emplacement du compartiment S3 où la plateforme de données clients en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **[!UICONTROL Chemin d’accès au dossier]** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme de données clients en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
   * **[!UICONTROL Format du fichier]** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.

   ![Informations de base sur Campaign](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Cliquez sur **[!UICONTROL Créer]** après avoir renseigné les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](/help/rtcdp/destinations/activate-destinations.md).

## Attributs de destination {#destination-attributes}

Lors de l’[activation des segments](/help/rtcdp/destinations/activate-destinations.md) vers la destination Adobe Campaign, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. For more information, see [Select which schema fields to use as destination attributes in your exported files](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in email marketing destinations documentation.

## Données exportées {#exported-data}

For [!DNL Adobe Campaign] destinations, Adobe Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Pour plus d’informations sur les fichiers, reportez-vous à la section Destinations du marketing par [courrier électronique et Destinations](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) d’enregistrement Cloud dans le didacticiel sur l’activation des segments.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Adobe_Campaign_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Configurer l’importation des données dans Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Gardez à l’esprit les limites d’enregistrement SFTP, les limites d’enregistrement de base de données et les limites de profil principal conformément à votre contrat Adobe Campaign lors de cette intégration.
>* Vous devez planifier, importer et mapper vos segments exportés en Adobe Campaign à l’aide de [!DNL Campaign] workflows. Reportez-vous à [Configuration d’une importation](https://docs.adobe.com/content/help/fr-FR/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#setting-up-a-périoring-import) périodique dans la documentation Adobe Campaign.



After connecting Real-time CDP to your [!DNL Amazon S3] or SFTP storage, you must set up the data import from your storage location into Adobe Campaign. To learn how to accomplish this, refer to [Importing data](https://docs.adobe.com/content/help/fr-FR/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) in the Adobe Campaign documentation.