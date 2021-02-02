---
keywords: Experience Platform ; accueil ; rubriques populaires ; Enregistrement Google Cloud ; enregistrement Google Cloud
solution: Experience Platform
title: Connecteur d’Enregistrement Google Cloud
topic: overview
description: La documentation ci-dessous fournit des informations sur la connexion de l’Enregistrement Google Cloud à la plate-forme à l’aide des API ou de l’interface utilisateur.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 4%

---


# Connecteur d’Enregistrement Google Cloud

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform] et [!DNL Azure], ce qui vous permet d’importer vos données à partir de ces systèmes.

Les sources d’enregistrement Cloud peuvent importer vos propres données dans [!DNL Platform] sans avoir à télécharger, mettre en forme ou télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Platform] vous permet d’importer des données  [!DNL Google Cloud Storage] par lots.

## LISTE AUTORISÉE d&#39;adresse IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources. Pour plus d&#39;informations, consultez la page [liste autorisée d&#39;adresse IP](../../ip-address-allow-list.md).

## Configuration requise pour la connexion de votre compte [!DNL Google Cloud Storage]

Pour vous connecter à [!DNL Platform], vous devez d&#39;abord activer l&#39;interopérabilité pour votre compte [!DNL Google Cloud Storage]. Pour accéder au paramètre d&#39;interopérabilité, ouvrez [!DNL Google Cloud Platform] et sélectionnez **[!UICONTROL Paramètres]** dans l&#39;option **[!UICONTROL Enregistrement]** du panneau de navigation.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

La page **[!UICONTROL Paramètres]** s&#39;affiche. À partir de cette page, vous pouvez consulter des informations concernant votre ID de projet [!DNL Google] et des détails sur votre compte [!DNL Google Cloud Storage]. Pour accéder aux paramètres d&#39;interopérabilité, sélectionnez **[!UICONTROL Interopérabilité]** dans l&#39;en-tête supérieur.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La page **[!UICONTROL Interopérabilité]** contient des informations sur l&#39;authentification, les clés d&#39;accès et le projet par défaut associé à votre compte utilisateur. Si vous n&#39;avez pas encore établi un projet par défaut pour l&#39;accès interopérable, vous pouvez en configurer un dans la section **[!UICONTROL Projet par défaut pour l&#39;accès interopérable]**. Si un projet par défaut a déjà été établi, la section affiche la confirmation qu&#39;un projet a été défini comme projet par défaut.

Pour générer un nouvel ID de clé d’accès et une clé d’accès secret pour votre compte utilisateur, sélectionnez **[!UICONTROL Créer une clé]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Vous pouvez utiliser votre identifiant de clé d&#39;accès et votre clé d&#39;accès secret nouvellement générés pour connecter votre compte [!DNL Google Cloud Storage] à [!DNL Platform].

## Contraintes de nommage pour les fichiers et répertoires

Voici une liste de contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire d’enregistrement cloud.

- Les noms des composants de répertoire et de fichier ne peuvent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S&#39;il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement placés en séquence d’échappement : `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL non autorisés. Les points de code tels que `\uE000`, bien qu&#39;ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode dans HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (.) et deux caractères de point (.).

## Connecter [!DNL Google Cloud Storage] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Google Cloud Storage] à [!DNL Platform] à l&#39;aide d&#39;API ou de l&#39;interface utilisateur :

### Utilisation des API

- [Création d’un connecteur d’Enregistrement Google Cloud à l’aide de l’API du service de flux](../../tutorials/api/create/cloud-storage/google.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’un connecteur source Google Cloud Storage dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configuration d’un flux de données pour un connecteur d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)