---
keywords: Experience Platform ; accueil ; rubriques populaires ; Enregistrement Google Cloud ; enregistrement Google Cloud
solution: Experience Platform
title: Présentation du connecteur de source d’Enregistrement Google Cloud
topic-legacy: overview
description: Découvrez comment connecter Google Cloud Enregistrement à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 5%

---

# Connecteur d’Enregistrement Google Cloud

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform] et [!DNL Azure], ce qui vous permet d’importer vos données à partir de ces systèmes.

Les sources de stockage dans le cloud peuvent introduire vos propres données dans Platform sans avoir à les télécharger, les formater ou les transférer. Les données insérées peuvent être formatées au format JSON ou Parquet conforme au modèle de données d’expérience (XDM) ou dans un format délimité. Chaque étape du processus est intégrée dans le processus des sources. Plateforme vous permet d&#39;importer des données de [!DNL Google Cloud Storage] par lots.

## LISTE AUTORISÉE d&#39;adresse IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources. Pour plus d&#39;informations, consultez la page [liste autorisée d&#39;adresse IP](../../ip-address-allow-list.md).

## Configuration requise pour la connexion de votre compte [!DNL Google Cloud Storage]

Pour vous connecter à la plate-forme, vous devez d&#39;abord activer l&#39;interopérabilité pour votre compte [!DNL Google Cloud Storage]. Pour accéder au paramètre d’interopérabilité, ouvrez [!DNL Google Cloud Platform] et sélectionnez **[!UICONTROL Paramètres]** dans l’option **[!UICONTROL Enregistrement cloud]** du panneau de navigation.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

La page **[!UICONTROL Paramètres]** s&#39;affiche. À partir de cette page, vous pouvez consulter des informations concernant votre ID de projet [!DNL Google] et des détails sur votre compte [!DNL Google Cloud Storage]. Pour accéder aux paramètres d&#39;interopérabilité, sélectionnez **[!UICONTROL Interopérabilité]** dans l&#39;en-tête supérieur.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La page **[!UICONTROL Interopérabilité]** contient des informations sur l&#39;authentification, les clés d&#39;accès et le projet par défaut associé à votre compte de service. Pour générer un nouvel ID de clé d&#39;accès et une clé d&#39;accès secret pour votre compte de service, sélectionnez **[!UICONTROL Créer une clé pour un compte de service]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Vous pouvez utiliser votre identifiant de clé d&#39;accès nouvellement généré et votre clé d&#39;accès secret pour connecter votre compte [!DNL Google Cloud Storage] à la plate-forme.

## Contraintes de nommage pour les fichiers et répertoires

Voici une liste de contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire d’enregistrement cloud.

- Les noms des composants de répertoire et de fichier ne peuvent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S&#39;il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement placés en séquence d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL non autorisés. Les points de code tels que `\uE000`, bien qu&#39;ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode dans HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (.) et deux caractères de point (.).

## Connecter [!DNL Google Cloud Storage] à la plate-forme

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Google Cloud Storage] à la plate-forme à l&#39;aide d&#39;API ou de l&#39;interface utilisateur :

### Utilisation des API

- [Création d’une connexion à la source d’Enregistrement Google Cloud à l’aide de l’API du service de flux](../../tutorials/api/create/cloud-storage/google.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion à la source d’Enregistrement Google Cloud dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configuration d’un flux de données pour une connexion d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
