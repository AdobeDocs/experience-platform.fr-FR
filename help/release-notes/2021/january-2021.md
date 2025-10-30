---
title: Notes de mise à jour d’Adobe Experience Platform - Janvier 2021
description: Notes de mise à jour de janvier 2021 pour Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 86%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 27 janvier 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Fonctions d’expressions régulières | Le mappeur de [!DNL Data Prep] prend désormais en charge la correspondance et l’extraction d’une partie du champ d’entrée en fonction des expressions régulières. |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation](../../data-prep/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] est la solution de stockage d’objets de Microsoft pour le cloud. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Correspondance d’ID avancée | Améliorations des fonctionnalités relatives aux taux de correspondance d’audience dans [!DNL Facebook Custom Audiences] et [!DNL Google Customer Match], grâce à l’ajout de la prise en charge de la correspondance d’identités supplémentaires, comme les ID externes, les numéros de téléphone et les ID d’appareil mobile. Pour plus d’informations, consultez la documentation suivante : <ul><li>[Destination Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destination Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Activation des données d’audience vers des destinations d’exportation de segments de diffusion](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Pour en savoir plus, consultez la [présentation des destinations](../../destinations/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le [!DNL Profile] vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Suppression d’un jeu de données du magasin de profils | Lorsque vous supprimez un jeu de données du lac de données d’Experience Platform, ce jeu est automatiquement supprimé du magasin de profils. Vous n’avez plus besoin d’utiliser le point d’entrée de l’API des tâches du système de profils pour effectuer une demande de suppression permettant de supprimer explicitement le jeu de données du magasin de profils. Pour plus d’informations, consultez le [guide relatif au point d’entrée de l’API du système de profils](../../profile/api/profile-system-jobs.md). |
| Estimation du nombre d’espaces de noms d’ID pour un segment donné | Pour l’estimation du nombre de profils, l’API de prévisualisation indique désormais :<ul><li>Le nombre total de profils estimés dans un segment pour un espace de noms donné.</li><li>Le nombre total de profils estimés dans le schéma d’union des profils pour un espace de noms donné.</li></ul>Pour en savoir plus, consultez le [guide relatif au point d’entrée de l’API de prévisualisation du profil](../../profile/api/preview-sample-status.md). |

Pour plus d’informations sur le profil client en temps réel, notamment les bonnes pratiques et les tutoriels relatifs à l’utilisation des données [!DNL Profile], consultez tout d’abord la [&#x200B; présentation du profil client en temps réel](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations du connecteur source Adobe Audience Manager | Vous pouvez désormais filtrer et sélectionner des segments propriétaires individuels depuis Audience Manager pour les ingérer dans Experience Platform, ainsi que filtrer les caractéristiques propriétaires. Pour plus d’informations, consultez le tutoriel sur la [création d’un connecteur source Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Améliorations du connecteur source [!DNL Google BigQuery] | Vous pouvez désormais ingérer des fichiers de plus de 10 Go lors d’une seule exécution de flux à l’aide du connecteur source [!DNL BigQuery]. Pour plus d’informations, consultez la présentation du connecteur source [[!DNL BigQuery] &#x200B;](../../sources/connectors/databases/bigquery.md). |
| Prise en charge de types de données complexes pour le stockage sur le cloud | Vous pouvez désormais ingérer des types de données complexes, tels que des tableaux dans des fichiers JSON, lors de l’utilisation d’un connecteur source d’espace de stockage. Pour plus d’informations, consultez les tutoriels sur la création d’un flux de données d’espace de stockage [dans l’interface utilisateur](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) ou [à l’aide de  [!DNL Flow Service] l’API &#x200B;](../../sources/tutorials/api/collect/cloud-storage.md). |
| Prise en charge de l’authentification basée sur la clé de service principale pour la source [!DNL Microsoft Dynamics] | Vous pouvez désormais vous authentifier auprès de votre compte [!DNL Dynamics] à l’aide d’une clé de service principale. Cela représente une alternative à l’authentification par mot de passe. Pour plus d’informations, consultez la présentation du connecteur source [[!DNL Dynamics] &#x200B;](../../sources/connectors/crm/ms-dynamics.md). |
| Prise en charge de l’interface utilisateur pour les séparateurs personnalisés dans les sources d’espace de stockage | Vous pouvez désormais définir un délimiteur de colonne personnalisé, tel qu’une virgule (`,`), une tabulation (`\t`) ou une barre verticale (&vert;) pour collecter les fichiers délimités dans l’interface utilisateur. Pour plus d’informations, consultez le tutoriel sur la [création d’un flux de données avec un connecteur source d’espace de stockage](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
