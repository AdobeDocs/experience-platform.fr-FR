---
title: Notes de mise à jour d’octobre 2020 d’Adobe Experience Platform
description: Les notes de mise à jour d’octobre 2020 pour Adobe Experience Platform
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 23%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : jeudi 14 octobre 2020**

- [Préparation des données](#data-prep)
- [Profil client en temps réel](#profile)
- [Segmentation Service](#segmentation)
- [Sources](#sources)
- [Délai de rentabilisation](#time-to-value)

## Préparation de données {#data-prep}

La préparation des données permet aux personnes travaillant dans l’ingénierie de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| fonction `is_set` | La fonction `is_set` vous permet de vérifier la présence d’un attribut dans les données source. `is_set` peut être utilisé en combinaison avec `is_empty` pour vérifier à la fois la présence de l’attribut et la présence de la valeur dans l’attribut . |
| Fonction `get_values` | La fonction `get_values` vous permet d’obtenir les valeurs du mappage d’entrée pour n’importe quelle clé donnée. |

Pour plus d’informations, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Grâce à [!DNL Real-Time Customer Profile], vous disposez d’une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Ajouts de l’API d’aperçu de profil | L’API d’aperçu de profil (`/previewsamplestatus`) offre désormais la possibilité d’afficher la répartition du total des fragments de profil dans votre organisation, ainsi que la répartition des fragments de profil dans les espaces de noms d’identité. |
| Mises à jour de la vue de schéma d’union | Dans l’interface utilisateur d’Experience Platform, les utilisateurs peuvent plus facilement trouver des informations concernant tous les schémas et jeux de données qui contribuent au schéma d’union, ainsi que les attributs clés de surface tels que les champs d’identité et de relation. Ces mises à jour améliorent la capacité à résoudre les problèmes et à vérifier que les profils sont correctement configurés, que les identités sont correctement assemblées et que les données ont bien été ingérées. |

Pour plus d’informations sur [!DNL Real-Time Customer Profile], notamment les bonnes pratiques et les tutoriels relatifs à l’utilisation des données [!DNL Profile], consultez la [ présentation du profil client en temps réel ](../../profile/home.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir des données [!DNL Real-Time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Experience Platform], ce qui les rend facilement accessibles depuis n’importe quelle application Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Suppression de la limite de segmentation en flux continu | La limite de sept jours pour la période de recherche en amont a été supprimée. |

Pour plus d’informations sur les [!DNL Segmentation Service], consultez la [ présentation de la segmentation ](../../segmentation/home.md)

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de l’authentification SSH pour le protocole SFTP | Vous pouvez connecter votre compte SFTP à [!DNL Experience Platform] à l’aide de clés SSH ouvertes RSA/DSA. Pour plus d’informations[&#128279;](../../sources/connectors/cloud-storage/sftp.md) consultez la  Présentation du protocole SFTP . |
| Améliorations de l’expérience utilisateur | Vous pouvez activer votre jeu de données pour [!DNL Profile] pendant le processus d’ingestion des données. Pour plus d’informations, consultez le tutoriel [workflow de flux de données de stockage dans le cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) . |

Pour en savoir plus sur les sources, consultez la [vue d’ensemble des sources](../../sources/home.md).

## Délai de rentabilisation {#time-to-value}

Adobe Experience Platform permet aux équipes des opérations marketing de créer une vue à 360 degrés de leurs clients sans avoir besoin d’une expertise approfondie en ingénierie de données. L’objectif est d’accélérer les équipes et de créer de la valeur grâce à la vitesse des données.

« Time to Value » (Délai de rentabilisation) concerne plusieurs profils. Les ingénieurs de données peuvent effectuer des tâches de manière efficace et accélérée avec la transparence de l’activité des données, de sorte qu’un profil client en temps réel robuste et évolutif soit disponible plus rapidement. Les marketeurs peuvent ensuite utiliser le profil client complet et robuste pour la segmentation et l&#39;activation.

### Caractéristiques des fonctionnalités

#### Schéma

Met à niveau la convivialité et les workflows, et fournit des informations prêtes à l’emploi, la normalisation et la transparence des champs clés dans les compositions de schémas. Expose la parenté des données pour la combinaison de modèles de données individuels représentés comme le « schéma d’union », fournissant insight dans la structure et les ingrédients du profil client en temps réel.

- Mise à niveau du workflow du schéma
   - Utilisez des raccourcis pour le type de schéma XDM le plus courant, avec des paramètres automatisés dans les recommandations de l’éditeur de schémas et du groupe de champs de schéma en fonction de vos objectifs
   - Augmentation de l’efficacité des workflows avec la sélection de plusieurs groupes de champs et la fonctionnalité de prévisualisation
   - Fournissez de la transparence sur les attributs clés de la composition des schémas, y compris l’identité, la relation et les champs obligatoires et obsolètes.
- Parenté des données du schéma d’union et transparence des attributs clés

#### Ingestion et collecte de données

Le mappage automatique, l’aperçu du mappage et la mise à niveau de la convivialité apportent des données de n’importe quelle plateforme ou source à utiliser dans le profil, la segmentation en aval et l’activation. Le système a l&#39;efficacité et l&#39;intelligence de rendre ce processus plus facile à utiliser, même pour les personnes en dehors de l&#39;informatique.

- Accès plus facile aux sources de données avec la mise à niveau des modèles d’action intégrés des cartes de pages de catalogue et des tableaux de données
- Champ/expression calculé pour l’ingestion de données
- Les recommandations de mappage de données accélèrent le processus d’ingestion
- Aperçu et validations du mappage

#### Configuration du profil

La visionneuse de profils conviviale pour les marketeurs avec une personnalisation vous permet de comprendre la composition d’un profil à utiliser dans les cas de segmentation, de planification et d’activation. Le workflow consolidé hydrate le profil de manière contrôlée et efficace en fournissant un workflow par étapes pour la politique de fusion.

- Affichez chaque profil individuel dans une visionneuse de profils améliorée qui affiche un tableau de bord avec une personnalisation complète, ce qui permet d’obtenir des données cross-canal groupées en fonction des objectifs commerciaux du spécialiste marketing.
- Modifiez les attributs standard et personnalisés dans le widget Informations de base, en fonction des besoins de l’entreprise.
- Personnalisez les widgets avec des attributs du profil client en temps réel à l’aide du sélecteur de schéma d’union. Le schéma d’union est dérivé des modèles de données sous-jacents utilisés dans l’ingestion des données de profil.


#### Surveillance

Assure la transparence du flux de données et fournit à insight des informations sur l’intégrité du trafic de données dans le système à partir des connecteurs source, ce qui offre davantage de libre-service et une possibilité d’action plus rapide pour la résolution des problèmes.

- Surveillez toutes les exécutions de flux et consultez une vue détaillée de chaque exécution, y compris l’état d’achèvement, la durée d’exécution, la liste des fichiers traités, les erreurs et les diagnostics exploitables.
