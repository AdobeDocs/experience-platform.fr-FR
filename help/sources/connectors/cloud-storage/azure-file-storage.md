---
keywords: Experience Platform;accueil;rubriques les plus consultées;stockage de fichiers Azure;stockage de fichiers Azure
solution: Experience Platform
title: Présentation du connecteur source de stockage de fichiers Azure
topic-legacy: overview
description: Découvrez comment connecter le stockage de fichiers Azure à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 0a5e9df6-9760-4eeb-86d5-d92d77df3d2b
source-git-commit: 446436346e3368d98eb990dba1000ac0974b84dc
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 3%

---

# Connecteur Azure File Storage

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de cloud tels qu’AWS, [!DNL Google Cloud Platform] et [!DNL Azure], ce qui vous permet d’importer vos données de ces systèmes.

Les sources de stockage dans le cloud peuvent importer vos propres données dans [!DNL Platform] sans avoir à les télécharger, les formater ou les charger. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le workflow Sources . [!DNL Platform] vous permet d’importer des données  [!DNL Azure File Storage] par lots.

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Pour plus d’informations, consultez la page [liste autorisée d’adresses IP](../../ip-address-allow-list.md) .

## Contraintes de dénomination pour les fichiers et répertoires

Voici une liste des contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S’il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement précédés d’une séquence d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL interdits. Les points de code tels que `\uE000`, bien qu’ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (..) et deux caractères de point (.).

## Connectez [!DNL Azure File Storage] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Azure File Storage] à [!DNL Platform] à l’aide des API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’une connexion de base de stockage de fichiers Azure à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Explorez la structure de données et le contenu d’une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Création d’un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion source de stockage de fichiers Azure dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Création d’un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
