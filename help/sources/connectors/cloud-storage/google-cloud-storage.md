---
keywords: Experience Platform;accueil;rubriques les plus consultées;Google Cloud Storage;stockage dans le cloud Google
solution: Experience Platform
title: Présentation du connecteur source de stockage Google Cloud
topic-legacy: overview
description: Découvrez comment connecter Google Cloud Storage à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 5%

---

# Connecteur Google Cloud Storage

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform] et [!DNL Azure], ce qui vous permet d’importer vos données de ces systèmes.

Les sources de stockage dans le cloud peuvent introduire vos propres données dans Platform sans avoir à les télécharger, les formater ou les transférer. Les données ingérées peuvent être formatées au format JSON ou Parquet conforme au modèle de données d’expérience (XDM) ou dans un format délimité. Chaque étape du processus est intégrée dans le workflow des sources. Platform vous permet d’importer des données de [!DNL Google Cloud Storage] par lots.

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Pour plus d’informations, consultez la page [liste autorisée d’adresses IP](../../ip-address-allow-list.md) .

## Configuration requise pour connecter votre compte [!DNL Google Cloud Storage]

Pour vous connecter à Platform, vous devez d’abord activer l’interopérabilité de votre compte [!DNL Google Cloud Storage]. Pour accéder au paramètre d’interopérabilité, ouvrez [!DNL Google Cloud Platform] et sélectionnez **[!UICONTROL Paramètres]** dans l’option **[!UICONTROL Stockage cloud]** du panneau de navigation.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

La page **[!UICONTROL Paramètres]** s’affiche. À partir de là, vous trouverez des informations sur l’ID de projet [!DNL Google] et des détails sur votre compte [!DNL Google Cloud Storage]. Pour accéder aux paramètres d’interopérabilité, sélectionnez **[!UICONTROL Interopérabilité]** dans l’en-tête supérieur.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La page **[!UICONTROL Interopérabilité]** contient des informations sur l’authentification, les clés d’accès et le projet par défaut associé à votre compte de service. Pour générer un nouvel identifiant de clé d’accès et une clé d’accès secrète pour votre compte de service, sélectionnez **[!UICONTROL Créer une clé pour un compte de service]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Vous pouvez utiliser votre identifiant de clé d’accès nouvellement généré et votre clé d’accès secrète pour connecter votre compte [!DNL Google Cloud Storage] à Platform.

## Contraintes de dénomination pour les fichiers et répertoires

Voici une liste des contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S’il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement précédés d’une séquence d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL interdits. Les points de code tels que `\uE000`, bien qu’ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (..) et deux caractères de point (.).

## Connecter [!DNL Google Cloud Storage] à Platform

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Google Cloud Storage] à Platform à l’aide d’API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’une connexion de base de stockage Google Cloud à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/google.md)
- [Explorez la structure de données et le contenu d’une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Création d’un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion source Google Cloud Storage dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Création d’un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
