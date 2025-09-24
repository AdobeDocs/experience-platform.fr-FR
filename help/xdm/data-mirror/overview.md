---
keywords: Experience Platform;miroir de données;schéma basé sur un modèle;schéma relationnel;modifier la capture de données;synchronisation de la base de données;clé primaire;relations
solution: Experience Platform
title: Présentation de Data Mirror
description: Découvrez comment Data Mirror permet l’ingestion de modifications au niveau des lignes à partir de bases de données externes dans Adobe Experience Platform à l’aide de schémas basés sur des modèles avec une unicité, des relations et un contrôle de version appliqués.
badge: Disponibilité limitée
source-git-commit: 6ce214073f625a253fcc5bb14dfdb6a4a61e6e7b
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 1%

---

# Présentation de Data Mirror

>[!AVAILABILITY]
>
>Data Mirror et les schémas basés sur des modèles sont disponibles pour les détenteurs de licence Adobe Journey Optimizer **Campagnes orchestrées**. Ils sont également disponibles en tant que **version limitée** pour les utilisateurs de Customer Journey Analytics, selon votre licence et l’activation des fonctionnalités. Contactez votre représentant Adobe pour obtenir l’accès.

Data Mirror est une fonctionnalité de Adobe Experience Platform qui permet l’ingestion de modifications au niveau des lignes à partir de bases de données externes dans le lac de données à l’aide de schémas basés sur des modèles. Il préserve les relations de données, applique l’unicité et prend en charge le contrôle de version sans nécessiter de processus d’extraction, de transformation et de chargement (ETL) en amont.

Utilisez Data Mirror pour synchroniser les insertions, les mises à jour et les suppressions (données modifiables) de systèmes externes tels que [!DNL Snowflake], [!DNL Databricks] ou [!DNL BigQuery] directement dans Experience Platform. Cela vous permet de préserver la structure du modèle de base de données existant et l’intégrité des données lorsque vous importez des données dans Platform.

## Fonctionnalités et avantages

Data Mirror offre les fonctionnalités essentielles suivantes pour la synchronisation des bases de données :

* **Application des clés de Principal** : garantit l’unicité dans les jeux de données et empêche les enregistrements en double lors de l’ingestion.
* **Ingestion des modifications au niveau des lignes** : prend en charge les modifications de données granulaires, y compris les upserts et les suppressions, avec un contrôle de précision.
* **Relations de schéma** : permet des relations de clés étrangères et primaires entre les jeux de données par le biais de descripteurs.
* **Gestion des événements dans le désordre** : les processus modifient les événements à l’aide de descripteurs de version et d’horodatage, même lorsqu’ils arrivent dans une séquence différente.
* **Intégration d’entrepôt de données direct** : se connecte aux entrepôts de données cloud pris en charge pour une synchronisation des modifications en temps quasi réel.

Utilisez Data Mirror pour ingérer des modifications directement à partir de vos systèmes sources, appliquer l’intégrité des schémas et rendre les données disponibles pour les workflows d’analyse, d’orchestration des parcours et de conformité. Data Mirror élimine les processus ETL en amont complexes et accélère la mise en œuvre en permettant la mise en miroir directe des modèles de base de données existants.

Planifiez les exigences de suppression et de nettoyage de données lors de l’implémentation de schémas basés sur des modèles avec Data Mirror. Toutes les applications doivent tenir compte de la manière dont les suppressions affectent les jeux de données associés, les workflows de conformité et les processus en aval avant le déploiement.

## Conditions préalables {#prerequisites}

Avant de commencer, vous devez connaître les composants d’Experience Platform ci-après et vous assurer que votre environnement répond aux exigences techniques et structurelles :

