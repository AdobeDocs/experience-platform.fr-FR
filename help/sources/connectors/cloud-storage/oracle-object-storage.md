---
keywords: Experience Platform ; accueil ; rubriques populaires ; Enregistrement d'objet Oracle ; enregistrement d'objet oracle
solution: Experience Platform
title: Présentation du connecteur de source d'Enregistrement d'objets d'Oracle
topic: aperçu
description: Découvrez comment connecter l’Enregistrement d’objet d’Oracle à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
translation-type: tm+mt
source-git-commit: 04c605aedd4c52b54d0f075c169ce919650cdee9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 3%

---


# Connecteur d&#39;Enregistrement d&#39;objet Oracle

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform], ce qui vous permet d’importer des données de ces systèmes dans Platform en vue de les utiliser dans les services et destinations en aval.

Les sources d’enregistrement Cloud peuvent importer vos données dans la plate-forme sans avoir à télécharger, mettre en forme ou télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus des sources. Plateforme vous permet d&#39;importer des données de [!DNL Oracle Object Storage] par lots.

## LISTE AUTORISÉE d&#39;adresse IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources. Pour plus d&#39;informations, consultez le document [liste autorisée d&#39;adresse IP](../../ip-address-allow-list.md).

## Contraintes de nommage pour les fichiers et répertoires

Voici une liste de contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire d’enregistrement cloud :

- Les noms des composants de répertoire et de fichier ne peuvent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S&#39;il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement placés en séquence d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL non autorisés. Les points de code tels que `\uE000`, bien qu&#39;ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode ne sont pas autorisés, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.). Pour les règles régissant les chaînes Unicode dans HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (.) et deux caractères de point (.).

## Connecter [!DNL Oracle Object Storage] à la plate-forme

La documentation ci-dessous fournit des informations sur la connexion de l’Enregistrement d’objet d’Oracle à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’une connexion source d’Enregistrement d’objet d’Oracle à l’aide de l’API du service de flux](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion à la source d’Enregistrement d’objet d’Oracle dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Configuration d’un flux de données pour une connexion d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)