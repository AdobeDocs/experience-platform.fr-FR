---
title: Création d’audiences à l’aide de SQL
description: Découvrez comment utiliser l’extension d’audience SQL dans Adobe Experience Platform Data Distiller pour créer, gérer et publier des audiences à l’aide de commandes SQL. Ce guide couvre tous les aspects du cycle de vie de l’audience, notamment la création, la mise à jour et la suppression de profils, ainsi que l’utilisation de définitions d’audience pilotées par les données pour cibler des destinations basées sur des fichiers.
source-git-commit: 8b9a46d9dd35a60fc3f3087d5fd3c4dad395b1aa
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 1%

---

# Création d’audiences à l’aide de SQL

Ce document explique comment utiliser l’extension d’audience SQL dans Adobe Experience Platform Data Distiller pour créer, gérer et publier des audiences à l’aide de commandes SQL.

Utilisez l’extension d’audience SQL pour créer des audiences avec les données du lac de données, y compris toutes les entités de dimension existantes. Cette extension vous permet de définir des segments d’audience directement à l’aide de SQL, ce qui offre une certaine flexibilité sans avoir besoin de données brutes dans vos profils. Les audiences créées à l’aide de cette méthode sont automatiquement enregistrées dans l’espace de travail Audience, où vous pouvez les cibler davantage vers des destinations basées sur des fichiers.

