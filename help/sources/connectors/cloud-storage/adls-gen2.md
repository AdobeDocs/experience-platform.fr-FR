---
title: Présentation du connecteur Source Azure Data Lake Storage Gen2
description: Découvrez comment connecter Azure Data Lake Storage Gen2 à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: f879f2a627e55db96a89796b9f3308744bf93f67
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 62%

---

# Connecteur Azure Data Lake Storage Gen2

Adobe Experience Platform fournit une connectivité native pour les fournisseurs cloud tels qu’AWS, [!DNL Google Cloud Platform] et [!DNL Azure], ce qui vous permet d’importer vos données à partir de ces systèmes.

Les sources de stockage dans le cloud peuvent importer vos propres données dans Experience Platform sans avoir à les télécharger, les formater ou les charger. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. Experience Platform vous permet d’importer des données de [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) par lots.

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

>[!IMPORTANT]
>
>La source [!DNL Azure Data Lake Storage Gen2] ne prend pas en charge la connectivité de la même région à l’Experience Platform. Si votre instance Azure utilise la même région de réseau qu’Experience Platform, une connexion aux sources Experience Platform ne peut pas être établie. N’utilisez pas les régions Azure East US 2, Azure West Europe et Azure Australia East lors de la configuration de votre source [!DNL Azure Data Lake Storage Gen2]. Actuellement, seule la connectivité inter-régions est prise en charge.

## Contraintes de dénomination pour fichiers et répertoires

La liste suivante inclut les contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL illégaux interdits. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

## Connecter [!DNL Azure Data Lake Storage Gen2] à l’Experience Platform

>[!NOTE]
>
>L’entité de service utilisée dans la création d’un compte [!DNL Azure Data Lake Storage Gen2] doit avoir au moins le rôle **Reader de données Blob de stockage** attribué à partir du contrôle d’accès (IAM).

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Azure Data Lake Storage Gen2] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

- [Créer une connexion de base  [!DNL Azure Data Lake Storage Gen2] à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Explorer la structure de données et le contenu d’une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Créer un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utiliser l’interface utilisateur

- [Création d’une connexion source  [!DNL Azure Data Lake Storage Gen2] dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Créer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
