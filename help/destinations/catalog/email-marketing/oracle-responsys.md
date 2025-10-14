---
keywords: e-mail;E-mail;e-mail;destinations d’e-mail;destination oracle responsys
title: Connexion Oracle Responsys
description: Responsys est un outil de marketing par e-mail d’entreprise proposé par Oracle dans le cadre de campagnes marketing sur plusieurs canaux. Il permet de personnaliser les interactions entre e-mails, terminaux mobiles, écrans et réseaux sociaux.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 44%

---

# Connexion [!DNL Oracle Responsys]

## Présentation {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) est un outil de marketing par e-mail d’entreprise pour les campagnes marketing cross-canal proposées par [!DNL Oracle] pour personnaliser les interactions entre les e-mails, les appareils mobiles, l’affichage et les réseaux sociaux.

Pour envoyer des données d’audience à [!DNL Oracle Responsys], vous devez d’abord [vous connecter à la destination](#connect-destination) dans Adobe Experience Platform, puis [configurer une importation de données](#import-data-into-responsys) à partir de l’emplacement de stockage vers [!DNL Oracle Responsys].

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
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

Lors de la configuration de destinations de marketing par e-mail avec stockage SFTP, Adobe vous recommande d’ajouter certaines plages d’adresses IP à votre liste autorisée de données.

Reportez-vous à la section [&#x200B; liste autorisée d’adresses IP pour les destinations SFTP &#x200B;](../cloud-storage/ip-address-allow-list.md) si vous devez ajouter des adresses IP Adobe à votre liste autorisée.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Cette destination prend en charge les types de connexion suivants :

* **[!UICONTROL SFTP avec mot de passe]**
* **[!UICONTROL SFTP avec clé SSH]**

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir :
   * [!UICONTROL Domaine]
   * [!UICONTROL Port]
   * [!UICONTROL Nom d’utilisateur]
   * [!UICONTROL Mot de passe]
* Pour les connexions **[!UICONTROL SFTP avec clé SSH]**, vous devez fournir :
   * [!UICONTROL Domaine]
   * [!UICONTROL Port]
   * [!UICONTROL Nom d’utilisateur]
   * [!UICONTROL &#x200B; Clé SSH &#x200B;]
* Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Clé]**. Votre clé publique doit être écrite en tant que chaîne codée en [!DNL Base64].
* **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination.
* **[!UICONTROL Chemin du dossier]** : indiquez le chemin d’accès à l’emplacement de stockage où Experience Platform déposera vos données d’exportation au format CSV.
* **[!UICONTROL Format de fichier]** : sélectionnez **CSV** pour exporter des fichiers CSV vers votre emplacement de stockage.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [&#x200B; Activer les données d’audience vers des destinations d’exportation de profils par lots &#x200B;](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Attributs de destination {#destination-attributes}

Lors de l’activation des audiences vers cette destination, Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [&#x200B; Bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail](overview.md#best-practices).

## Données exportées {#exported-data}

Pour les destinations [!DNL Oracle Responsys], Experience Platform crée un fichier `.csv` à l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez [vérifier l’activation de l’audience](../../ui/activate-batch-profile-destinations.md#verify) dans le tutoriel sur l’activation des audiences.

## Configurer l’importation des données dans [!DNL Oracle Responsys] {#import-data-into-responsys}

Après la connexion de [!DNL Experience Platform] à votre espace de stockage [!DNL SFTP], vous devez configurer l’importation des données depuis l’emplacement de stockage vers [!DNL Oracle Responsys]. Pour découvrir la procédure à suivre, consultez la section [Importer des contacts ou des comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) de la [!DNL Oracle Responsys Help Center].
