---
keywords: Experience Platform;accueil;rubriques les plus consultées;sources;ingestion;dépannage;dépannage des sources;faq;faq;faq;connecteurs source;connecteur source;faqs des connecteurs source;dépannage des connecteurs source;dépannage des connecteurs source
solution: Experience Platform
title: Résolution des problèmes liés aux sources
topic-legacy: troubleshooting
description: Ce document répond aux questions les plus fréquemment posées sur les sources dans Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: b55097b6e7cd49166f68d0c86b788cd36ebdebab
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 18%

---

# Guide de dépannage des sources

Ce document répond aux questions les plus fréquemment posées sur les sources dans Adobe Experience Platform. Pour les questions et le dépannage liés à d’autres [!DNL Platform] les services, y compris ceux qui sont rencontrés dans tous les [!DNL Platform] API, reportez-vous à la section [Guide de dépannage des Experience Platform](../landing/troubleshooting.md).

## Questions fréquentes

Vous trouverez ci-dessous une liste de réponses aux questions fréquentes sur les sources.

### Dois-je apporter des modifications à nos paramètres de sécurité réseau pour activer les sources ?

Vous devrez peut-être placer sur la liste autorisée certaines adresses IP pour activer les sources. Pour plus d’informations, consultez la documentation sur votre connecteur source spécifique.

### Quels types d’authentification sont pris en charge par les sources ?

Les sources peuvent être authentifiées à l’aide de chaînes de connexion, de noms d’utilisateur et de mots de passe, ou de jetons d’accès et de clés. Vous trouverez des détails spécifiques sur les types d’authentification pris en charge dans la documentation du connecteur source spécifié.

### Pourquoi toutes mes exécutions de flux récentes échouent-elles ?

Si vous constatez que toutes vos exécutions de flux récentes échouent, vos informations d’identification ont peut-être changé ou expiré. Pour résoudre ce problème, essayez de mettre à jour votre connexion avec les informations d’identification les plus récentes.

### Quels types de fichiers sont pris en charge ?

Actuellement, les types de fichiers pris en charge sont les fichiers délimités JSON et Parquet.

### Quelles sont les contraintes sur les noms et tailles de fichier ?

Vous trouverez ci-dessous une liste des contraintes que vous devez tenir compte des fichiers dans les sources.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL illégaux interdits. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).
- Le nombre maximal de fichiers par lot est de 1 500, avec une taille de lot maximale de 100 Go.
- Le nombre maximal de propriétés ou de champs par ligne est de 10 000.
- Le nombre maximal de lots pouvant être envoyés par utilisateur, par minute, est de 138.

### Quels types de données sont pris en charge ?

Les types de données pris en charge sont les entiers, les chaînes, les valeurs booléennes, les objets datetime, les tableaux et les objets.

### Quels formats de date et d’heure sont pris en charge ?

Les sources prennent en charge un large éventail de formats de date et heure lors de l’ingestion de données. Vous trouverez plus d’informations sur les formats de date et d’heure pris en charge dans la section dates du [guide de gestion des formats de données](../data-prep/data-handling.md#dates) dans la documentation relative à la préparation des données.

### Comment formater des tableaux dans des fichiers CSV, JSON et Parquet ?

Les fichiers JSON et Parquet prennent en charge de manière native les tableaux. Pour les structures plates, telles que les fichiers CSV, les tableaux ne sont pas pris en charge. Cependant, les chaînes comportant plusieurs valeurs peuvent être divisées en un tableau à l’aide de fonctions de préparation de données telles que l’explosion et la jointure. Vous trouverez plus d’informations sur ces fonctions de préparation de données dans la section [guide des fonctions de préparation de données](../data-prep/functions.md#string)

### Quelles sources prennent en charge l’ingestion partielle ?

Toutes les sources d’ingestion par lots prennent en charge l’ingestion partielle. Toutefois, les sources d’ingestion par flux ne prennent pas en charge l’ingestion partielle.

### Quand dois-je utiliser l’ingestion partielle ?

L’ingestion partielle doit être utilisée si vous le faites **not** ont des contraintes, telles que l’ingestion de l’intégralité du fichier dans Platform. Vous pouvez également utiliser l’ingestion partielle si vous n’avez pas envie d’ingérer des données susceptibles de contenir des erreurs.

### Quel est le seuil d’erreur d’ingestion partielle type ?

Il n’existe pas de &quot;seuil d’erreur type&quot; pour l’ingestion partielle. Cette valeur peut plutôt varier d’un cas d’utilisation à l’autre. Par défaut, le seuil d’erreur est défini sur 5 %.

### Combien de temps faut-il pour qu’un état d’exécution de flux soit mis à jour après la création d’un nouveau flux de données ?

Les exécutions de flux ne sont pas générées instantanément et peuvent prendre entre deux et trois minutes pour se mettre à jour après avoir été désignées. `startTime`. La vérification de l’état d’une exécution de flux, immédiatement après la création d’un nouveau flux de données ne renvoie pas d’informations sur l’exécution de flux de `lastRunDetails` comme cela ne s&#39;est pas encore produit. Il est recommandé d’autoriser le flux de données à générer quelques minutes avant de vérifier l’état de l’exécution du flux.