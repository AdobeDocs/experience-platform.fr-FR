---
keywords: e-mail;e-mail;destinations d’e-mail;adobe campaign;campagne
title: Connexion Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 18%

---

# Connexion Adobe Campaign

## Présentation {#overview}

Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne. Voir [Prise en main de Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=fr) pour plus d’informations.

Pour envoyer des données de segment à Adobe Campaign, vous devez d’abord [connecter la destination](#connect-destination) dans Adobe Experience Platform, puis [configurer une importation de données](#import-data-into-campaign) à partir de l’emplacement de stockage dans Adobe Campaign.

## Type d&#39;export {#export-type}

**Basé sur un profil**  : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse email, numéro de téléphone, nom), tel que sélectionné dans l&#39;étape  **[!UICONTROL Sélectionner les]** attributs du workflow d&#39;activation de l&#39; [audience](../../ui/activate-batch-profile-destinations.md#select-attributes).

## LISTE AUTORISÉE d’adresses IP {#allow-list}

Lors de la configuration des destinations de marketing par e-mail avec stockage SFTP, Adobe vous recommande d’ajouter certaines plages d’adresses IP à votre liste autorisée.

Reportez-vous à la [liste autorisée d’adresses IP pour les destinations de stockage dans le cloud](../cloud-storage/ip-address-allow-list.md) si vous devez ajouter des adresses IP d’Adobe à votre liste autorisée.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Adobe Campaign prend en charge les types de connexions suivants :

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP avec mot de passe]**
* **[!UICONTROL SFTP avec clé SSH]**
* **[!UICONTROL Azure Blob]**

La méthode préférée pour envoyer des données à Adobe Campaign est [!DNL Amazon S3] ou [!DNL Azure Blob].

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* Pour les connexions **[!UICONTROL Amazon S3]**, vous devez fournir votre [!UICONTROL identifiant de clé d’accès] et [!UICONTROL clé d’accès secrète].
* Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir [!UICONTROL Domaine], [!UICONTROL Port], [!UICONTROL Nom d’utilisateur] et [!UICONTROL Mot de passe].
* Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Nom d’utilisateur] et [!UICONTROL Clé SSH].
* Pour les connexions **[!UICONTROL Azure Blob]**, vous devez fournir une chaîne de connexion.
* Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Clé]** . Votre clé publique doit être écrite en tant que chaîne codée [!DNL Base64].
* **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination.
* **[!UICONTROL Nom du compartiment]** : *pour les connexions S3*. Saisissez l’emplacement de votre compartiment S3 où [!DNL Platform] dépose vos données d’exportation au format CSV ou séparé par des tabulations.
* **[!UICONTROL Chemin du dossier]** : Indiquez le chemin d’accès dans l’emplacement de stockage où  [!DNL Platform] déposer vos données d’exportation au format CSV ou les fichiers délimités par des tabulations.
* **[!UICONTROL Conteneur]** :  *Pour les connexions Blob*. Conteneur contenant l’objet Blob dans lequel se trouve le chemin d’accès de votre dossier.
* **[!UICONTROL Format du fichier]** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de profil de lot](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#destination-attributes}

Lors de l’activation des segments vers cette destination, Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, reportez-vous aux [bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail](overview.md#best-practices).

## Données exportées {#exported-data}

Pour les destinations [!DNL Adobe Campaign], [!DNL Platform] crée un fichier `.csv` délimité par des tabulations dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Vérification de l’activation du segment](../../ui/activate-batch-profile-destinations.md#verify) dans le tutoriel sur l’activation du segment.

## Configurer l’importation des données dans Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Gardez à l’esprit les limites de stockage [!DNL SFTP], les limites de stockage dans la base de données et les principales limites de profil conformément à votre contrat Adobe Campaign lors de l’exécution de cette intégration.
>* Vous devez planifier, importer et mapper vos segments exportés dans Adobe Campaign à l’aide de workflows [!DNL Campaign]. Reportez-vous aux sections [Configuration d’un import récurrent](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html?lang=fr) dans la documentation Adobe Campaign Classic et [À propos des activités de Data Management](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) dans la documentation Adobe Campaign Standard.
>* La méthode préférée pour envoyer des données à Adobe Campaign est [!DNL Amazon S3] ou [!DNL Azure Blob].


Après avoir connecté [!DNL Platform] à votre [!DNL Amazon S3] ou [!DNL Azure Blob] stockage, vous devez configurer l’importation des données depuis votre emplacement de stockage vers Adobe Campaign. Pour découvrir la procédure à suivre, consultez les pages de documentation Adobe Campaign suivantes :
* [Prise en main de l’import et de l’](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=fr) export de données et  [Chargement (fichier)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html)  dans la documentation Adobe Campaign Classic.
* [Prise en main des processus et de la ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) gestion des données et  [Chargement ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) de fichier dans la documentation Adobe Campaign Standard.
