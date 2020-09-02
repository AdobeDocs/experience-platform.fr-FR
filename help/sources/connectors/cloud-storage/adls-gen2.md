---
keywords: Experience Platform;home;popular topics;Azure Data Lake Storage Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Connecteur Azure Data Lake Enregistrement Gen2
topic: overview
description: La documentation ci-dessous fournit des informations sur la façon de connecter Azure Data Lake Enregistrement Gen2 à Platform à l'aide d'API ou de l'interface utilisateur.
translation-type: tm+mt
source-git-commit: d42351c194bb5a11f3175535de83fbd3b6ac58d2
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 3%

---


# Connecteur Azure Data Lake Enregistrement Gen2

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform]et [!DNL Azure]vous permet d’importer vos données à partir de ces systèmes.

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Platform] vous permet d’importer des données à partir de [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) par lots.

## LISTE AUTORISÉE d&#39;adresse IP

Les adresses IP suivantes doivent être ajoutées à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources.

### Région est-américaine

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Région de l&#39;Europe occidentale

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australie-Est

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## Contraintes de nommage pour les fichiers et répertoires

Voici une liste de contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire d’enregistrement cloud.

- Les noms des composants de répertoire et de fichier ne peuvent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S&#39;il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement placés en séquence d’échappement : `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL non autorisés. Les points de code tels que `\uE000`, bien qu&#39;ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode dans HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles](https://www.ietf.org/rfc/rfc2616.txt) de base et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (.) et deux caractères de point (.).

## Se connecter [!DNL Azure Data Lake Storage Gen2] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Azure Data Lake Storage Gen2] à [!DNL Platform] l’aide des API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’un connecteur ADLS-Gen2 à l’aide de l’API du service de flux](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

## Utilisation de l’interface utilisateur

- [Création d’un connecteur source ADLS-Gen2 dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Configuration d’un flux de données pour un connecteur d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)