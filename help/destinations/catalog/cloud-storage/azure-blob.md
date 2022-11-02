---
keywords: Azure Blob;destination Blob;s3;destination blob Azure
title: Connexion Azure Blob
description: Créez une connexion sortante active à votre stockage Azure Blob pour exporter périodiquement des fichiers de données CSV à partir de Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 32%

---

# Connexion [!DNL Azure Blob]

## Journal des modifications de destination {#changelog}

>[!IMPORTANT]
>
>Avec la version bêta de la fonctionnalité d’exportation des jeux de données et la fonctionnalité améliorée d’exportation de fichiers, vous pouvez maintenant voir deux [!DNL Azure Blob] cartes dans le catalogue des destinations.
>* Si vous exportez déjà des fichiers vers le **[!UICONTROL Azure Blob]** destination : Créez de nouveaux flux de données dans le nouveau **[!UICONTROL Azure Blob beta]** destination.
>* Si vous n’avez pas encore créé de flux de données pour la variable **[!UICONTROL Azure Blob]** destination, veuillez utiliser la nouvelle **[!UICONTROL Azure Blob beta]** carte pour exporter des fichiers vers **[!UICONTROL Azure Blob]**.


![Image des deux cartes de destination Azure Blob dans une vue côte à côte.](/help/destinations/assets/catalog/cloud-storage/blob/two-azure-blob-destination-cards.png)

Améliorations de la nouvelle [!DNL Azure Blob] carte de destination :

* [Prise en charge de l’exportation des jeux de données](/help/destinations/ui/export-datasets.md).
* Additional [options de dénomination de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Possibilité de définir des en-têtes de fichier personnalisés dans vos fichiers exportés via le [étape de mappage améliorée](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Possibilité de personnaliser le formatage des fichiers de données CSV exportés](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Présentation {#overview}

[!DNL Azure Blob] (ci-après dénommées [!DNL Blob]) est la solution de stockage d’objets Microsoft pour le cloud. Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Blob] à l’aide de la variable [!DNL Platform] de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un [!DNL Blob] , vous pouvez ignorer le reste de ce document et passer au tutoriel sur [activation des segments vers votre destination](../../ui/activate-batch-profile-destinations.md).

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Formats de fichiers pris en charge {#file-formats}

[!DNL Experience Platform] prend en charge le format de fichier suivant à exporter vers [!DNL Azure Blob]:

* Valeurs séparées par des virgules (CSV) : La prise en charge des fichiers de données exportés est actuellement limitée aux valeurs séparées par des virgules.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="Clé publique RSA"
>abstract="Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64-encoded] chaîne. Affichez un exemple de clé correctement formatée dans le lien de documentation ci-dessous."

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL Chaîne de connexion]**: la chaîne de connexion est requise pour accéder aux données de votre stockage Blob. Le [!DNL Blob] Le modèle de chaîne de connexion commence par : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Pour plus d’informations sur la configuration de votre [!DNL Blob] chaîne de connexion, voir [Configuration d’une chaîne de connexion pour un compte de stockage Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) dans la documentation de Microsoft.
* **[!UICONTROL Clé de chiffrement]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64-encoded] chaîne. Affichez un exemple d’une clé codée en base64 correctement formatée dans le lien de documentation ci-dessous. La partie centrale est raccourcie par concision.

![Image montrant un exemple d’une clé PGP correctement formatée et chiffrée en base64 dans l’interface utilisateur](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]**: saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]**: saisissez une description de cette destination.
* **[!UICONTROL Chemin du dossier]**: saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.
* **[!UICONTROL Conteneur]**: saisissez le nom du [!DNL Azure Blob Storage] conteneur à utiliser par cette destination.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## (Version bêta) Exportation de jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez la section [tutoriel sur l’exportation de jeux de données](/help/destinations/ui/export-datasets.md).

## Données exportées {#exported-data}

Pour [!DNL Azure Blob Storage] destinations, [!DNL Platform] crée une `.csv` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) dans le tutoriel sur l’activation des segments.