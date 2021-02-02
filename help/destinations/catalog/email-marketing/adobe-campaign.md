---
keywords: e-mail ; e-mail ; e-mail ; destinations e-mail ; adobe campaign ; campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
seo-description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
translation-type: tm+mt
source-git-commit: cf2d76799c03a2ea0414aedd83b35f3ce2ca3cb5
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 44%

---


# Adobe Campaign

## Présentation

Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne. Pour plus d’informations, consultez [À propos d’Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Pour envoyer des données de segment à Adobe Campaign, vous devez tout d&#39;abord [connecter la destination](#connect-destination) dans Adobe Experience Platform, puis [configurer une importation de données](#import-data-into-campaign) à partir de votre emplacement d&#39;enregistrement dans Adobe Campaign.

## Type d&#39;exportation {#export-type}

**Basé sur**  le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [ d’activation de ](../../ui/activate-destinations.md#select-attributes)destination.

## Connexion à la destination {#connect-destination}

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez Adobe Campaign, puis **[!UICONTROL Connecter la destination]**.

![Se connecter à Adobe Campaign](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Dans le workflow Se connecter à la destination, sélectionnez le **[!UICONTROL Type de connexion]** de votre emplacement de stockage. Pour Adobe Campaign, vous pouvez sélectionner **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP avec mot de passe]**, **[!UICONTROL SFTP avec clé SSH]** et **[!UICONTROL Blob Azure]**. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter]**.

![Configuration de l’assistant Campaign](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Pour les connexions **[!UICONTROL Amazon S3]**, vous devez fournir un identifiant de clé d’accès et une clé d’accès secrète.
- Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.
- Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.
- Pour les connexions **[!UICONTROL Azure Blob]**, vous devez fournir une chaîne de connexion.

Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Clé]**. Notez que cette clé publique **doit** être écrite en tant que chaîne codée Base64.

![Renseignement des informations sur Campaign](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Dans **[!UICONTROL Informations de base]**, renseignez les informations pertinentes pour votre destination, comme illustré ci-dessous :
- **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
- **[!UICONTROL Description]** : saisissez une description pour votre destination.
- **[!UICONTROL Nom du compartiment]** : *pour les connexions S3*. Indiquez l’emplacement de votre compartiment S3 où Platform déposera vos données d’exportation au format CSV ou tabulé.
- **[!UICONTROL Chemin]** du dossier : Indiquez le chemin d’accès à l’emplacement de votre enregistrement où Platform déposera vos données d’exportation au format CSV ou tabulé.
- **[!UICONTROL Conteneur]** :  *Pour les connexions* Blob. Conteneur contenant l’objet Blob dans lequel se trouve le chemin d’accès du dossier.
- **[!UICONTROL Format du fichier]** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.

![Informations de base sur Campaign](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Cliquez sur **[!UICONTROL Créer]** après avoir renseigné les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](../../ui/activate-destinations.md) vers la destination.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md).

## Attributs de destination {#destination-attributes}

Lors de l’[activation des segments](../../ui/activate-destinations.md) vers la destination Adobe Campaign, nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](./overview.md#destination-attributes) dans la documentation des destinations de marketing par courriel.

## Données exportées {#exported-data}

Pour les destinations [!DNL Adobe Campaign], Platform crée un fichier délimité par des tabulations `.txt` ou `.csv` à l&#39;emplacement de l&#39;enregistrement que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Destinations du marketing par courriel et Destinations de l’enregistrement Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) dans le didacticiel sur l’activation des segments.

## Configurer l’importation des données dans Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Gardez à l’esprit les limites d’enregistrement SFTP, les limites d’enregistrement de base de données et les limites de profil principal conformément à votre contrat Adobe Campaign lors de cette intégration.
>- Vous devez planifier, importer et mapper vos segments exportés en Adobe Campaign à l’aide de [!DNL Campaign] workflows. Reportez-vous à [Configuration d’une importation périodique](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) dans la documentation Adobe Campaign.



Après avoir connecté Platform à votre enregistrement [!DNL Amazon S3] ou SFTP, vous devez configurer l’importation des données depuis votre emplacement d’enregistrement dans Adobe Campaign. Pour savoir comment y parvenir, consultez [Importation de données](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) dans la documentation Adobe Campaign.