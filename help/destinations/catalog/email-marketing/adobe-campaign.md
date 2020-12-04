---
keywords: email;Email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
seo-description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 60%

---


# Adobe Campaign

## Présentation

Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne. Pour plus d’informations, consultez [À propos d’Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Pour envoyer des données de segment à Campaign, vous devez d’abord [connecter la destination](#connect-destination) dans la plateforme de données clients en temps réel d’Adobe, puis [configurer une importation de données](#import-data-into-campaign) à partir de l’emplacement de stockage dans Adobe Campaign.

## Type d’exportation {#export-type}

**Basé sur** le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [d’activation de](../../ui/activate-destinations.md#select-attributes)destination.

## Connexion à la destination {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select Adobe Campaign, then select **[!UICONTROL Connect destination]**.

![Se connecter à Adobe Campaign](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Dans le workflow Se connecter à la destination, sélectionnez le **[!UICONTROL Type de connexion]** de votre emplacement de stockage. Pour Adobe Campaign, vous pouvez choisir parmi **[!UICONTROL Amazon S3]**, **[!UICONTROL le protocole SFTP avec mot de passe]** et **[!UICONTROL le protocole SFTP avec clé SSH]**. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter]**.

![Configuration de l’assistant Campaign](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Pour les connexions **[!UICONTROL Amazon S3]**, vous devez fournir un identifiant de clé d’accès et une clé d’accès secrète.
- Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
- Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Clé]** . Notez que cette clé publique **doit** être écrite en tant que chaîne codée Base64.

![Renseignement des informations sur Campaign](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Dans **[!UICONTROL Informations de base]**, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
- **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
- **[!UICONTROL Description]** : saisissez une description pour votre destination.
- **[!UICONTROL Nom du compartiment]** : *pour les connexions S3*. Indiquez l’emplacement du compartiment S3 où la plateforme de données clients en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
- **[!UICONTROL Chemin d’accès au dossier]** : indiquez le chemin d’accès dans l’emplacement de stockage où la plateforme de données clients en temps réel dépose vos données d’exportation sous forme de fichiers CSV ou séparés par des tabulations.
- **[!UICONTROL Format du fichier]** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.

![Informations de base sur Campaign](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Cliquez sur **[!UICONTROL Créer]** après avoir renseigné les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](../../ui/activate-destinations.md) vers la destination.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md).

## Attributs de destination {#destination-attributes}

Lors de l’[activation des segments](../../ui/activate-destinations.md) vers la destination Adobe Campaign, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. For more information, see [Select which schema fields to use as destination attributes in your exported files](./overview.md#destination-attributes) in email marketing destinations documentation.

## Données exportées {#exported-data}

For [!DNL Adobe Campaign] destinations, Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Pour plus d’informations sur les fichiers, reportez-vous à la section Destinations du marketing par [courrier électronique et Destinations](../../ui/activate-destinations.md#esp-and-cloud-storage) d’enregistrement Cloud dans le didacticiel sur l’activation des segments.

## Configurer l’importation des données dans Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Gardez à l’esprit les limites d’enregistrement SFTP, les limites d’enregistrement de base de données et les limites de profil principal conformément à votre contrat Adobe Campaign lors de cette intégration.
>- Vous devez planifier, importer et mapper vos segments exportés en Adobe Campaign à l’aide de [!DNL Campaign] workflows. Reportez-vous à [Configuration d’une importation](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) périodique dans la documentation Adobe Campaign.



After connecting Real-time CDP to your [!DNL Amazon S3] or SFTP storage, you must set up the data import from your storage location into Adobe Campaign. To learn how to accomplish this, refer to [Importing data](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) in the Adobe Campaign documentation.