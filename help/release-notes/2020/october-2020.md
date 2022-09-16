---
title: Notes de mise à jour de Adobe Experience Platform - Octobre 2020
description: Notes de mise à jour d’octobre 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 25%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 14 octobre 2020**

- [Préparation de données](#data-prep)
- [Profil client en temps réel](#profile)
- [Segmentation Service](#segmentation)
- [Sources](#sources)
- [Temps jusqu’à la valeur](#time-to-value)

## Préparation des données {#data-prep}

La préparation des données permet aux ingénieurs de données de mapper, transformer et valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| fonction `is_set` | Le `is_set` permet de vérifier la présence d’un attribut dans les données source. `is_set` peut être utilisé conjointement avec `is_empty` pour vérifier à la fois la présence de l’attribut et la présence de la valeur dans l’attribut . |
| Fonction `get_values` | Le `get_values` vous permet d’obtenir les valeurs de la carte d’entrée pour une clé donnée. |

Pour plus d’informations, veuillez lire la [Aperçu de la préparation des données](../../data-prep/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Avec [!DNL Real-time Customer Profile], vous pouvez obtenir une vue d’ensemble de chaque client qui combine des données provenant de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Ajout d’API d’aperçu de profil | API d’aperçu de profil (`/previewsamplestatus`) permet désormais d’afficher la ventilation du nombre total de fragments de profil dans votre organisation IMS, ainsi que la distribution des fragments de profil entre les espaces de noms d’identité. |
| Mises à jour des vues des schémas d’union | Dans l’interface utilisateur de l’Experience Platform, les utilisateurs peuvent trouver plus facilement des informations concernant tous les schémas et jeux de données contribuant au schéma d’union, ainsi que des attributs de clé de surface tels que les champs d’identité et de relation. Ces mises à jour améliorent la possibilité de dépanner et de valider que les profils sont correctement configurés, que les identités sont correctement regroupées et que les données ont été ingérées avec succès. |

Pour plus d’informations sur [!DNL Real-time Customer Profile], y compris des tutoriels et des bonnes pratiques pour travailler avec [!DNL Profile] data, veuillez lire la [Présentation de Real-time Customer Profile](../../profile/home.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir des données [!DNL Real-time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Platform], ce qui les rend facilement accessibles depuis n’importe quelle application Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Suppression de la limite de segmentation par flux | La limite de sept jours pour la période de recherche arrière a été supprimée. |

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md)

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide de [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de l’authentification SSH pour SFTP | Vous pouvez connecter votre compte SFTP à [!DNL Platform] à l’aide des clés SSH RSA/DSA Open. Voir [Présentation SFTP](../../sources/connectors/cloud-storage/sftp.md) pour plus d’informations. |
| Améliorations de l’expérience utilisateur | Vous pouvez activer votre jeu de données pour [!DNL Profile] pendant le processus d’ingestion des données. Voir [workflow de flux de données de stockage dans le cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) tutoriel pour plus d’informations. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).

## Temps jusqu’à la valeur {#time-to-value}

Adobe Experience Platform permet entièrement aux équipes d’opérations marketing de créer une vue à 360 degrés de leurs clients sans avoir besoin d’une expertise approfondie en ingénierie des données. L’objectif est d’accélérer les équipes et de valoriser à travers la vitesse des données.

&quot;Temps jusqu’à la valeur&quot; coupe les personas. Les ingénieurs de données peuvent exécuter les tâches de manière efficace et accélérée avec la transparence de l’activité des données, de sorte qu’un profil client en temps réel robuste et évolutif soit disponible plus tôt. Les marketeurs peuvent ensuite utiliser le profil client complet et robuste pour la segmentation et l’activation.

### Fonctionnalités principales

#### Schéma

Met à niveau la convivialité et le workflow, et fournit des informations prêtes à l’emploi, la normalisation et la transparence des champs clés dans les compositions de schéma. Expose la traçabilité des données pour la combinaison de modèles de données individuels représentés sous forme de &quot;schéma d’union&quot;, fournissant des informations sur la structure et les ingrédients de Real-time Customer Profile.

- Mise à niveau du workflow de schéma
   - Utilisez des raccourcis pour le type de schéma XDM le plus courant, avec des paramètres automatisés dans l’éditeur de schémas et des recommandations de groupe de champs de schéma basées sur vos objectifs.
   - Amélioration de l’efficacité des workflows grâce à la fonctionnalité de sélection et d’aperçu de plusieurs groupes de champs
   - Fournir de la transparence sur les attributs clés de la composition des schémas, y compris l’identité, la relation et les champs obligatoires et obsolètes
- Liaison des données de schéma d’union et transparence des attributs clés

#### Ingestion et collecte de données

Le mappage automatique, l’aperçu du mapping et la mise à niveau de la convivialité apportent des données de n’importe quelle plateforme ou source à utiliser dans les profils, la segmentation en aval et l’activation. Le système dispose de l’efficacité et de l’intelligence nécessaires pour rendre ce processus plus facile à utiliser, même pour les personnes qui ne sont pas informaticiens.

- Mise à niveau du modèle d’action intégré d’une carte de page de catalogue et d’un tableau de données plus facile d’accès aux sources de données
- Champ/expression calculé pour l’ingestion de données
- Les recommandations de mappage de données accélèrent le processus d’ingestion
- Prévisualisation et validations du mapping

#### Configuration des profils

La visionneuse de profils conviviale avec personnalisation vous aide à comprendre la composition d’un profil à utiliser dans les cas de segmentation, de planification et d’activation. Le workflow consolidé hydrate le profil de manière contrôlée et efficace en fournissant un workflow par étapes pour la stratégie de fusion.

- Affichez chaque profil individuel dans une visionneuse de profils améliorée qui affiche un tableau de bord entièrement personnalisé, ce qui permet de regrouper les données cross-canal en fonction des objectifs commerciaux du marketeur.
- Modifiez les attributs standard et personnalisés dans le widget Informations de base, en fonction des besoins de l’entreprise.
- Personnalisez des widgets avec des attributs du profil client en temps réel à l’aide du sélecteur de schéma d’union. Le schéma d’union est dérivé des modèles de données sous-jacents utilisés dans l’ingestion des données de profil.


#### Surveillance

Garantit la transparence du flux de données et donne des informations sur l’intégrité du trafic de données dans le système à partir des connecteurs source, ce qui permet un meilleur libre-service et une meilleure activité pour résoudre les problèmes.

- Surveillez toutes les exécutions de flux et affichez une vue détaillée de chaque exécution, y compris l’état d’achèvement, la durée d’exécution, la liste des fichiers traités, les erreurs et les diagnostics exploitables.
