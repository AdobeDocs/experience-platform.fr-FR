---
title: Ingestion de données Acxiom
description: Découvrez comment ingérer  [!DNL Acxiom]  données dans Real-Time Customer Data Platform, enrichir les profils propriétaires, améliorer les audiences et les activer sur l’ensemble des canaux marketing.
exl-id: 3bbbe4e1-5e34-4104-bf39-2c452865b807
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 32%

---

# [!DNL Acxiom Data Ingestion]

Utilisez la source de [!DNL Acxiom Data Ingestion] pour ingérer des données [!DNL Acxiom] dans Real-Time Customer Data Platform et enrichir les profils propriétaires. Ensuite, vous pouvez utiliser vos profils propriétaires enrichis de [!DNL Acxiom] pour améliorer les audiences et les activer sur l’ensemble des canaux marketing.

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

Lisez le document ci-dessous pour plus d’informations sur la configuration de votre compte source [!DNL Acxiom Data Ingestion].

## Conditions préalables {#prerequisites}

Pour connecter votre compte [!DNL Acxiom Data Ingestion] à Experience Platform, vous devez fournir des valeurs pour les informations d’authentification suivantes :

| Informations d’identification | Description |
| --- | --- |
| Clé d’authentification [!DNL Acxiom] | La clé d’authentification. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Clé d’accès [!DNL Amazon S3] | Identifiant de clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Clé secrète [!DNL Amazon S3] | L’identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |

## Liste autorisée d’adresses IP

Avant de pouvoir utiliser les connecteurs source, vous devez ajouter à votre place sur la liste autorisée les adresses IP requises pour votre région. Si vous n’ajoutez pas ces adresses IP, les connecteurs source risquent de ne pas fonctionner correctement ou de produire des erreurs. Placer sur la liste autorisée Pour obtenir des instructions détaillées et la liste des adresses IP à autoriser, lisez la page [Adresses IP à inclure](../../ip-address-allow-list.md).

### Configuration des autorisations sur Experience Platform

Pour connecter votre compte **[!UICONTROL à Experience Platform]** les autorisations **[!UICONTROL Afficher les sources et]** Gérer les sources[!DNL Acxiom Data Ingestion] doivent être activées. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

### Contraintes de dénomination pour fichiers et répertoires

Les restrictions répertoriées ci-dessous doivent être prises en compte lors de l’attribution d’un nom à votre fichier ou répertoire d’espace de stockage :

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Les caractères de chemin d’URL non autorisés ne sont pas autorisés. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration requise pour importer des données de votre compte [!DNL Acxiom] vers Experience Platform. Vous pouvez maintenant passer au guide sur la [connexion [!DNL Acxiom Data Ingestion] à Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
