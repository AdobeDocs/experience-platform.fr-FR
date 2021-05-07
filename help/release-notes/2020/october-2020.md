---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour des Experience Platform Octobre 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1012'
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
| `is_set` fonction | La fonction `is_set` permet de vérifier la présence d&#39;un attribut dans les données source. `is_set` peut être utilisé en combinaison avec  `is_empty` pour vérifier à la fois la présence de l&#39;attribut et la présence de la valeur dans l&#39;attribut. |
| `get_values` fonction | La fonction `get_values` vous permet d&#39;obtenir les valeurs de la carte d&#39;entrée pour une clé donnée. |

Pour plus d&#39;informations, veuillez lire le [Aperçu de l&#39;aperçu de l&#39;aperçu de l&#39;aperçu de l&#39;aperçu des données](../../data-prep/home.md).

## Real-time Customer Profile {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. [!DNL Real-time Customer Profile] permet de visualiser une vue holistique de chaque client qui combine des données provenant de plusieurs canaux, y compris des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte d’activité horodaté de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Ajouts à l’API de prévisualisation de profil | L&#39;API de prévisualisation de Profil (`/previewsamplestatus`) permet désormais de vue d&#39;une ventilation des fragments de profil totaux dans votre organisation IMS, ainsi que de vue de la distribution des fragments de profil entre espaces de nommage d&#39;identité. |
| Mises à jour de vue schéma Union | Dans l’interface utilisateur de l’Experience Platform, les utilisateurs peuvent plus facilement trouver des informations concernant tous les schémas et jeux de données contribuant au schéma d’union, ainsi que des attributs de surface clés tels que les champs d’identité et de relation. Ces mises à jour permettent de résoudre les problèmes et de vérifier que les profils sont correctement configurés, que les identités sont correctement assemblées et que les données ont été correctement ingérées. |

Pour plus d&#39;informations sur [!DNL Real-time Customer Profile], y compris des didacticiels et les meilleures pratiques pour travailler avec les données [!DNL Profile], consultez la [Présentation du Profil client en temps réel](../../profile/home.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-time Customer Profile]. Ces segments sont configurés et gérés de manière centralisée sur [!DNL Platform], ce qui les rend facilement accessibles par toute application d&#39;Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Suppression des limites de segmentation en flux continu | La limite de sept jours pour la période de consultation a été supprimée. |

Pour plus d&#39;informations sur [!DNL Segmentation Service], consultez la [Présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de l’authentification SSH pour SFTP | Vous pouvez connecter votre compte SFTP à [!DNL Platform] à l&#39;aide des clés SSH RSA/DSA Open SSH. Pour plus d&#39;informations, consultez l&#39;[aperçu SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Améliorations de l&#39;environnement | Vous pouvez activer votre jeu de données pour [!DNL Profile] pendant le processus d&#39;assimilation des données. Pour plus d&#39;informations, consultez le didacticiel [processus de flux de données d&#39;enregistrement cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).

## Temps jusqu&#39;à la valeur {#time-to-value}

Adobe Experience Platform permet aux équipes d’opérations marketing de créer une vue de 360 degrés de leurs clients sans avoir besoin d’une grande expertise en ingénierie des données. L&#39;objectif est d&#39;accélérer les équipes et de valoriser par la vélocité des données.

&quot;Temps de valeur&quot; coupe les personnalités. Les ingénieurs de données peuvent exécuter les tâches de manière efficace et accélérée grâce à la transparence de l’activité des données, de sorte qu’un profil client en temps réel robuste et évolutif soit disponible plus rapidement. Les marketeurs peuvent alors utiliser le profil complet et robuste de la clientèle pour la segmentation et l’activation.

### Faits saillants des fonctionnalités

#### Schéma

Met à niveau la convivialité et le flux de travail et fournit des informations prêtes à l&#39;emploi, la normalisation et la transparence des champs clés dans les compositions de schéma. Expose la lignée de données pour la combinaison de modèles de données individuels représentés sous le nom de &quot;schéma d’union&quot;, fournissant des informations sur la structure et les ingrédients du Profil client en temps réel.

- Mise à niveau du processus de schéma
   - Utilisez des raccourcis pour le type de schéma XDM le plus courant, avec des paramètres automatisés dans l&#39;éditeur de schéma et des recommandations de groupe de champs de schéma en fonction de vos objectifs.
   - Augmenter l&#39;efficacité du processus grâce à la sélection et à la prévisualisation de plusieurs groupes de champs
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

- Surveillez toutes les exécutions de flux et consultez une vue détaillée de chaque exécution, y compris l&#39;état d&#39;achèvement, la durée d&#39;exécution, la liste des fichiers traités, les erreurs et les diagnostics exploitables.
