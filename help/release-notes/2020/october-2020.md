---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour des Experience Platform Octobre 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e2b0048703816dc481eb9486310d86a8f2483af2
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 18%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 14 octobre 2020**

- [Préparation de données](#data-prep)
- [Real-time Customer Profile](#profile)
- [Segmentation Service](#segmentation)
- [Sources](#sources)
- [Temps jusqu’à la valeur](#time-to-value)

## Préparation de données {#data-prep}

La préparation des données permet aux ingénieurs de données de mapper, de transformer et de valider les données à partir du modèle de données d’expérience (XDM).

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| `is_set` fonction | La `is_set` fonction vous permet de vérifier la présence d’un attribut dans les données source. `is_set` peut être utilisé en combinaison avec `is_empty` pour vérifier à la fois la présence de l&#39;attribut et la présence de la valeur dans l&#39;attribut. |
| `get_values` fonction | La `get_values` fonction vous permet d&#39;obtenir les valeurs de la carte d&#39;entrée pour une clé donnée. |

For more information, please read the [Data Prep overview](../../data-prep/home.md).

## Real-time Customer Profile {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte d’activité horodaté de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Ajouts à l’API de prévisualisation de profil | L&#39;API Profil prévisualisation (`/previewsamplestatus`) permet désormais de vue d&#39;une ventilation du nombre total de fragments de profil dans votre organisation IMS, ainsi que de vue de la distribution de fragments de profil entre espaces de nommage d&#39;identité. |
| Mises à jour de vue schéma Union | Dans l’interface utilisateur de l’Experience Platform, les utilisateurs peuvent plus facilement trouver des informations concernant tous les schémas et jeux de données contribuant au schéma d’union, ainsi que des attributs de surface clés tels que les champs d’identité et de relation. Ces mises à jour permettent de résoudre les problèmes et de vérifier que les profils sont correctement configurés, que les identités sont correctement assemblées et que les données ont été correctement ingérées. |

For more information on [!DNL Real-time Customer Profile], including tutorials and best practices for working with [!DNL Profile] data, please read the [Real-time Customer Profile overview](../../profile/home.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], making them readily accessible by any Adobe application.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Suppression des limites de segmentation en flux continu | La limite de sept jours pour la période de consultation a été supprimée. |

For more information on [!DNL Segmentation Service], please see the [Segmentation overview](../../segmentation/home.md)

## Sources {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mappage hiérarchique | Vous pouvez prévisualisation un fichier source hiérarchique, tel que JSON ou Parquet, pendant le processus d’assimilation des données. |
| Prise en charge de l’authentification SSH pour SFTP | Vous pouvez connecter votre compte SFTP à [!DNL Platform] l’aide des clés SSH RSA/DSA Open SSH. See the [SFTP overview](../../sources/connectors/cloud-storage/ftp-sftp.md) for more information. |
| Améliorations de l&#39;environnement | Vous pouvez activer votre jeu de données pendant [!DNL Profile] le processus d&#39;assimilation des données. Pour plus d’informations, consultez le didacticiel sur le flux de travail [des flux de données](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) Cloud enregistrement. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).

## Temps jusqu’à la valeur {#time-to-value}

Adobe Experience Platform permet aux équipes d’opérations marketing de créer une vue de 360 degrés de leurs clients sans avoir besoin d’une grande expertise en ingénierie des données. L&#39;objectif est d&#39;accélérer les équipes et de valoriser par la vélocité des données.

&quot;Temps de valeur&quot; coupe les personnalités. Les ingénieurs de données peuvent exécuter les tâches de manière efficace et accélérée grâce à la transparence de l’activité des données, de sorte qu’un profil client en temps réel robuste et évolutif soit disponible plus rapidement. Les marketeurs peuvent alors utiliser le profil complet et robuste de la clientèle pour la segmentation et l’activation.

### Faits saillants des fonctionnalités

#### Schéma

Met à niveau la convivialité et le flux de travail et fournit des informations prêtes à l&#39;emploi, la normalisation et la transparence des champs clés dans les compositions de schéma. Expose la lignée de données pour la combinaison de modèles de données individuels représentés sous le nom de &quot;schéma d’union&quot;, fournissant des informations sur la structure et les ingrédients du Profil client en temps réel.

- Mise à niveau du processus de schéma
   - Utilisez des raccourcis pour le type de schéma XDM le plus courant, avec des paramètres automatisés dans l&#39;éditeur de schéma et des recommandations de mixin basés sur vos objectifs.
   - Augmenter l&#39;efficacité du processus grâce à plusieurs options de sélection et de prévisualisation de mixage
   - Fournir une transparence sur les attributs clés de la composition du schéma, y compris l&#39;identité, la relation et les champs obligatoires et obsolètes
- Transparence du lien entre les données du Schéma d&#39;Union et les attributs clés

#### Ingestion et collecte de données

La mise à niveau de la mise en correspondance automatique, de la prévisualisation de mappage et de la facilité d’utilisation permet d’importer des données de n’importe quelle plateforme ou source pour les utiliser dans le profil, la segmentation en aval et l’activation. Le système dispose de l&#39;efficacité et de l&#39;intelligence nécessaires pour faciliter l&#39;utilisation de ce processus, même pour les personnes extérieures à l&#39;informatique.

- Faciliter l&#39;accès aux sources de données grâce à la mise à niveau des modèles d&#39;action en ligne de la carte de page du catalogue et de la table de données
- Champ/expression calculé pour l’assimilation de données
- Les recommandations de mappage de données accélèrent le processus d’assimilation
- Mappage des prévisualisations et des validations

#### Configuration du profil

Le lecteur de profil compatible avec les marketeurs avec personnalisation vous permet de comprendre la composition d’un profil à utiliser dans les cas de segmentation, de planification et d’activation. Le processus consolidé hydrate le profil de manière contrôlée et efficace en fournissant un processus par étapes pour la stratégie de fusion.

- Vue chaque profil individuel dans un lecteur de profil amélioré qui affiche un tableau de bord entièrement personnalisé, ce qui permet de regrouper les données sur plusieurs canaux en fonction des objectifs commerciaux du spécialiste du marketing.
- Modifiez les attributs standard et personnalisés dans le widget Informations de base, en fonction des besoins de l’entreprise.
- Personnalisez les widgets avec des attributs provenant du profil client en temps réel, à l’aide du sélecteur de schéma d’union. Le schéma d&#39;union est dérivé des modèles de données sous-jacents utilisés dans l&#39;assimilation de données de profil.


#### Surveillance

Garantit la transparence du flux de données et fournit des informations sur l’état du trafic de données dans le système à partir des connecteurs source, ce qui permet d’améliorer le libre-service et d’accélérer les opérations de dépannage.

- Surveillez toutes les exécutions de flux et consultez une vue détaillée de chaque exécution, y compris l’état d’achèvement, la durée d’exécution, la liste des fichiers traités, les erreurs et les diagnostics exploitables.