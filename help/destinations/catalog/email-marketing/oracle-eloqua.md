---
keywords: e-mail;e-mail;destinations d’e-mail;oracle eloqua;oracle
title: Oracle de la connexion Eloqua
description: Oracle Eloqua est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 26%

---

# [!DNL Oracle Eloqua] connection

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/)[!DNL Oracle] est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par , qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.

Pour envoyer des données de segment à [!DNL Oracle Eloqua], vous devez d’abord [connecter la destination](#connect-destination) dans Adobe Experience Platform, puis [configurer une importation de données](#import-data-into-eloqua) à partir de l’emplacement de stockage dans [!DNL Oracle Eloqua].

## Type d&#39;export {#export-type}

**Basé sur un profil**  : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse email, numéro de téléphone, nom), tel que sélectionné dans l&#39;écran de sélection des attributs du workflow d&#39;activation de l&#39; [audience](../../ui/activate-batch-profile-destinations.md#select-attributes).

## LISTE AUTORISÉE d’adresses IP {#allow-list}

Lors de la configuration des destinations de marketing par e-mail avec stockage SFTP, Adobe vous recommande d’ajouter certaines plages d’adresses IP à votre liste autorisée.

Reportez-vous à la [liste autorisée d’adresses IP pour les destinations de stockage dans le cloud](../cloud-storage/ip-address-allow-list.md) si vous devez ajouter des adresses IP d’Adobe à votre liste autorisée.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Cette destination prend en charge les types de connexions suivants :

* **[!UICONTROL SFTP avec mot de passe]**
* **[!UICONTROL SFTP avec clé SSH]**

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir :
   * [!UICONTROL Domaine]
   * [!UICONTROL Port]
   * [!UICONTROL Nom d’utilisateur]
   * [!UICONTROL Mot de passe]
* Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir :
   * [!UICONTROL Domaine]
   * [!UICONTROL Port]
   * [!UICONTROL Nom d’utilisateur]
   * [!UICONTROL Clé SSH]

* Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Clé]** . Votre clé publique doit être écrite en tant que chaîne codée [!DNL Base64].
* **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination.
* **[!UICONTROL Chemin du dossier]** : Indiquez le chemin d’accès dans l’emplacement de stockage où Platform dépose vos données d’exportation au format CSV ou dans des fichiers séparés par des tabulations.
* **[!UICONTROL Format du fichier]** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de profil de lot](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#destination-attributes}

Lors de l’activation des segments vers cette destination, Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, reportez-vous aux [bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail](overview.md#best-practices).

## Données exportées {#exported-data}

Pour les destinations [!DNL Oracle Eloqua], Platform crée un fichier `.csv` délimité par des tabulations dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Vérification de l’activation du segment](../../ui/activate-batch-profile-destinations.md#verify) dans le tutoriel sur l’activation du segment.

## Configurer l’importation des données dans [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Après la connexion de [!DNL Platform] à votre stockage [!DNL SFTP], vous devez configurer l’importation des données depuis l’emplacement de stockage vers [!DNL Oracle Eloqua]. Pour découvrir la procédure à suivre, voir [Importation de contacts ou de comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) dans la section [!DNL Oracle Eloqua Help Center].
