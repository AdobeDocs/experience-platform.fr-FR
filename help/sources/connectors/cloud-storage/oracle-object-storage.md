---
keywords: Experience Platform;accueil;rubriques les plus consultées;stockage d’objet Oracle;stockage d’objet oracle
solution: Experience Platform
title: Présentation du connecteur source de stockage d’objet Oracle
topic-legacy: overview
description: Découvrez comment connecter le stockage d’objets d’Oracle à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

---

# Oracle Object Storage connector

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de cloud comme AWS, [!DNL Google Cloud Platform], ce qui vous permet d’importer les données de ces systèmes dans Platform pour les utiliser dans les services et destinations en aval.

Les sources de stockage dans le cloud peuvent importer vos données dans Platform sans avoir à les télécharger, les formater ou les charger. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le workflow des sources. Platform vous permet d’importer des données de [!DNL Oracle Object Storage] par lots.

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Pour plus d’informations, consultez le document [liste autorisée d’adresses IP](../../ip-address-allow-list.md) .

## Contraintes de dénomination pour les fichiers et répertoires

Voici une liste des contraintes dont vous devez tenir compte lors de l’attribution du nom à votre fichier ou répertoire de stockage dans le cloud :

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S’il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement précédés d’une séquence d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL interdits. Les points de code tels que `\uE000`, bien qu’ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode ne sont pas autorisés, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.). Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (..) et deux caractères de point (.).

## Connecter [!DNL Oracle Object Storage] à Platform

La documentation ci-dessous fournit des informations sur la manière de connecter le stockage d’objets d’Oracle à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’une connexion de base de stockage d’objets Oracle à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Explorez la structure de données et le contenu d’une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Création d’un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion source de stockage d’objet Oracle dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Création d’un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
