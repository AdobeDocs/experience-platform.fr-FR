---
keywords: Experience Platform ; accueil ; rubriques populaires ; sources ; assimilation ; dépannage ; sources ; dépannage ; sources faq ; faq ; connecteurs source ; connecteur source ; connecteurs source ; faqs ; connecteurs source ; dépannage ; connecteurs source ;
solution: Experience Platform
title: Dépannage des sources
topic: troubleshooting
description: Ce document fournit des réponses aux questions fréquentes sur les sources de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 26e7116858574b366760ffd4f92b14117ccd28eb
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 2%

---


# (Bêta) Guide de dépannage des sources

Ce document fournit des réponses aux questions fréquentes sur les sources de Adobe Experience Platform. Pour toute question ou dépannage concernant d&#39;autres services [!DNL Platform], y compris ceux rencontrés sur toutes les API [!DNL Platform], consultez le [guide de dépannage Experience Platform](../landing/troubleshooting.md).

## Questions fréquemment posées 

Voici une liste de réponses aux questions fréquemment posées sur les sources.

### Dois-je apporter des modifications à nos paramètres de sécurité réseau pour activer les sources ?

Vous devrez peut-être placer sur la liste autorisée certaines adresses IP pour activer les sources. Pour plus d&#39;informations, veuillez lire la documentation sur votre connecteur source spécifique.

### Quels types d&#39;authentification sont pris en charge par les sources ?

Les sources peuvent être authentifiées à l’aide de chaînes de connexion, de noms d’utilisateur et de mots de passe, ou de jetons d&#39;accès et clés. Vous trouverez des détails spécifiques sur les types d&#39;authentification pris en charge dans la documentation du connecteur source spécifié.

### Pourquoi tous mes flux récents échouent-ils ?

Si vous constatez que toutes vos exécutions de flux récentes échouent, vos informations d’identification ont peut-être été modifiées ou ont expiré. Pour résoudre ce problème, essayez de mettre à jour votre connexion avec les dernières informations d’identification.

### Quels types de fichier sont pris en charge ?

Actuellement, les types de fichiers pris en charge sont les fichiers délimités, JSON et Parquet.

### Quelles sont les contraintes relatives aux noms et tailles de fichiers ?

Vous trouverez ci-dessous une liste de contraintes dont vous devez tenir compte pour les fichiers des sources.

- Les noms des composants de répertoire et de fichier ne peuvent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). S&#39;il est fourni, il sera automatiquement supprimé.
- Les caractères d’URL réservés suivants doivent être correctement placés en séquence d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL non autorisés. Les points de code tels que `\uE000`, bien qu&#39;ils soient valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode dans HTTP/1.1, voir [RFC 2616, Section 2.2 : Règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractère point (.) et deux caractères de point (.).
- Le nombre maximal de fichiers par lot est de 1 500, avec une taille de lot maximale de 100 Go.
- Le nombre maximal de propriétés ou de champs par ligne est de 10 000.
- Le nombre maximal de lots pouvant être envoyés par utilisateur par minute est de 138.

### Quels types de données sont pris en charge ?

Les types de données pris en charge sont les entiers, les chaînes, les booléens, les objets datetime, les tableaux et les objets.

### Quels formats de date et d’heure sont pris en charge ?

Les sources prennent en charge une grande variété de formats de date et heure lors de l’importation de données. Pour plus d&#39;informations sur les formats de date et heure pris en charge, consultez le [guide des fonctions de date de préparation des données](../data-prep/dates.md).

### Comment formater des tableaux dans des fichiers CSV, JSON et Parquet ?

Les fichiers JSON et Parquet prennent en charge les tableaux de manière native. Pour les structures plates, telles que les CSV, les tableaux ne sont pas pris en charge. Cependant, il est possible de diviser les chaînes avec plusieurs valeurs en tableau à l’aide des fonctions de prép de données telles que exploser et joindre. Pour plus d&#39;informations sur ces fonctions de prép de données, consultez le [guide des fonctions de prép de données](../data-prep/functions.md#string).

### Quelles sources prennent en charge l&#39;ingestion partielle ?

Toutes les sources d&#39;assimilation par lot prennent en charge l&#39;assimilation partielle. Cependant, les sources d’assimilation en flux continu ne prennent pas en charge l’assimilation partielle.

### Quand dois-je utiliser l&#39;ingestion partielle ?

L&#39;assimilation partielle doit être utilisée si **ne** a pas de contraintes, comme le fait que le fichier entier soit ingéré dans Platform. Vous pouvez également utiliser l’assimilation partielle si vous n’avez pas d’inconvénient à ingérer des données susceptibles de contenir des erreurs.

### Quel est le seuil d&#39;erreur d&#39;assimilation partielle type ?

Il n’existe pas de &quot;seuil d’erreur type&quot; pour l’assimilation partielle. Au lieu de cela, cette valeur peut varier d’un cas d’utilisation à l’autre. Par défaut, le seuil d’erreur est défini à 5 %.