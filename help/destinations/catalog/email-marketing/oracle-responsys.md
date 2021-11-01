---
keywords: e-mail;e-mail;destinations d’e-mail;destination de réponse d’oracle
title: Oracle de la connexion Responsys
description: Responsys est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: b0d6e02c67f2a62971332acb224c7422ea467e6c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 20%

---

# [!DNL Oracle Responsys] connection

## Présentation {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/)[!DNL Oracle] est un outil de marketing par e-mail d’entreprise proposé par dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.

Pour envoyer des données de segment à [!DNL Oracle Responsys], vous devez d’abord [se connecter à la destination](#connect-destination) dans Adobe Experience Platform, puis [configurer un import de données](#import-data-into-responsys) de votre emplacement de stockage dans [!DNL Oracle Responsys].

## Type d&#39;export {#export-type}

**Basé sur les profils** - vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), selon le choix effectué dans l’écran de sélection des attributs de la variable [workflow d&#39;activation d&#39;audience](../../ui/activate-batch-profile-destinations.md#select-attributes).

## LISTE AUTORISÉE d’adresses IP {#allow-list}

Lors de la configuration des destinations de marketing par e-mail avec stockage SFTP, Adobe vous recommande d’ajouter certaines plages d’adresses IP à votre liste autorisée.

Voir [LISTE AUTORISÉE d’adresses IP pour les destinations de stockage dans le cloud](../cloud-storage/ip-address-allow-list.md) si vous devez ajouter des adresses IP d’Adobe à votre liste autorisée.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Cette destination prend en charge les types de connexions suivants :

* **[!UICONTROL SFTP avec mot de passe]**
* **[!UICONTROL SFTP avec clé SSH]**

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* Pour **[!UICONTROL SFTP avec mot de passe]** connexions, vous devez fournir les éléments suivants :
   * [!UICONTROL Domaine]
   * [!UICONTROL Port]
   * [!UICONTROL Nom d’utilisateur]
   * [!UICONTROL Mot de passe]
* Pour **[!UICONTROL SFTP avec clé SSH]** connexions, vous devez fournir les éléments suivants :
   * [!UICONTROL Domaine]
   * [!UICONTROL Port]
   * [!UICONTROL Nom d’utilisateur]
   * [!UICONTROL Clé SSH]
* Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous le **[!UICONTROL Clé]** . Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.
* **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination.
* **[!UICONTROL Chemin du dossier]**: Indiquez le chemin d’accès dans votre emplacement de stockage où Platform dépose vos données d’exportation au format CSV.
* **[!UICONTROL Format du fichier]**: Sélectionner **CSV** pour exporter des fichiers CSV vers votre emplacement de stockage.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#destination-attributes}

Lors de l’activation des segments vers cette destination, Adobe vous recommande de sélectionner un identifiant unique parmi vos [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, reportez-vous à la section [bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail](overview.md#best-practices).

## Données exportées {#exported-data}

Pour [!DNL Oracle Responsys] destinations, Platform crée une `.csv` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [vérification de l’activation des segments](../../ui/activate-batch-profile-destinations.md#verify) dans le tutoriel sur l’activation des segments.

## Configurer l’importation des données dans [!DNL Oracle Responsys] {#import-data-into-responsys}

Après la connexion [!DNL Platform] à [!DNL SFTP] stockage, vous devez configurer l’importation des données depuis l’emplacement de stockage vers [!DNL Oracle Responsys]. Pour découvrir la procédure à suivre, reportez-vous à la section [Importer des contacts ou des comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) dans le [!DNL Oracle Responsys Help Center].
