---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 27 janvier 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 18712835b2408b24cd2735b19c94bf1b1fe50df1
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 35%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 27 janvier 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, de transformer et de valider des données à partir du modèle de données d’expérience (XDM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Fonctions d&#39;expression régulières | [!DNL Data Prep] Le mappeur prend désormais en charge la correspondance et l’extraction d’une partie du champ d’entrée en fonction d’expressions régulières. |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation des ](../../data-prep/home.md).

## Destinations {#destinations}

[!DNL Destinations] sont des intégrations préétablies avec des plateformes de destination qui permettent une activation transparente des données de Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] est la solution d&#39;enregistrement d&#39;objets de Microsoft pour le cloud. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Correspondance d’ID avancée | Améliorations des fonctionnalités de taux de correspondance d&#39;audience dans [!DNL Facebook Custom Audiences] et [!DNL Google Customer Match], en ajoutant la prise en charge de la correspondance d&#39;identité supplémentaire, telle que les identifiants externes, les numéros de téléphone et les identifiants de périphérique mobile. Pour plus d’informations, consultez la documentation suivante : <ul><li>[Destination Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destination de la correspondance client Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Activation de profils et de segments vers une destination](../../destinations/ui/activate-destinations.md)</li></ul> |

Pour en savoir plus, consultez la [présentation des destinations](../../destinations/home.md).

## Real-time Customer Profile {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Real-time Customer Profile offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider les données client en une vue unifiée offrant un compte horodaté interactif de chaque interaction client.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Supprimer un jeu de données du magasin de Profils | Lorsque vous supprimez un jeu de données du lac Data Experience Platform, il est automatiquement supprimé du magasin de Profils. Vous n’avez plus besoin d’utiliser le point de terminaison API des tâches du système de Profil pour effectuer une demande de suppression afin de supprimer explicitement le jeu de données du magasin de Profils. Pour plus d&#39;informations, consultez le [profil system jobs API endpoint guide](../../profile/api/profile-system-jobs.md). |
| Estimation du nombre d’espaces de nommage d’ID pour un segment donné | Pour une estimation du nombre de profils, l’API de prévisualisation signale maintenant :<ul><li>Nombre total de profils estimés dans un segment pour un espace de nommage donné.</li><li>Nombre total de profils estimés dans le Schéma d&#39;Union de Profil pour un espace de nommage donné.</li></ul>Pour en savoir plus, consultez le [guide du point de terminaison de l&#39;API de prévisualisation de profil](../../profile/api/preview-sample-status.md). |

Pour plus d&#39;informations sur le Profil client en temps réel, y compris des didacticiels et les meilleures pratiques pour l&#39;utilisation des données [!DNL Profile], veuillez commencer par lire la [Présentation du Profil client en temps réel](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations du connecteur source Adobe Audience Manager | Vous pouvez désormais filtrer et sélectionner des segments propriétaires individuels, de l’Audience Manager à l’assimilation dans la plate-forme, ainsi que filtrer les caractéristiques propriétaires. Pour plus d&#39;informations, consultez le didacticiel [Création d&#39;un connecteur de source d&#39;Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| [!DNL Google BigQuery] amélioration du connecteur source | Vous pouvez désormais assimiler des fichiers de plus de 10 Go lors d’une seule exécution de flux à l’aide du connecteur source [!DNL BigQuery]. Pour plus d&#39;informations, consultez l&#39;[[!DNL BigQuery] aperçu du connecteur source](../../sources/connectors/databases/bigquery.md). |
| Prise en charge de types de données complexes pour les enregistrements de cloud | Vous pouvez désormais ingérer des types de données complexes, tels que des tableaux dans des fichiers JSON, lors de l’utilisation d’un connecteur source d’enregistrement cloud. Pour plus d’informations, consultez les didacticiels relatifs à la création d’un flux de données d’enregistrement cloud [dans l’interface utilisateur](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) ou [à l’aide de l’ [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Prise en charge de l&#39;authentification par clé principale de service pour la source [!DNL Microsoft Dynamics] | Vous pouvez désormais vous authentifier auprès de votre compte [!DNL Dynamics] à l’aide d’une clé principale de service en tant qu’alternative à l’authentification par mot de passe. Pour plus d&#39;informations, consultez l&#39;[[!DNL Dynamics] aperçu du connecteur source](../../sources/connectors/crm/ms-dynamics.md). |
| Prise en charge de l’interface utilisateur pour les séparateurs personnalisés dans les sources d’enregistrement cloud | Vous pouvez désormais définir un délimiteur de colonne personnalisé, tel qu’une virgule (`,`), une tabulation (`\t`) ou une barre verticale (`|`), pour collecter les fichiers délimités dans l’interface utilisateur. Pour plus d&#39;informations, consultez le didacticiel sur la [création d&#39;un flux de données avec un connecteur source d&#39;enregistrement de cloud ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
