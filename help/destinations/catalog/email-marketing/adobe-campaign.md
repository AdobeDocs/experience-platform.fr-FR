---
keywords: e-mail;E-mail;e-mail;destinations d’e-mail;adobe campaign;campaign
title: Connexion Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 38%

---

# Connexion Adobe Campaign

## Présentation {#overview}

Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne. Consultez [Prise en main de Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=fr) pour plus d’informations.

Pour envoyer des données d’audience à Adobe Campaign, vous devez d’abord [connecter la destination](#connect-destination) dans Adobe Experience Platform, puis [configurer une importation de données](#import-data-into-campaign) depuis l’emplacement de stockage vers Adobe Campaign.

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Liste autorisée d’adresses IP {#allow-list}

Lors de la configuration de destinations de marketing par e-mail avec stockage SFTP, Adobe vous recommande d’ajouter certaines plages d’adresses IP à votre place sur la liste autorisée.

Consultez la section [place sur la liste autorisée des adresses IP pour les destinations SFTP](../cloud-storage/ip-address-allow-list.md) si vous devez ajouter des adresses IP Adobe à votre place sur la liste autorisée.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [ présentation du contrôle d’accès ](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Adobe Campaign prend en charge les types de connexion suivants :

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP avec mot de passe]**
* **[!UICONTROL SFTP avec clé SSH]**
* **[!UICONTROL Azure Blob]**

La méthode privilégiée pour envoyer des données à Adobe Campaign est la [!DNL Amazon S3] ou la [!DNL Azure Blob].

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* Pour les connexions **[!UICONTROL Amazon S3]**, vous devez fournir vos [!UICONTROL ID de clé d&#39;accès] et [!UICONTROL Clé d&#39;accès secrète].
* Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir [!UICONTROL Domaine], [!UICONTROL Port], [!UICONTROL Nom d’utilisateur] et [!UICONTROL Mot de passe].
* Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir [!UICONTROL Domaine], [!UICONTROL Port], [!UICONTROL Nom d’utilisateur] et [!UICONTROL Clé SSH].
* Pour les connexions **[!UICONTROL Azure Blob]**, vous devez fournir une chaîne de connexion.
* Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Clé]**. Votre clé publique doit être écrite en tant que chaîne codée en [!DNL Base64].
* **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination.
* **[!UICONTROL Nom du compartiment]** : *pour les connexions S3*. Entrez l’emplacement de votre compartiment S3 où [!DNL Experience Platform] déposerez vos données d’exportation au format CSV.
* **[!UICONTROL Chemin du dossier]** : indiquez le chemin d’accès à l’emplacement de stockage où [!DNL Experience Platform] déposerez vos données d’exportation sous forme de fichiers CSV.
* **[!UICONTROL Conteneur]** : *pour les connexions Blob*. Conteneur contenant l’objet Blob dans lequel se trouve le chemin d’accès de votre dossier.
* **[!UICONTROL Format de fichier]** : sélectionnez **CSV** pour exporter des fichiers CSV vers votre emplacement de stockage.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}


Consultez [ Activer les données d’audience vers des destinations d’exportation de profils par lots ](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Attributs de destination {#destination-attributes}

Lors de l’activation des audiences vers cette destination, Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [ Bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail](overview.md#best-practices).

## Données exportées {#exported-data}

Pour les destinations [!DNL Adobe Campaign], [!DNL Experience Platform] crée un fichier `.csv` à l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez la section [vérifier l’activation de l’audience](../../ui/activate-batch-profile-destinations.md#verify) dans le tutoriel sur l’activation de l’audience.

## Configurer l’importation des données dans Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Lorsque vous effectuez cette intégration, gardez à l’esprit les limites de stockage [!DNL SFTP], les limites de stockage de la base de données et les limites de profil actif conformément à votre contrat Adobe Campaign.
>* Vous devez planifier, importer et mapper vos segments exportés dans Adobe Campaign à l’aide de workflows [!DNL Campaign]. Consultez les sections [Configuration d’un import récurrent](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html?lang=fr) dans la documentation de Adobe Campaign Classic et [À propos des activités de gestion des données](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html?lang=fr) dans la documentation de Adobe Campaign Standard.
>* La méthode privilégiée pour envoyer des données à Adobe Campaign est la [!DNL Amazon S3] ou la [!DNL Azure Blob].

Après la connexion de [!DNL Experience Platform] à votre stockage [!DNL Amazon S3] ou [!DNL Azure Blob], vous devez configurer l’importation des données depuis l’emplacement de stockage vers Adobe Campaign. Pour découvrir comment y parvenir, consultez les pages de documentation d’Adobe Campaign suivantes :
* [Prise en main de l’import et de l’export de données](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=fr) et [Chargement de données (fichier)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html?lang=fr) dans la documentation de Adobe Campaign Classic.
* [Prise en main des processus et de la gestion des données](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html?lang=fr) et [Chargement de fichier](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html?lang=fr) dans la documentation de Adobe Campaign Standard.
