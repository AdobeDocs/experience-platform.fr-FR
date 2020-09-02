---
keywords: Experience Platform;home;popular topics;Google Cloud Storage;google cloud storage
solution: Experience Platform
title: Connecteur d’Enregistrement Google Cloud
topic: overview
description: La documentation ci-dessous fournit des informations sur la connexion de l’Enregistrement Google Cloud à la plate-forme à l’aide des API ou de l’interface utilisateur.
translation-type: tm+mt
source-git-commit: d42351c194bb5a11f3175535de83fbd3b6ac58d2
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 4%

---


# Connecteur d’Enregistrement Google Cloud

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform]et [!DNL Azure]vous permet d’importer vos données à partir de ces systèmes.

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Platform] vous permet d’importer des données à partir de [!DNL Google Cloud Storage] lots.

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

## Configuration requise pour la connexion de votre [!DNL Google Cloud Storage] compte

Pour vous connecter à [!DNL Platform], vous devez d&#39;abord activer l&#39;interopérabilité pour votre [!DNL Google Cloud Storage] compte. Pour accéder au paramètre d’interopérabilité, ouvrez [!DNL Google Cloud Platform] et sélectionnez **[!UICONTROL Paramètres]** dans l’option **[!UICONTROL Enregistrement]** du panneau de navigation.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

The **[!UICONTROL Settings]** page appears. A partir de là, vous pouvez voir des informations concernant l&#39;ID de votre [!DNL Google] projet et des détails sur votre [!DNL Google Cloud Storage] compte. Pour accéder aux paramètres d&#39;interopérabilité, sélectionnez **[!UICONTROL Interopérabilité]** dans l&#39;en-tête supérieur.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La page **[!UICONTROL Interopérabilité]** contient des informations sur l’authentification, les clés d’accès et le projet par défaut associé à votre compte utilisateur. Si vous n&#39;avez pas encore établi de projet par défaut pour l&#39;accès interopérable, vous pouvez en configurer un dans la section **[!UICONTROL Par défaut pour l&#39;accès]** interopérable. Si un projet par défaut a déjà été établi, la section affiche la confirmation qu&#39;un projet a été défini comme projet par défaut.

Pour générer un nouvel ID de clé d’accès et une clé d’accès secret pour votre compte d’utilisateur, sélectionnez **[!UICONTROL Créer une clé]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Vous pouvez utiliser votre identifiant de clé d’accès nouvellement généré et votre clé d’accès secret pour connecter votre [!DNL Google Cloud Storage] compte à [!DNL Platform].

## Contraintes de nommage pour les fichiers et répertoires

Voici une liste de contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire d’enregistrement cloud.

- Les noms des composants de répertoire et de fichier ne peuvent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S&#39;il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement placés en séquence d’échappement : `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL non autorisés. Les points de code tels que `\uE000`, bien qu&#39;ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode dans HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles](https://www.ietf.org/rfc/rfc2616.txt) de base et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (.) et deux caractères de point (.).

## Se connecter [!DNL Google Cloud Storage] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Google Cloud Storage] à [!DNL Platform] l’aide des API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’un connecteur d’Enregistrement Google Cloud à l’aide de l’API du service de flux](../../tutorials/api/create/cloud-storage/google.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’un connecteur source Google Cloud Storage dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configuration d’un flux de données pour un connecteur d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)