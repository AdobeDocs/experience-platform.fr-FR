---
title: Ingestion des données par l’intermédiaire d’Acxiom
description: Découvrez comment ingérer [!DNL Acxiom] données à Real-time Customer Data Platform, enrichissez les profils propriétaires, améliorez les audiences et activez-les sur l’ensemble des canaux marketing.
badge: Version Beta
source-git-commit: 9419da451616ca7f087ecea7aa66a6c10a474fb3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 42%

---

# [!DNL Acxiom Data Ingestion]

>[!NOTE]
>
>La source [!DNL Acxiom Prospecting Data Import] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Utilisez la variable [!DNL Acxiom Data Ingestion] source à ingérer [!DNL Acxiom] des données dans Real-time Customer Data Platform et enrichissez les profils propriétaires. Vous pouvez ensuite utiliser la variable [!DNL Acxiom]profils propriétaires enrichis pour améliorer les audiences et les activer sur les canaux marketing.

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

Pour plus d’informations sur la configuration de votre [!DNL Acxiom Data Ingestion] compte source.

## Conditions préalables {#prerequisites}

Pour connecter votre [!DNL Acxiom Data Ingestion] pour Experience Platform, vous devez fournir des valeurs pour les informations d’authentification suivantes :

| Informations d’identification | Description |
| --- | --- |
| [!DNL Acxiom] clé d&#39;authentification | Clé d’authentification. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |
| [!DNL Amazon S3] clé d&#39;accès | Identifiant de la clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |
| Clé secrète [!DNL Amazon S3] | Identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

### Configuration des autorisations sur Experience Platform

Vous devez disposer des deux **[!UICONTROL Afficher les sources]** et **[!UICONTROL Gérer les sources]** autorisations activées pour votre compte afin de connecter [!DNL Acxiom Data Ingestion] compte à Experience Platform. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez la section [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

### Contraintes de dénomination pour fichiers et répertoires

Les restrictions répertoriées ci-dessous doivent être prises en compte lors de la dénomination de votre fichier ou répertoire de stockage dans le cloud :

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Les caractères de chemin d’URL interdits ne sont pas autorisés. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration préalable nécessaire pour importer les données de votre [!DNL Acxiom] compte à Experience Platform. Vous pouvez maintenant passer au guide sur la [connexion [!DNL Acxiom Data Ingestion] Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
