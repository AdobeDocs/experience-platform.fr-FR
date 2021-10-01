---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 11 mars 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: notes de mise à jour;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 64%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 11 mars 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] permet aux entreprises de rassembler des données issues de plusieurs systèmes d’entreprise afin de mieux permettre aux spécialistes du marketing d’identifier, de comprendre et d’impliquer les clients. [!DNL Experience Platform] comprend une infrastructure de gouvernance des données de bout en bout afin d’assurer une utilisation appropriée des données au sein  [!DNL Platform] et lors du partage entre les systèmes.

Adobe Experience Platform [!DNL Data Governance] est une série de stratégies et de technologies utilisées pour gérer les données clients et garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Il joue un rôle clé à différents niveaux dans [!DNL Experience Platform], notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les stratégies d’accès aux données et le contrôle d’accès sur les données pour les actions marketing.

**Nouvelles fonctionnalités**

>[!NOTE]
>
>Certaines des nouvelles fonctionnalités suivantes sont actuellement en version bêta et ne sont pas disponibles pour tous les utilisateurs. Les fonctionnalités en version bêta peuvent être modifiées.

| Fonctionnalité | Description |
| ------- | ----------- |
| Application automatisée des stratégies d’utilisation des données pour [!DNL Real-time Customer Data Platform] | Les stratégies d’utilisation des données sont désormais appliquées dans le workflow d’activation des données vers les destinations. [!DNL Data Governance] est également incorporé et appliqué lorsque vous apportez des modifications qui affectent les activations existantes (telles que les modifications apportées aux libellés de jeux de données, aux stratégies de fusion, aux définitions de segment, etc.). |
| Traçabilité des données pour l’application | Lorsqu’une stratégie d’utilisation des données est violée dans la plateforme de données clients en temps réel, l’interface utilisateur affiche une notification contenant des informations de traçabilité des données pour aider l’utilisateur à comprendre pourquoi les stratégies ont été violées et ce qu’il peut faire pour résoudre la violation. |


**Problèmes connus**

* Aucun

Pour plus d’informations sur [!DNL Data Governance], consultez la [Présentation de la gouvernance des données](../../data-governance/home.md).

## Data Ingestion {#ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’ingérer n’importe quel type et n’importe quelle latence de données. Adobe Experience Platform [!DNL Data Ingestion] offre plusieurs alternatives pour l’ingestion de données, notamment des API par lots, des API par flux, des connecteurs d’Adobe natifs, des partenaires d’intégration de données ou l’interface utilisateur de Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Ingestion par lots partielle | L’ingestion par lots partielle permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent ingérer toutes leurs données correctes dans Adobe Experience Platform, alors que toutes leurs données incorrectes sont traitées par lots séparément. Des détails sont ajoutés aux lots infructueux pour expliquer pourquoi ils n’ont pas été validés. Vous trouverez plus d’informations sur l’ingestion par lots partielle dans la [documentation de l’ingestion par lots partielle](../../ingestion/batch-ingestion/partial.md). |

**Problèmes connus**

* Aucun

Pour en savoir plus sur l’ingestion de données dans Platform, consultez la [Documentation de Data Ingestion](../../ingestion/home.md).


## Destinations {#destinations}

Dans la [plateforme de données clients en temps réel](../../rtcdp/overview.md), les destinations sont des intégrations préconfigurées avec des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| Destinations de stockage dans le cloud | La plateforme CDP en temps réel peut désormais fournir vos segments sous forme de fichiers de données à vos emplacements de stockage dans le cloud [!DNL Amazon S3] ou SFTP. Vous pouvez ainsi envoyer des audiences et leurs attributs de profils à vos systèmes internes au moyen de fichiers CSV ou séparés par des tabulations. |
| Destinations publicitaires | La carte de destination [!DNL Google] est désormais divisée en trois cartes de destination, pour les trois plateformes [!DNL Google] différentes actuellement prises en charge dans la plateforme de données clients en temps réel : [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Affichage et vidéo 360. |

Pour en savoir plus, consultez la [présentation des destinations](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Graphique privé amélioré | La fonctionnalité Graphique privé a été améliorée afin de réduire la latence de génération de graphiques d’un traitement par lots hebdomadaire à un graphique actualisé quotidiennement, ce qui permet aux clients [!DNL Identity Service] d’accéder à des graphiques d’identités et à des liens plus récents. |

**Problèmes connus**

* Aucun

Pour plus d’informations sur [!DNL Identity Service], consultez la [présentation d’Identity Service](../../identity-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Signaux obsolètes du connecteur d’Adobe Audience Manager | Les données au niveau du signal d’Audience Manager ne seront plus envoyées. Notez que l’adhésion aux segments pour les Caractéristiques et les Segments sera toujours incluse. Suite à ce changement, les jeux de données entrants ne seront plus générés. |
| Jeux de données renommés | Les jeux de données générés par le connecteur d’Audience Manager ont des noms et des descriptions à jour. |
| Activer le bouton bascule [!DNL Profile] dans Audience Manager | [!DNL Profile] Le basculement peut être activé ou désactivé pour convertir le jeu de données en  [!DNL Real-time Customer Profile]. La bascule est activée par défaut. |
| Prise en charge de l’interface utilisateur pour les systèmes de stockage dans le cloud | Nouveau connecteur source pour [!DNL Azure Data Lake Storage Gen2] dans l’interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes de gestion de la relation client | Nouveau connecteur source pour [!DNL HubSpot], [!DNL Salesforce Service Cloud] et [!DNL ServiceNow] dans l’interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes de base de données | Nouveau connecteur source pour [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] et [!DNL MySQL] dans l’interface utilisateur. |

**Problèmes connus**

* Aucun

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
