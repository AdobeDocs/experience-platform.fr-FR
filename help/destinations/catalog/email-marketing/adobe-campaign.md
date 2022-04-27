---
keywords: e-mail;e-mail;destinations d’e-mail;adobe campaign;campagne
title: Connexion Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 22%

---

# Adobe Campaign Connexion 

## Présentation {#overview}

Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne. Voir [Prise en main du Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=fr) pour plus d’informations.

Pour envoyer des données de segment à Adobe Campaign, vous devez d’abord [connecter la destination](#connect-destination) dans Adobe Experience Platform, puis [configurer un import de données](#import-data-into-campaign) de votre emplacement de stockage dans Adobe Campaign.

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

Adobe Campaign prend en charge les types de connexions suivants :

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP avec mot de passe]**
* **[!UICONTROL SFTP avec clé SSH]**
* **[!UICONTROL Azure Blob]**

La méthode préconisée pour envoyer des données à Adobe Campaign consiste à : [!DNL Amazon S3] ou [!DNL Azure Blob].

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* Pour **[!UICONTROL Amazon S3]** connexions, vous devez fournir vos [!UICONTROL Accès ID de clé] et [!UICONTROL Clé d’accès secrète].
* Pour **[!UICONTROL SFTP avec mot de passe]** connexions, vous devez fournir [!UICONTROL Domaine], [!UICONTROL Port], [!UICONTROL Nom d’utilisateur], et [!UICONTROL Mot de passe].
* Pour **[!UICONTROL SFTP avec clé SSH]** connexions, vous devez fournir [!UICONTROL Domaine], [!UICONTROL Port], [!UICONTROL Nom d’utilisateur], et [!UICONTROL Clé SSH].
* Pour **[!UICONTROL Azure Blob]** connexions, vous devez fournir une chaîne de connexion.
* Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous le **[!UICONTROL Clé]** . Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.
* **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination.
* **[!UICONTROL Nom du compartiment]** : *pour les connexions S3*. Saisissez l’emplacement de votre compartiment S3 où [!DNL Platform] dépose vos données d’exportation au format CSV.
* **[!UICONTROL Chemin du dossier]**: Indiquez le chemin d’accès à l’emplacement de stockage où [!DNL Platform] dépose vos données d’exportation au format CSV.
* **[!UICONTROL Conteneur]**: *Pour les connexions Blob*. Conteneur contenant l’objet Blob dans lequel se trouve le chemin d’accès de votre dossier.
* **[!UICONTROL Format du fichier]**: Sélectionner **CSV** pour exporter des fichiers CSV vers votre emplacement de stockage.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.


Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#destination-attributes}

Lors de l’activation des segments vers cette destination, Adobe vous recommande de sélectionner un identifiant unique parmi vos [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, reportez-vous à la section [bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail](overview.md#best-practices).

## Données exportées {#exported-data}

Pour [!DNL Adobe Campaign] destinations, [!DNL Platform] crée une `.csv` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [vérification de l’activation des segments](../../ui/activate-batch-profile-destinations.md#verify) dans le tutoriel sur l’activation des segments.

## Configurer l’importation des données dans Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Gardez à l’esprit les [!DNL SFTP] limites de stockage, limites de stockage dans la base de données et principales limites de profil conformément à votre contrat Adobe Campaign lors de l’exécution de cette intégration.
>* Vous devez planifier, importer et mapper vos segments exportés dans Adobe Campaign à l’aide de [!DNL Campaign] workflows. Voir [Configurer un import récurrent](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html?lang=fr) dans la documentation Adobe Campaign Classic et [A propos des activités de Data Management](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) dans la documentation Adobe Campaign Standard.
>* La méthode préconisée pour envoyer des données à Adobe Campaign consiste à : [!DNL Amazon S3] ou [!DNL Azure Blob].


Après la connexion [!DNL Platform] à [!DNL Amazon S3] ou [!DNL Azure Blob] stockage, vous devez configurer l’importation des données depuis l’emplacement de stockage vers Adobe Campaign. Pour découvrir la procédure à suivre, consultez les pages de documentation Adobe Campaign suivantes :
* [Prise en main de l’import et de l’export de données](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=fr) et [Chargement (fichier)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html?lang=fr) dans la documentation de Adobe Campaign Classic.
* [Prise en main des processus et de la gestion des données](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) et [Chargement de fichier](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) dans la documentation Adobe Campaign Standard.
