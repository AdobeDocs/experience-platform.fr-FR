---
title: Création d’audiences à l’aide de SQL
description: Découvrez comment utiliser l’extension d’audience SQL dans Adobe Experience Platform Data Distiller pour créer, gérer et publier des audiences à l’aide de commandes SQL. Ce guide couvre tous les aspects du cycle de vie de l’audience, notamment la création, la mise à jour et la suppression de profils, ainsi que l’utilisation de définitions d’audience pilotées par les données pour cibler des destinations basées sur des fichiers.
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 2%

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

## Activer des audiences vers les destinations {#activate-audiences}

Activez vos audiences en les ciblant sur n’importe quelle destination basée sur des fichiers, telle que [!DNL Amazon S3], [!DNL SFTP] ou [!DNL Azure Blob]. Les attributs d’audience enrichis peuvent être affinés et filtrés selon les besoins.

![ Diagramme de flux des types de destinations Adobe Experience Platform, présentant les destinations publiques et privées/personnalisées, y compris les options de lot et de diffusion en continu.](../images/data-distiller/sql-audiences/destination-types.png)

## Clarifications des fonctionnalités {#faqs}

Cette section traite des questions fréquentes sur la création et la gestion d’audiences externes à l’aide de SQL dans Data Distiller.

**Questions** :

- La création d’audience est-elle prise en charge uniquement pour les jeux de données plats ?

+++Réponse

Actuellement, la création de l’audience est limitée aux attributs plats (au niveau racine) lors de la définition de l’audience.

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

Oui, le jeu de données associé à l’audience est créé sur le lac de données. Les attributs de ce jeu de données sont disponibles dans le compositeur d’audience et le flux de destination sous forme d’attributs enrichis.

+++

- Les attributs de l’audience sont-ils limités aux destinations basées sur des fichiers de lot d’entreprise ? (Oui ou Non)

+++Réponse

Non. Les attributs enrichis dans l’audience peuvent être utilisés dans des destinations par lots d’entreprise et des destinations basées sur des fichiers. Si vous rencontrez une erreur du type &quot;Les identifiants de segment suivants ont des espaces de noms non autorisés pour cette destination : e917f626-a038-42f7-944c-xyxyx&quot;, créez un segment dans Data Distiller et utilisez-le avec n’importe quelle destination disponible.

+++

- Puis-je créer une audience d’audiences qui utilise une audience Distiller de données ?

+++Réponse

Oui, vous pouvez créer une audience qui utilise une audience Distiller de données.

+++

- Ces audiences s’affichent-elles dans Adobe Journey Optimizer ? Dans le cas contraire, que se passe-t-il lorsque je crée une audience dans le créateur de règles qui inclut tous les membres de cette audience ?

+++Réponse

Les audiences du Distilleur de données ne sont actuellement pas disponibles dans Adobe Journey Optimizer. Pour être disponible dans Adobe Journey Optimizer, vous devez créer une audience dans le créateur de règles Adobe Journey Optimizer.

+++

- Les audiences Data Distiller sont-elles supprimées tous les 30 jours puisqu’elles sont des audiences externes ?

+++Réponse

Oui, les audiences Distiller de données sont supprimées tous les 30 jours puisqu’il s’agit d’audiences externes.

+++

## Étapes suivantes

Après avoir lu ce document, vous avez appris à utiliser l’extension d’audience SQL dans Data Distiller pour créer, gérer et publier efficacement des audiences à l’aide de commandes SQL. Vous pouvez désormais personnaliser les définitions d’audience en fonction de vos besoins commerciaux uniques et les activer dans différentes destinations, afin d’optimiser vos stratégies marketing et vos décisions basées sur les données.

Vous pouvez ensuite lire la documentation suivante pour développer et optimiser vos stratégies de gestion de l’audience Platform :

- **Explorer l’évaluation de l’audience** : découvrez les [méthodes d’évaluation de l’audience dans Adobe Experience Platform](../../segmentation/home.md#evaluate-segments) : segmentation par flux pour les mises à jour en temps réel, segmentation par lots pour le traitement planifié ou à la demande et segmentation de périphérie pour l’évaluation instantanée sur l’Edge Network.
- **Intégration avec les destinations** : lisez le guide sur l’[exportation de fichiers à la demande vers des destinations par lot](../../destinations/ui/export-file-now.md) à l’aide de l’interface utilisateur Destinations de plateforme.
- **Réviser les performances de l’audience** : analysez les performances de vos audiences définies par SQL sur différents canaux. Utilisez les informations sur les données pour ajuster et améliorer vos définitions d’audience et vos stratégies de ciblage. Lisez le document sur [Audience insights](../../dashboards/insights/audiences.md) pour savoir comment accéder aux requêtes SQL et les adapter aux informations sur les audiences dans Adobe Real-Time CDP. Vous pouvez ensuite créer vos propres insights et transformer les données brutes en informations exploitables en personnalisant le tableau de bord Audiences afin de visualiser et d’utiliser efficacement ces informations pour une meilleure prise de décision.
