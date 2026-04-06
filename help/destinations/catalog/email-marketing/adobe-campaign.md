---
keywords: e-mail;E-mail;e-mail;destinations d’e-mail;adobe campaign;campaign
title: Connexion Adobe Campaign
description: Adobe Campaign est un ensemble de solutions qui permet de personnaliser les campagnes et de les diffuser via tous vos canaux en ligne et hors ligne.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 29%

---

# Connexion [!DNL Adobe Campaign]

## Vue d’ensemble {#overview}

[!DNL Adobe Campaign] est un ensemble de solutions qui vous permet de personnaliser et de diffuser des campagnes sur l’ensemble de vos canaux en ligne et hors ligne. Consultez [Prise en main de Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) pour plus d’informations.

Pour envoyer des données d’audience à [!DNL Adobe Campaign], vous devez d’abord [connecter la destination](#connect-destination) en [!DNL Adobe Experience Platform], puis [configurer une importation de données](#import-data-into-campaign) depuis l’emplacement de stockage vers [!DNL Adobe Campaign].

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
| ---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform, telles que [!DNL Adobe Journey Optimizer], </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données [!DNL Adobe Experience Platform]. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Profile-based]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Batch]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Liste autorisée d’adresses IP {#allow-list}

Lors de la configuration de destinations de marketing par e-mail avec stockage SFTP, Adobe vous recommande d’ajouter certaines plages d’adresses IP à votre place sur la liste autorisée.

Consultez la section place sur la liste autorisée des adresses IP pour les destinations SFTP[ si vous devez ajouter des adresses IP Adobe à votre place sur la liste autorisée.](../cloud-storage/ip-address-allow-list.md)

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Manage Destinations]** [Access Control](/help/access-control/home.md#permissions). Lisez la [ présentation du contrôle d’accès ](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

[!DNL Adobe Campaign] prend en charge les types de connexion suivants :

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**
* **[!UICONTROL Azure Blob]**

La méthode préférée pour envoyer des données à [!DNL Adobe Campaign] est via [!DNL Amazon S3] ou [!DNL Azure Blob].

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* Pour les connexions **[!UICONTROL Amazon S3]**, vous devez fournir vos [!UICONTROL Access Key ID] et [!UICONTROL Secret Access Key].
* Pour les connexions **[!UICONTROL SFTP with Password]**, vous devez fournir [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] et [!UICONTROL Password].
* Pour les connexions **[!UICONTROL SFTP with SSH Key]**, vous devez fournir [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] et [!UICONTROL SSH Key].
* Pour les connexions **[!UICONTROL Azure Blob]**, vous devez fournir une chaîne de connexion .
* Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Key]** . Votre clé publique doit être écrite en tant que chaîne codée en [!DNL Base64].
* **[!UICONTROL Name]** : choisissez un nom approprié pour votre destination.
* **[!UICONTROL Description]** : saisissez une description de la destination.
* **[!UICONTROL Bucket Name]** : *pour les connexions S3*. Entrez l’emplacement de votre compartiment S3 où [!DNL Experience Platform] déposerez vos données d’exportation au format CSV.
* **[!UICONTROL Folder Path]** : indiquez le chemin d’accès à l’emplacement de stockage où [!DNL Experience Platform] allez déposer vos données d’exportation au format CSV.
* **[!UICONTROL Container]** : *pour les connexions Blob*. Conteneur contenant l’objet Blob dans lequel se trouve le chemin d’accès de votre dossier.
* **[!UICONTROL File Format]** : sélectionnez **CSV** pour exporter des fichiers CSV vers votre emplacement de stockage.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**[](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}


Consultez [ Activer les données d’audience vers des destinations d’exportation de profils par lots ](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Attributs de destination {#destination-attributes}

Lors de l’activation des audiences vers cette destination, Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [ Bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail](overview.md#best-practices).

## Données exportées {#exported-data}

Pour les destinations [!DNL Adobe Campaign], [!DNL Experience Platform] crée un fichier `.csv` à l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez la section [vérifier l’activation de l’audience](../../ui/activate-batch-profile-destinations.md#verify) dans le tutoriel sur l’activation de l’audience.

## Configurer l’importation des données dans [!DNL Adobe Campaign] {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Lorsque vous effectuez cette intégration, gardez à l’esprit les limites de stockage [!DNL SFTP], les limites de stockage de la base de données et les limites de profil actif selon votre contrat de [!DNL Adobe Campaign].
>* Vous devez planifier, importer et mapper vos segments exportés dans [!DNL Adobe Campaign] à l’aide de workflows [!DNL Campaign]. Voir [Configuration d’un import récurrent](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html?lang=fr) dans [!DNL Adobe Campaign Classic] documentation et [À propos des activités de gestion des données](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) dans [!DNL Adobe Campaign Standard] documentation.
>* La méthode préférée pour envoyer des données à [!DNL Adobe Campaign] est via [!DNL Amazon S3] ou [!DNL Azure Blob].

Après la connexion de [!DNL Experience Platform] à votre stockage [!DNL Amazon S3] ou [!DNL Azure Blob], vous devez configurer l’importation des données depuis l’emplacement de stockage vers [!DNL Adobe Campaign]. Pour découvrir comment y parvenir, consultez les pages de documentation [!DNL Adobe Campaign] suivantes :

* [Prise en main de l’import et de l’export de données](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=fr) et [Chargement de données (fichier)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html?lang=fr) dans la documentation de [!DNL Adobe Campaign Classic].
* [Prise en main des processus et de la gestion des données](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) et [Chargement de fichier](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) dans la documentation de [!DNL Adobe Campaign Standard].
