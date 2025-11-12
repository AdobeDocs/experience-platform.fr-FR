---
keywords: Experience Platform;accueil;rubriques les plus consultées;Google Cloud Storage;google cloud storage
solution: Experience Platform
title: Présentation du connecteur Source de Google Cloud Storage
description: Découvrez comment connecter Google Cloud Storage à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 45%

---

# Connecteur Google Cloud Storage

>[!IMPORTANT]
>
>Vous pouvez désormais utiliser la source [!DNL Google Cloud Storage] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de services cloud comme AWS, [!DNL Google Cloud Platform] et [!DNL Azure], ce qui vous permet d’importer vos données à partir de ces systèmes.

Les sources de stockage dans le cloud peuvent importer vos propres données dans Experience Platform sans avoir à les télécharger, les formater ou les charger. Les données ingérées peuvent être formatées au format JSON ou Parquet conforme au modèle de données d’expérience (XDM), ou dans un format délimité. Chaque étape du processus est intégrée dans le processus Sources. Experience Platform vous permet d’importer des données de [!DNL Google Cloud Storage] par lots.

## Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Placer sur la liste autorisée Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à Experience Platform](../../ip-address-allow-list.md).

## Configuration requise pour connecter votre compte [!DNL Google Cloud Storage]

Pour vous connecter à Experience Platform, vous devez d’abord activer l’interopérabilité pour votre compte [!DNL Google Cloud Storage]. Pour accéder au paramètre d’interopérabilité, ouvrez [!DNL Google Cloud Platform] et sélectionnez **[!UICONTROL Settings]** dans l’option **[!UICONTROL Cloud Storage]** du panneau de navigation.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

La page **[!UICONTROL Settings]** s’affiche. À partir de là, vous pouvez voir des informations relatives à votre ID de projet [!DNL Google] et les détails de votre compte [!DNL Google Cloud Storage]. Pour accéder aux paramètres d’interopérabilité, sélectionnez **[!UICONTROL Interoperability]** dans l’en-tête supérieur.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

La page **[!UICONTROL Interoperability]** contient des informations sur l’authentification, les clés d’accès et le projet par défaut associé à votre compte de service. Pour générer un nouvel identifiant de clé d’accès et une clé d’accès secrète pour votre compte de service, sélectionnez **[!UICONTROL Create a Key for a Service Account]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Vous pouvez utiliser votre identifiant de clé d’accès nouvellement généré et votre clé d’accès secrète pour connecter votre compte [!DNL Google Cloud Storage] à Experience Platform.

Pour plus d’informations, consultez le guide sur la [création et gestion des clés de compte de service](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) disponible dans la documentation [!DNL Google Cloud].

## Contraintes de dénomination pour fichiers et répertoires

La liste suivante inclut les contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL illégaux interdits. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

## Connexion de [!DNL Google Cloud Storage] à Experience Platform

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Google Cloud Storage] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

- [Créer une connexion de base Google Cloud Storage à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/google.md)
- [Explorer la structure de données et le contenu d’une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Créer un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utiliser l’interface utilisateur

- [Créer une connexion source Google Cloud Storage dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Créer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
