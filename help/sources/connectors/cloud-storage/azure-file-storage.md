---
keywords: Experience Platform ; accueil ; rubriques populaires ; Enregistrement de fichiers Azure ; enregistrement de fichiers azurés
solution: Experience Platform
title: Présentation du connecteur source d'Enregistrement de fichiers Azure
topic: aperçu
description: Découvrez comment connecter Azure File Enregistrement à Adobe Experience Platform à l'aide d'API ou de l'interface utilisateur.
translation-type: tm+mt
source-git-commit: 7fc99214272d2ce743b3666826c66f5d65e4d2ca
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 2%

---


# (Bêta) Connecteur d&#39;Enregistrement de fichier Azure

>[!NOTE]
>
>Le connecteur d&#39;Enregistrement de fichiers Azure est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../home.md#terms-and-conditions).

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform] et [!DNL Azure], ce qui vous permet d’importer vos données à partir de ces systèmes.

Les sources d’enregistrement Cloud peuvent importer vos propres données dans [!DNL Platform] sans avoir à télécharger, mettre en forme ou télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Platform] vous permet d’importer des données  [!DNL Azure File Storage] par lots.

## LISTE AUTORISÉE d&#39;adresse IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources. Pour plus d&#39;informations, consultez la page [liste autorisée d&#39;adresse IP](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Le connecteur source [!DNL Azure File Storage] ne prend actuellement pas en charge la connectivité de la même région à la plate-forme. Cela signifie que si votre instance Azure utilise la même région réseau que Platform, une connexion aux sources de la plateforme ne peut pas être établie. Actuellement, seule la connectivité inter-régions est prise en charge. Pour plus d&#39;informations, contactez votre gestionnaire de compte d&#39;Adobe.

## Contraintes de nommage pour les fichiers et répertoires

Voici une liste de contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire d’enregistrement cloud.

- Les noms des composants de répertoire et de fichier ne peuvent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S&#39;il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement placés en séquence d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL non autorisés. Les points de code tels que `\uE000`, bien qu&#39;ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode dans HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (.) et deux caractères de point (.).

## Connecter [!DNL Azure File Storage] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Azure File Storage] à [!DNL Platform] à l&#39;aide d&#39;API ou de l&#39;interface utilisateur :

### Utilisation des API

- [Création d&#39;une connexion source d&#39;Enregistrement de fichiers Azure à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d&#39;une connexion source d&#39;Enregistrement de fichiers Azure dans l&#39;interface utilisateur](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Configuration d’un flux de données pour une connexion d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)