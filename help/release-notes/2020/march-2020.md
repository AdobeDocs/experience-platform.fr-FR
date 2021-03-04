---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 11 mars 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: notes de mise à jour;
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 60%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 11 mars 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] permet aux entreprises de rassembler des données issues de plusieurs systèmes d’entreprise afin de mieux permettre aux spécialistes du marketing d’identifier, de comprendre et d’impliquer les clients. [!DNL Experience Platform] comprend une infrastructure de gouvernance des données de bout en bout pour garantir une utilisation adéquate des données au sein  [!DNL Platform] et lors du partage entre les systèmes.

Adobe Experience Platform [!DNL Data Governance] est une série de stratégies et de technologies utilisées pour gérer les données client et assurer le respect des réglementations, restrictions et politiques applicables à l&#39;utilisation des données. Il joue un rôle clé à l&#39;intérieur de [!DNL Experience Platform] à divers niveaux, notamment le catalogage, la lignée de données, l&#39;étiquetage de l&#39;utilisation des données, les stratégies d&#39;accès aux données et le contrôle d&#39;accès sur les données pour les actions marketing.

**Nouvelles fonctionnalités**

>[!NOTE]
>
>Certaines des nouvelles fonctionnalités suivantes sont actuellement en version bêta et ne sont pas disponibles pour tous les utilisateurs. Les fonctionnalités en version bêta peuvent être modifiées.

| Fonctionnalité | Description |
| ------- | ----------- |
| Application automatisée des stratégies d&#39;utilisation des données pour [!DNL Real-time Customer Data Platform] | Les stratégies d’utilisation des données sont désormais appliquées dans le workflow d’activation des données vers les destinations. [!DNL Data Governance] est également incorporée et appliquée lorsque vous apportez des modifications qui affectent les activations existantes (telles que les modifications apportées aux étiquettes de jeux de données, aux stratégies de fusion, aux définitions de segment, etc.). |
| Traçabilité des données pour l’application | Lorsqu’une stratégie d’utilisation des données est violée dans la plateforme de données clients en temps réel, l’interface utilisateur affiche une notification contenant des informations de traçabilité des données pour aider l’utilisateur à comprendre pourquoi les stratégies ont été violées et ce qu’il peut faire pour résoudre la violation. |


**Problèmes connus**

* Aucun

Pour plus d&#39;informations sur [!DNL Data Governance], consultez la [Présentation de la gouvernance des données](../../data-governance/home.md).

## Ingestion des données {#ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’ingérer n’importe quel type et n’importe quelle latence de données. Adobe Experience Platform [!DNL Data Ingestion] offre plusieurs alternatives pour l’assimilation de données, notamment les API de lot, les API de diffusion en continu, les connecteurs d’Adobe natifs, les partenaires d’intégration de données ou l’interface utilisateur Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Ingestion par lots partielle | L’ingestion par lots partielle permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent ingérer toutes leurs données correctes dans Adobe Experience Platform, alors que toutes leurs données incorrectes sont traitées par lots séparément. Des détails sont ajoutés aux lots infructueux pour expliquer pourquoi ils n’ont pas été validés. Vous trouverez plus d’informations sur l’ingestion par lots partielle dans la [documentation de l’ingestion par lots partielle](../../ingestion/batch-ingestion/partial.md). |

**Problèmes connus**

* Aucun

Pour en savoir plus sur l’ingestion de données dans Platform, consultez la [Documentation de Data Ingestion](../../ingestion/home.md).


## Destinations {#destinations}

Dans [Plate-forme de données client en temps réel](../../rtcdp/overview.md), les destinations sont des intégrations préétablies avec les plateformes de destination qui activent les données à ces partenaires de manière transparente.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| Destinations de stockage dans le cloud | Le service CDP en temps réel peut désormais diffuser vos segments sous forme de fichiers de données à vos emplacements d’enregistrement de cloud [!DNL Amazon S3] ou SFTP. Vous pouvez ainsi envoyer des audiences et leurs attributs de profils à vos systèmes internes au moyen de fichiers CSV ou séparés par des tabulations. |
| Destinations publicitaires | La carte de destination [!DNL Google] est maintenant divisée en trois cartes de destination, pour les trois plateformes différentes [!DNL Google] actuellement prises en charge dans le CDP en temps réel : [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Affichage et vidéo 360. |

Pour en savoir plus, consultez la [présentation des destinations](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Adobe Experience Platform [!DNL Identity Service] vous aide à mieux vue de votre client et de son comportement en rapprochant les identités entre les périphériques et les systèmes, ce qui vous permet de fournir des expériences numériques personnelles et impactées en temps réel.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Graphique privé amélioré | La fonctionnalité Graphique privé a été améliorée afin de réduire la latence de génération de graphiques d&#39;un traitement par lots hebdomadaire à un graphique actualisé quotidiennement, ce qui permet à [!DNL Identity Service] clients d&#39;accéder à des graphiques d&#39;identité et des liens d&#39;identité plus à jour. |

**Problèmes connus**

* Aucun

Pour plus d&#39;informations sur [!DNL Identity Service], consultez la [Présentation du service d&#39;identité](../../identity-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Signaux obsolètes du connecteur d’Adobe Audience Manager | Les données au niveau du signal d’Audience Manager ne seront plus envoyées. Notez que l’adhésion aux segments pour les Caractéristiques et les Segments sera toujours incluse. Suite à ce changement, les jeux de données entrants ne seront plus générés. |
| Jeux de données renommés | Les jeux de données générés par le connecteur d’Audience Manager ont des noms et des descriptions à jour. |
| Activer la bascule [!DNL Profile] dans le Gestionnaire d&#39;Audiences | [!DNL Profile] la bascule peut être activée ou désactivée pour promouvoir le jeu de données à  [!DNL Real-time Customer Profile]. La bascule est activée par défaut. |
| Prise en charge de l’interface utilisateur pour les systèmes de stockage dans le cloud | Nouveau connecteur source pour [!DNL Azure Data Lake Storage Gen2] dans l’interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes de gestion de la relation client | Nouveau connecteur source pour [!DNL HubSpot], [!DNL Salesforce Service Cloud] et [!DNL ServiceNow] dans l’interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes de base de données | Nouveau connecteur source pour [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] et [!DNL MySQL] dans l’interface utilisateur. |

**Problèmes connus**

* Aucun

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).