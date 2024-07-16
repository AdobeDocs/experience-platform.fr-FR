---
title: Présentation de Merkury Enterprise Identity Resolution Source
description: Découvrez comment connecter Merkury Enterprise Identity Resolution à Adobe Experience Platform à l’aide de l’interface utilisateur.
last-substantial-update: 2023-12-12T00:00:00Z
badge: Version bêta
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 44%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>La source [!DNL Merkury Enterprise Identity Resolution] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform prend en charge l’ingestion de données à partir d’une application de partenaire de données. [!DNL Merkury Enterprise Identity Resolution] est compatible avec les partenaires de données.

Vous pouvez utiliser [!DNL Merkury] par [!DNL Merkle] pour reconnaître davantage de visiteurs numériques, même sans l’utilisation de cookies, et offrir les expériences pertinentes et personnalisées dont votre client a besoin.

Vous pouvez utiliser l’ **ID de personne** dans le cadre de la source [!DNL Merkury] pour combiner tout ce que votre organisation sait sur un individu dans un profil complet unique. Ces détails peuvent inclure :

- comportements numériques
- préférences d’achat
- des informations d’identification telles qu’un nom, une adresse électronique, une adresse physique ou un identifiant d’appareil.

Vous pouvez formater les données ingérées sous la forme d’un fichier JSON de modèle de données d’expérience (XDM), d’un dossier XDM ou d’un fichier délimité. Chaque étape du processus est intégrée dans le travail des sources.

![Illustration du processus de traitement des données pour la source Merkury.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Contraintes de dénomination pour fichiers et répertoires

La liste suivante inclut les contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL illégaux interdits. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

## Conditions préalables

Vous devez respecter les conditions préalables suivantes avant de pouvoir commencer à utiliser la source [!DNL Merkury] :

- Vous devez effectuer votre configuration [!DNL Merkury] avec votre équipe [!DNL Merkury].
- Vous devez récupérer vos informations d’identification (clé d’accès, clé secrète et nom du compartiment) auprès de votre équipe [!DNL Merkury]. 

>[!NOTE]
>
>Un chemin d&#39;accès au fichier tel que `myBucket/folder/subfolder/subsubfolder/abc.csv` peut vous conduire à accéder uniquement à `subsubfolder/abc.csv`. Si vous souhaitez accéder au sous-dossier, vous pouvez spécifier le paramètre de compartiment comme myBucket et le folderPath comme dossier/sous-dossier pour vous assurer que l’exploration des fichiers démarre au niveau du sous-dossier et non de `subsubfolder/abc.csv`.

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration préalable nécessaire pour importer les données de votre compte [!DNL Merkury] vers Experience Platform. Vous pouvez maintenant passer au guide sur la [connexion [!DNL Merkury] à l’Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/data-partners/merkury.md).
