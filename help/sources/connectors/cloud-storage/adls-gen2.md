---
keywords: Experience Platform;accueil;rubriques populaires;Azure Data Lake Storage Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Présentation du connecteur source Azure Data Lake Storage Gen2
topic-legacy: overview
description: Découvrez comment connecter Azure Data Lake Storage Gen2 à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 3%

---

# Connecteur Azure Data Lake Storage Gen2

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform] et [!DNL Azure], ce qui vous permet d’importer vos données de ces systèmes.

Les sources de stockage dans le cloud peuvent importer vos propres données dans [!DNL Platform] sans avoir à les télécharger, les formater ou les charger. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le workflow Sources . [!DNL Platform] vous permet d’importer des données depuis  [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) par lots.

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Pour plus d’informations, consultez la page [liste autorisée d’adresses IP](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Le connecteur source [!DNL Azure Data Lake Storage Gen2] ne prend actuellement pas en charge la connectivité de la même région à Platform. Cela signifie que si votre instance Azure utilise la même région réseau que Platform, une connexion aux sources Platform ne peut pas être établie. Actuellement, seule la connectivité inter-régions est prise en charge. Pour plus d’informations, contactez votre gestionnaire de compte d’Adobe.

## Contraintes de dénomination pour les fichiers et répertoires

Voici une liste des contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S’il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement précédés d’une séquence d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL interdits. Les points de code tels que `\uE000`, bien qu’ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (..) et deux caractères de point (.).

## Connectez [!DNL Azure Data Lake Storage Gen2] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Azure Data Lake Storage Gen2] à [!DNL Platform] à l’aide des API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’une connexion de base ADLS-Gen2 à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Explorez la structure de données et le contenu d’une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Création d’un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion source ADLS-Gen2 dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Création d’un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
