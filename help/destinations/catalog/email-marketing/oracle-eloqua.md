---
keywords: e-mail;e-mail;destinations d’e-mail;oracle eloqua;oracle
title: Connexion Orale Eloqua
description: Oracle Eloqua est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 28%

---

# Connexion [!DNL Oracle Eloqua]

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/)[!DNL Oracle] est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par , qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.

Pour envoyer des données de segment à [!DNL Oracle Eloqua], vous devez d’abord [connecter la destination](#connect-destination) dans Adobe Experience Platform, puis [configurer un import de données](#import-data-into-eloqua) de votre emplacement de stockage dans [!DNL Oracle Eloqua].

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Liste autorisée d’adresses IP {#allow-list}

Lors de la configuration des destinations de marketing par e-mail avec stockage SFTP, Adobe vous recommande d’ajouter certaines plages d’adresses IP à votre liste autorisée.

Voir [LISTE AUTORISÉE d’adresses IP pour les destinations de stockage dans le cloud](../cloud-storage/ip-address-allow-list.md) si vous devez ajouter des adresses IP d’Adobe à votre liste autorisée.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Cette destination prend en charge les types de connexions suivants :

* **[!UICONTROL SFTP avec mot de passe]**
* **[!UICONTROL SFTP avec clé SSH]**

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

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

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#destination-attributes}

Lors de l’activation des segments vers cette destination, Adobe vous recommande de sélectionner un identifiant unique parmi vos [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, reportez-vous à la section [bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail](overview.md#best-practices).

## Données exportées {#exported-data}

Pour [!DNL Oracle Eloqua] destinations, Platform crée une `.csv` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [vérification de l’activation des segments](../../ui/activate-batch-profile-destinations.md#verify) dans le tutoriel sur l’activation des segments.

## Configurer l’importation des données dans [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Après la connexion [!DNL Platform] à [!DNL SFTP] stockage, vous devez configurer l’importation des données depuis l’emplacement de stockage vers [!DNL Oracle Eloqua]. Pour découvrir la procédure à suivre, reportez-vous à la section [Importer des contacts ou des comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) dans le [!DNL Oracle Eloqua Help Center].
