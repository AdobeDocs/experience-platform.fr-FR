---
keywords: Azure Blob;destination Blob;s3;destination blob Azure
title: Connexion Azure Blob
description: Créez une connexion sortante active à votre stockage Azure Blob pour exporter périodiquement des fichiers de données CSV à partir de Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 14%

---

# [!DNL Azure Blob] connection

## Présentation {#overview}

[!DNL Azure Blob] (ci-après dénommées [!DNL Blob]) est la solution de stockage d’objets Microsoft pour le cloud. Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Blob] à l’aide de la variable [!DNL Platform] de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel de l’éditeur de schémas](../../../xdm/tutorials/create-schema-ui.md): Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’un [!DNL Blob] , vous pouvez ignorer le reste de ce document et passer au tutoriel sur [activation des segments vers votre destination](../../ui/activate-batch-profile-destinations.md).

## Formats de fichiers pris en charge {#file-formats}

[!DNL Experience Platform] prend en charge le format de fichier suivant à exporter vers [!DNL Blob]:

* Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules. La prise en charge des fichiers DSV généraux sera assurée à l’avenir.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Chaîne de connexion]**: la chaîne de connexion est requise pour accéder aux données de votre stockage Blob. Le [!DNL Blob] Le modèle de chaîne de connexion commence par : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Pour plus d’informations sur la configuration de votre [!DNL Blob] chaîne de connexion, voir [Configuration d’une chaîne de connexion pour un compte de stockage Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) dans la documentation de Microsoft.

* Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.
* **[!UICONTROL Nom]**: saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]**: saisissez une description de cette destination.
* **[!UICONTROL Chemin du dossier]**: saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.
* **[!UICONTROL Conteneur]**: saisissez le nom du [!DNL Azure Blob Storage] conteneur à utiliser par cette destination.

Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.
