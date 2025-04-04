---
keywords: Experience Platform;accueil;rubriques populaires;Blob;blob;Azure Blob;azure Blob
solution: Experience Platform
title: Présentation du connecteur Source Azure Blob
description: Découvrez comment connecter Azure Blob à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 67%

---

# Connecteur Azure Blob

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels qu’AWS, [!DNL Google Cloud Platform] et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans [!DNL Experience Platform].

Les sources de stockage dans le cloud peuvent introduire vos propres données dans [!DNL Experience Platform] sans avoir à les télécharger, les formater ou les transférer. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Experience Platform] vous permet d’importer des données de [!DNL Azure Blob] par lots.

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

>[!IMPORTANT]
>
>La source [!DNL Azure Blob] ne prend pas en charge la connectivité de la même région à Experience Platform. Si votre instance [!DNL Azure] utilise la même région réseau qu’Experience Platform, il n’est pas possible d’établir une connexion aux sources Experience Platform. Actuellement, seule la connectivité inter-régions est prise en charge.

## Contraintes de dénomination pour fichiers et répertoires

La liste suivante inclut les contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL illégaux interdits. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

## Connexion de [!DNL Azure Blob] à [!DNL Experience Platform]

La documentation ci-dessous fournit des informations sur la connexion d’Azure Blob à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

- [Créer une connexion de base Azure Blob à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/blob.md)
- [Explorer la structure de données et le contenu d’une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Créer un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utiliser l’interface utilisateur

- [Créer une connexion source Azure Blob dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/blob.md)
- [Créer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