![Infographie montrant le workflow d’extension de l’audience SQL. Les étapes incluent la création d’audiences avec Query Service à l’aide de commandes SQL, leur gestion dans l’interface utilisateur de Platform, afin de les activer dans des destinations basées sur des fichiers.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

## Cycle de vie de la création d’audience dans Data Distiller {#audience-creation-lifecycle}

Pour gérer efficacement vos audiences, procédez comme suit. Les audiences créées s’intègrent de manière transparente dans le flux d’audience, ce qui vous permet de créer des segments à partir de ces audiences de base et des destinations basées sur des fichiers cibles pour le ciblage des clients. Utilisez les commandes SQL suivantes pour [créer](#create-audience), [modifier](#add-profiles-to-audience) et [supprimer](#delete-audience) des audiences dans Adobe Experience Platform.

### Créer une audience {#create-audience}

Utilisez la commande `CREATE AUDIENCE AS SELECT` pour définir une nouvelle audience. L’audience créée est enregistrée dans un jeu de données et enregistrée dans l’espace de travail [!UICONTROL Audiences] sous Data Distiller.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title']) 
AS (select_query)
```

**Paramètres**

Utilisez ces paramètres pour définir votre requête de création d&#39;audience SQL :

| Paramètre | Description |
|--------------------|------------------------------------------------------------------|
| `schema` | Facultatif. Définit le schéma XDM du jeu de données créé par la requête. |
| `table_name` | Nom de la table et de l&#39;audience. |
| `primary_identity` | Indique la colonne d’identité principale de l’audience. |
| `identity_namespace` | Espace de noms de l’identité. |
| `select_query` | Une instruction SELECT définissant l’audience. La syntaxe de la requête SELECT se trouve dans la section [Requêtes SELECT](../sql/syntax.md#select-queries) . |

{style="table-layout:auto"}

**Exemple :**

L&#39;exemple suivant montre comment structurer votre requête de création d&#39;audience SQL :

```sql
CREATE Audience aud_test 
WITH (primary_identity=month, identity_namespace=queryService) 
AS SELECT month FROM profile_dim_date LIMIT 5;
```

**Limites :**

Tenez compte des limites suivantes lors de l’utilisation de SQL pour la création d’audience :

- La colonne d&#39;identité principale **doit** se trouve au niveau racine.
- Les nouveaux lots remplacent les jeux de données existants ; la fonctionnalité d’ajout n’est actuellement pas prise en charge.
- Les attributs imbriqués ne sont actuellement pas pris en charge.

### Ajouter des profils à une audience existante {#add-profiles-to-audience}

Utilisez la commande `INSERT INTO` pour ajouter des profils à une audience existante.

```sql
INSERT INTO table_name 
SELECT select_query
```

**Paramètres**

Le tableau ci-dessous explique les paramètres requis pour la commande `INSERT INTO` :

| Paramètre | Description |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | Nom de la table qui a été créée dans le cadre de la commande de création d’audience. |
| `select_query` | Instruction SELECT. La syntaxe de la requête SELECT se trouve dans la section Requêtes SELECT . |

{style="table-layout:auto"}

**Exemple :**

L’exemple suivant montre comment ajouter des profils à une audience existante avec la commande `INSERT INTO` :

```sql
INSERT INTO Audience aud_test 
SELECT month FROM profile_dim_date LIMIT 10;
```

### Suppression d’une audience (DROP AUDIENCE) {#delete-audience}

Utilisez la commande `DROP AUDIENCE` pour supprimer une audience existante. Si l’audience n’existe pas, une exception se produit, sauf si `IF EXISTS` est spécifié.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**Paramètres**

La table contient les paramètres requis pour la commande `DROP AUDIENCE` :

| Paramètre | Description |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | Facultatif. Si spécifié, dans le cas où la table est introuvable, aucune exception n’est générée. |
| `db_name` | Indique le groupe de données utilisé pour qualifier le jeu de données d’audience. |
| `table_name` | Nom de la table qui a été créée dans le cadre de la commande de création d’audience. |

{style="table-layout:auto"}

**Exemple :**

L’exemple suivant montre comment supprimer une audience à l’aide de la commande DROP AUDIENCE :

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### Publication automatique d’audiences {#auto-publish-audiences}

Les audiences créées à l’aide de l’extension SQL s’enregistrent automatiquement sous Data Distiller dans l’espace de travail Audience. Une fois enregistrées, ces audiences sont disponibles pour le ciblage et peuvent être utilisées dans des destinations basées sur des fichiers, ce qui améliore votre segmentation et vos stratégies de ciblage.

![L’espace de travail Audience dans Adobe Experience Platform, présentant les audiences Distiller de données automatiquement publiées et prêtes à l’emploi.](../images/data-distiller/sql-audiences/audiences.png)

## Activation des audiences vers les destinations {#activate-audiences}

Activez vos audiences en les ciblant sur n’importe quelle destination basée sur des fichiers, telle que [!DNL Amazon S3], [!DNL SFTP] ou [!DNL Azure Blob]. Les attributs d’audience enrichis peuvent être affinés et filtrés selon les besoins.

![ Diagramme de flux des types de destinations Adobe Experience Platform, présentant les destinations publiques et privées/personnalisées, y compris les options de lot et de diffusion en continu.](../images/data-distiller/sql-audiences/destination-types.png)

## Clarifications des fonctionnalités {#faqs}

Cette section traite des questions fréquentes sur la création et la gestion d’audiences externes à l’aide de SQL dans Data Distiller.

+++Sélectionner pour afficher les questions et réponses

**Questions** :

- La création d’audience est-elle prise en charge uniquement pour les jeux de données plats ?

+++Réponse

Les jeux de données imbriqués sont également pris en charge, mais seuls les attributs plats sont disponibles dans l’audience.

+++

- La création d’audience génère-t-elle un ou plusieurs jeux de données uniques ou varie-t-elle en fonction de la configuration ?

+++Réponse

Il existe un mappage un-à-un entre une audience et un jeu de données.

+++

- Le jeu de données créé lors de la création de l’audience est-il marqué pour Profile ?

+++Réponse

Non, le jeu de données créé lors de la création de l’audience n’est pas marqué pour Profile.

+++

- Le jeu de données est-il créé sur le lac de données ?

+++Réponse

Oui, le jeu de données est créé sur le lac de données.

+++

- Les attributs de l’audience sont-ils limités à une utilisation uniquement dans les destinations basées sur des fichiers de lot d’entreprise ? (Oui ou Non)

+++Réponse

Oui, les attributs de l’audience sont limités pour une utilisation uniquement dans les destinations basées sur des fichiers de lot d’entreprise.

+++

- Puis-je créer une audience d’audiences qui utilise une audience Distiller de données ?

+++Réponse

Oui, vous pouvez créer une audience qui utilise une audience Distiller de données.

+++

- Ces audiences s’affichent-elles dans Adobe Journey Optimizer ? Dans le cas contraire, que se passe-t-il lorsque je crée une audience dans le créateur de règles qui inclut tous les membres de cette audience ?

+++Réponse

Les audiences du Distilleur de données ne sont actuellement pas disponibles dans Adobe Journey Optimizer. Pour être disponible dans Adobe Journey Optimizer, vous devez créer une audience dans le créateur de règles Adobe Journey Optimizer.

+++

- Comment créer deux audiences Distiller de données avec des plannings différents ? Combien de jeux de données sont créés et sont-ils marqués pour Profile ?

+++Réponse

Deux jeux de données seront créés, car chaque audience possède un jeu de données sous-jacent. Toutefois, ces jeux de données ne sont pas marqués pour Profile. Les deux jeux de données sont gérés selon leurs propres plannings.

+++

- Comment supprimer une audience ?

+++Réponse

Pour supprimer une audience, vous pouvez utiliser la commande [`DROP AUDIENCE`](#delete-audience) dans l’interface de ligne de commande ou utiliser les [ actions rapides de l’espace de travail Audiences](../../segmentation/ui/audience-portal.md#quick-actions). REMARQUE : les audiences utilisées dans des destinations en aval ou dépendantes d’autres audiences ne peuvent pas être supprimées.

+++

- Lorsque je publie une audience dans Profile, à quelle heure est-elle disponible dans l’interface utilisateur du créateur de segments et quand est-elle disponible dans les destinations ?

+++Réponse

Une fois l’exportation de l’instantané de profil terminée, les profils sont visibles dans l’audience.

+++

- Les audiences Data Distiller sont-elles supprimées tous les 30 jours puisqu’elles sont des audiences externes ?

+++Réponse

Oui, les audiences Distiller de données sont supprimées tous les 30 jours puisqu’il s’agit d’audiences externes.

+++

- Les audiences Data Distiller apparaissent-elles dans l’inventaire des audiences ?

+++Réponse

Oui, les audiences Distiller de données apparaissent dans l’inventaire des audiences sous le nom d’origine &quot;Distiller de données&quot;.

+++

+++

## Étapes suivantes

Après avoir lu ce document, vous avez appris à utiliser l’extension d’audience SQL dans Data Distiller pour créer, gérer et publier efficacement des audiences à l’aide de commandes SQL. Vous pouvez désormais personnaliser les définitions d’audience en fonction de vos besoins commerciaux uniques et les activer dans différentes destinations, afin d’optimiser vos stratégies marketing et vos décisions basées sur les données.

Vous pouvez ensuite lire la documentation suivante pour développer et optimiser vos stratégies de gestion de l’audience Platform :

- **Explorer l’évaluation de l’audience** : découvrez les [méthodes d’évaluation de l’audience dans Adobe Experience Platform](../../segmentation/home.md#evaluate-segments) : segmentation par flux pour les mises à jour en temps réel, segmentation par lots pour le traitement planifié ou à la demande et segmentation de périphérie pour l’évaluation instantanée sur l’Edge Network.
- **Intégration avec les destinations** : lisez le guide sur l’[exportation de fichiers à la demande vers des destinations par lot](../../destinations/ui/export-file-now.md) à l’aide de l’interface utilisateur Destinations de plateforme.
- **Réviser les performances de l’audience** : analysez les performances de vos audiences définies par SQL sur différents canaux. Utilisez les informations sur les données pour ajuster et améliorer vos définitions d’audience et vos stratégies de ciblage. Lisez le document sur [Audience insights](../../dashboards/insights/audiences.md) pour savoir comment accéder aux requêtes SQL et les adapter aux informations sur les audiences dans Adobe Real-time Customer Data Platform. Vous pouvez ensuite créer vos propres insights et transformer les données brutes en informations exploitables en personnalisant le tableau de bord Audiences afin de visualiser et d’utiliser efficacement ces informations pour une meilleure prise de décision.
