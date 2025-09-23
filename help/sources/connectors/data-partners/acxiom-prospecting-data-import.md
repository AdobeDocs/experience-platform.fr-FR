---
title: Import de données de prospection Acxiom
description: Découvrez comment connecter les données de prospection Acxiom à Adobe Experience Platform et Adobe Real-time Customer Data Platform à l’aide de l’interface utilisateur.
exl-id: 6df674d9-c14b-42ea-a287-5377484e567d
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 31%

---

# [!DNL Acxiom Prospecting Data Import]

Adobe Experience Platform prend en charge l’ingestion de données à partir d’une application d’un partenaire de données. La prise en charge des partenaires de données et d’identité inclut [!DNL Acxiom Prospecting Data Import].

L’importation de données de prospection pour Adobe Real-Time Customer Data Platform de [!DNL Acxiom] est un processus permettant de fournir les audiences de prospects les plus productives possible. [!DNL Acxiom] prend les données propriétaires de Real-Time CDP par le biais d’une exportation sécurisée et les exécute via un système primé d’hygiène et de résolution d’identité. Un fichier de données qui peut être utilisé comme liste de suppression est généré. Ce fichier de données est ensuite comparé à la base de données [!DNL Acxiom Global], ce qui permet de personnaliser les listes de prospects pour l’importation.

Vous pouvez utiliser la source de [!DNL Acxiom] pour récupérer et mapper les réponses du service de prospect [!DNL Acxiom] en utilisant [!DNL Amazon S3] comme point de dépôt.

![acxiom-prospecting-workflow](../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/acxiom-prospecting.png)

Lisez le document ci-dessous pour plus d’informations sur la configuration de votre compte source [!DNL Acxiom Prospecting Data Import].

## Conditions préalables

Pour accéder à votre compartiment sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| Clé d’authentification [!DNL Acxiom] | La clé d’authentification. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Clé d’accès [!DNL Amazon S3] | Identifiant de clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Clé secrète [!DNL Amazon S3] | L’identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |

## Liste autorisée d’adresses IP

Avant de pouvoir utiliser les connecteurs source, vous devez ajouter à votre place sur la liste autorisée les adresses IP requises pour votre région. Si vous n’ajoutez pas ces adresses IP, les connecteurs source risquent de ne pas fonctionner correctement ou de produire des erreurs. Placer sur la liste autorisée Pour obtenir des instructions détaillées et la liste des adresses IP à autoriser, lisez la page [Adresses IP à inclure](../../ip-address-allow-list.md).

### Configuration des autorisations sur Experience Platform

Pour connecter votre compte **[!UICONTROL à Experience Platform]** les autorisations **[!UICONTROL Afficher les sources et]** Gérer les sources[!DNL Acxiom Prospecting Data Import] doivent être activées. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/abac/ui/permissions.md).

## Contraintes de dénomination pour fichiers et répertoires

Les restrictions répertoriées ci-dessous doivent être prises en compte lors de l’attribution d’un nom à votre fichier ou répertoire d’espace de stockage :

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Les caractères de chemin d’URL non autorisés ne sont pas autorisés. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration requise pour importer des données de votre compte [!DNL Acxiom] vers Experience Platform. Vous pouvez maintenant passer au guide sur la [connexion [!DNL Acxiom Prospecting Data Import] à Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).
