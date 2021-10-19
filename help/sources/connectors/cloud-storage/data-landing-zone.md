---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Source de la zone d’entrée de données
topic-legacy: overview
description: Découvrez comment connecter la zone d’entrée des données à Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecc9bc603bfd7b56f5f232b0d6d91eb65a901510
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 4%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] est un [!DNL Azure Blob] Interface de stockage configurée par Adobe Experience Platform, vous permettant d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour importer des fichiers dans Platform. Vous avez accès à une [!DNL Data Landing Zone] conteneur par environnement de test et le volume total de données sur tous les conteneurs est limité au total des données fournies avec votre licence Produits et Services Platform. Tous les clients de Platform et ses services d’application tels que [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], et [!DNL Real-time Customer Data Platform] sont configurés avec un [!DNL Data Landing Zone] conteneur par environnement de test. Vous pouvez lire et écrire des fichiers dans votre conteneur par le biais de [!DNL Azure Storage Explorer] ou votre interface de ligne de commande.

[!DNL Data Landing Zone] prend en charge l’authentification SAS et ses données sont protégées par la norme [!DNL Azure Blob] des mécanismes de sécurité du stockage au repos et en transit. L’authentification SAS vous permet d’accéder en toute sécurité à votre [!DNL Data Landing Zone] Conteneur via une connexion Internet publique. Aucune modification réseau n’est requise pour accéder à votre [!DNL Data Landing Zone] , ce qui signifie que vous n’avez pas besoin de configurer de listes autorisées ou de configurations inter-régions pour votre réseau. Platform applique une durée de vie stricte de sept jours sur tous les fichiers chargés dans un [!DNL Data Landing Zone] conteneur. Tous les fichiers sont supprimés au bout de sept jours.

## Contraintes de dénomination pour les fichiers et répertoires

Vous trouverez ci-dessous une liste des contraintes dont vous devez tenir compte lorsque vous nommez vos fichiers ou répertoires de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S’il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement précédés d’une séquence d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL interdits. Points de code comme `\uE000`, s’ils sont valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (tels que `0x00` to `0x1F`, `\u0081`, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (..) et deux caractères de point (.).

## Connexion [!DNL Data Landing Zone] to [!DNL Platform]

La documentation ci-dessous fournit des informations sur la manière d’importer des données de votre [!DNL Data Landing Zone] conteneur vers Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.

### Utilisation des API

- [Créez un [!DNL Data Landing Zone] Connexion source à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Création d’un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Connexion [!DNL Data Landing Zone] vers Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Création d’un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