* [Création de schémas dans l’interface utilisateur d’Experience Platform](../ui/resources/schemas.md) ou [API](../api/schemas.md)
* [Configuration des connexions source au cloud](../../sources/home.md#cloud-storage)
* [Application des concepts de capture de données de modification](../../sources/tutorials/api/change-data-capture.md) (upserts, suppressions)
* Faites la distinction entre [schémas standard](../schema/composition.md) et [schémas basés sur des modèles](../schema/model-based.md)
* [Définir des relations structurelles avec des descripteurs](../api/descriptors.md)

### Exigences d’implémentation

Votre instance de Platform et les données sources doivent répondre à des exigences spécifiques pour que Data Mirror fonctionne correctement. Data Mirror requiert des **schémas basés sur des modèles**, qui sont des structures de données flexibles avec des contraintes appliquées. Actuellement, Data Mirror fonctionne principalement avec des schémas basés sur des modèles, bien que l’intégration aux schémas XDM standard soit prise en charge par les fonctionnalités d’objets personnalisés B2B à venir (prévues pour octobre 2025).

Incluez une **clé primaire et un descripteur de version** dans tous les schémas. Si vous utilisez un schéma de série temporelle, un **descripteur d’horodatage** est également requis.

Votre base de données externe doit prendre en charge la capture de données de modification ou fournir des métadonnées qui identifient les insertions, les mises à jour et les suppressions. Les données Source doivent inclure des **identifiants uniques**, soit un champ unique, soit une clé primaire composite et des **informations de version** afin que le système puisse appliquer les mises à jour dans l’ordre approprié.

Pour détecter les suppressions, ajoutez une colonne `_change_request_type` qui spécifie si chaque enregistrement est un upsert ou une suppression.

## Implémentation de Data Mirror {#implementation-workflow}

Contrairement aux approches d’ingestion standard, Data Mirror préserve la structure de votre modèle de base de données dans le lac de données Experience Platform. Cette cohérence de la structure des données élimine le besoin de prétraitement externe. Voici un workflow général d’implémentation de Data Mirror. Choisissez votre méthode d’implémentation en fonction du workflow et du système source de votre équipe.

### Définition de la structure du schéma

Créez des [schémas basés sur des modèles](../schema/model-based.md) avec les descripteurs requis (métadonnées qui définissent le comportement et les contraintes des schémas). Sélectionnez une méthode adaptée au workflow de votre équipe, soit par le biais de l’interface utilisateur, soit directement par le biais de l’API.

* **Approche de l’interface utilisateur** : [création de schémas basés sur un modèle dans l’éditeur de schémas](../ui/resources/schemas.md#create-model-based-schema)
* **Approche API** : [création de schémas via l’API Schema Registry](../api/schemas.md#create-model-based-schema)

### Mapper les relations et définir la gestion des données

Définissez des connexions entre les jeux de données à l’aide de descripteurs de relation. Gérez les relations et maintenez la qualité des données entre les jeux de données. Ces tâches assurent des jointures cohérentes et prennent en charge la conformité aux exigences d’hygiène des données.

* **Relations de schéma** : [définissez des relations entre les jeux de données à l’aide de descripteurs](../api/descriptors.md)
* **Hygiène des enregistrements** : [Gérer les suppressions d’enregistrements de précision](../../hygiene/ui/record-delete.md#model-based-record-delete)

### Configurer votre connexion source

Sélectionnez une méthode d’ingestion en fonction de votre système source et de votre cas d’utilisation. Chaque option prend en charge différents niveaux d’automatisation, de transformation et d’évolutivité.

* [**Configuration des connexions source au cloud**](../../sources/home.md#cloud-storage)
* **Ingestion SQL** : utilisez Data Distiller pour écrire dans des jeux de données relationnels
* [**Chargement de fichier**](../ui/resources/schemas.md#upload-ddl-file) : chargez manuellement des fichiers pour une ingestion par lots ou unique

### Activer l’ingestion de capture de données de modification

Configurez des connexions de capture de données de modification avec les entrepôts de données cloud pris en charge. Ingérez des modifications au niveau des lignes tout en conservant l’unicité et en appliquant les mises à jour dans le bon ordre.

* **Modifier la capture de données** : [Activer la capture de données de modification dans les connexions source](../../sources/tutorials/api/change-data-capture.md)

## Cas d&#39;utilisation courants {#use-cases}

Examinez les cas d’utilisation courants répertoriés ci-dessous dans lesquels Data Mirror prend en charge la synchronisation précise des données et la conservation des relations. Chaque scénario montre comment Data Mirror prend en charge les besoins courants de l’entreprise en matière d’analyse, d’orchestration et de conformité.

### Modélisation des données relationnelles

Utilisez les [schémas basés sur des modèles](../schema/model-based.md) (également appelés schémas relationnels) dans Data Mirror pour représenter les entités, traiter les insertions, les mises à jour et les suppressions au niveau des lignes, et conserver les relations de clés primaires et étrangères qui existent dans vos sources de données. Cette approche apporte des principes de modélisation des données relationnelles à Experience Platform et assure la cohérence structurelle entre les jeux de données.

### Synchronisation entrepôt à lac

Mettez en miroir les données d’événement, les journaux d’interaction client, les événements de campagne et les données auxiliaires des entrepôts de données cloud pris en charge dans Experience Platform. Elle prend en charge l’éligibilité des campagnes, la précision de ciblage et le séquencement des messages. Journey Optimizer et Real-Time CDP B2B s’appuient sur cette logique pour une logique d’orchestration en temps quasi réel.

### Intégration de Customer Journey Analytics

Synchronisez des événements de série temporelle tels que des clics web, des consultations de produits, des achats et des interactions d’assistance à partir de systèmes tels que des centres d’appels ou des journaux de conversation. Un historique complet des modifications prend en charge une analyse des tendances et une segmentation comportementale précises. Experience Platform Data Mirror for Customer Journey Analytics l’utilise pour refléter les upserts et les suppressions des systèmes sources.

### Modélisation des relations B2B

Préserver les relations telles que les hiérarchies compte à contact, abonnement à compte ou contact à région. Ils prennent en charge la segmentation, la notation des prospects, le suivi des opportunités et la coordination multicanal. Contrairement à l’ingestion standard qui aplatit les relations, Data Mirror les conserve en mode natif à l’aide de descripteurs pour une modélisation plus précise.

### Gestion des abonnements

Suivez les événements tels que les renouvellements, les annulations, les mises à niveau, les rétrogradations et les modifications de plan avec un historique complet des versions. Cela prend en charge les campagnes de rétention, la prédiction de l’attrition et la segmentation basée sur le cycle de vie. L’historique complet permet d’obtenir des informations comportementales et un ciblage précis.

### Opérations d’hygiène des données

Utilisez la capture de données de modification pour permettre des suppressions précises au niveau des enregistrements à des fins de conformité (par exemple, pour les secteurs réglementés) et de nettoyage des workflows. Data Mirror applique les suppressions avec précision tout en préservant les données associées entre les jeux de données connectés.

## Considérations importantes {#considerations}

Examinez ces considérations clés pour vous assurer que votre implémentation s’aligne sur les comportements de schéma, les méthodes d’ingestion et les modèles de relation pris en charge. Une planification appropriée permet d’éviter les problèmes d’intégration et d’assurer une modélisation des données précise.

### Suppression des données et exigences en matière d’hygiène

Toutes les applications qui utilisent des schémas basés sur des modèles et Data Mirror doivent comprendre les implications de la suppression de données. Les schémas basés sur des modèles permettent des suppressions précises au niveau des enregistrements qui peuvent avoir un impact sur les données associées entre les jeux de données connectés. Ces fonctionnalités de suppression affectent l’intégrité des données, la conformité et le comportement des applications en aval, quel que soit votre cas d’utilisation spécifique. Examinez les [exigences en matière d’hygiène des données](../../hygiene/ui/record-delete.md#model-based-record-delete) et planifiez les scénarios de suppression avant la mise en œuvre.

### Sélection du comportement du schéma

Les schémas basés sur des modèles sont définis par défaut sur **comportement d’enregistrement**, qui capture le statut de l’entité (clients, comptes, etc.). Si vous avez besoin d’un **comportement de série temporelle** pour le suivi des événements, vous devez le configurer explicitement.

### Comparaison des méthodes d’ingestion

Utilisez ce tableau de comparaison pour choisir la méthode d’ingestion la mieux adaptée à vos besoins en matière de données, que vous ayez besoin d’une synchronisation en temps réel, d’une transformation SQL ou de chargements manuels de fichiers.

| Méthode d’ingestion | Exemple d’utilisation |
| ----------------------- | -------------------------------------------------------------- |
| **Modifier la capture de données** | Synchronisation en temps réel à partir des entrepôts cloud pris en charge |
| **Distiller de données** | Workflows d’ingestion et de transformation SQL |
| **Chargement de fichier** | Ingestion manuelle/par lots lorsque l’intégration source n’est pas disponible |

### Limites de la relation

Data Mirror prend en charge les relations **un-à-un** et **plusieurs-à-un** à l’aide de descripteurs. Les relations **plusieurs à plusieurs** nécessitent une modélisation supplémentaire et ne sont pas directement prises en charge.

## Étapes suivantes

Après avoir consulté cette présentation, vous devriez être en mesure de déterminer si Data Mirror correspond à votre cas d’utilisation et de comprendre les exigences de mise en œuvre. Pour commencer :

1. Les **architectes des données** doivent évaluer votre modèle de données pour s’assurer qu’il prend en charge les clés primaires, le contrôle de version et les fonctionnalités de suivi des modifications.
2. **Les parties prenantes de l’entreprise** doivent confirmer que votre licence comprend la prise en charge des schémas basés sur des modèles et les éditions Experience Platform requises.
3. Les **concepteurs de schémas** doivent planifier la structure de votre schéma pour identifier les descripteurs requis, les relations entre les champs et les besoins en matière de gouvernance des données.
4. Les **équipes d’implémentation** doivent choisir une méthode d’ingestion en fonction de vos systèmes sources, des exigences en temps réel et des workflows opérationnels.

Pour plus d’informations sur l’implémentation, consultez la [documentation sur les schémas basés sur des modèles](../schema/model-based.md).
