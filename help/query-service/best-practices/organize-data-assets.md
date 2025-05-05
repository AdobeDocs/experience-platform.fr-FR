---
title: Bonnes pratiques relatives à l’organisation des ressources de données dans Query Service
description: Ce document décrit un moyen logique d’organiser les données pour faciliter leur utilisation avec Query Service.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# Organisation des ressources de données dans Query Service

Ce document fournit des conseils sur les bonnes pratiques d’organisation des ressources de données, notamment les jeux de données, les vues et les tables temporaires à utiliser avec Adobe Experience Platform Query Service. Il explique comment structurer vos données et explique comment accéder à ces informations, les mettre à jour et les supprimer.

Il est important d’organiser logiquement vos ressources de données dans le [!DNL Data Lake] Experience Platform au fur et à mesure de leur croissance. Query Service étend les constructions SQL qui vous permettent de regrouper logiquement des ressources de données dans un sandbox. Cette méthode d’organisation permet de partager des ressources de données entre les schémas sans avoir à les déplacer physiquement.

## Commencer

Avant de poursuivre avec ce document, vous devez bien comprendre les fonctionnalités de [Query Service](../home.md) et avoir lu le guide de l’interface utilisateur [&#128279;](../ui/user-guide.md).

## Organisation des données dans Query Service

Les exemples suivants montrent les éléments que vous pouvez créer via Adobe Experience Platform Query Service pour organiser logiquement vos données à l’aide d’une syntaxe SQL standard. Commencez par créer une base de données qui servira de conteneur pour vos points de données. Une base de données peut contenir un ou plusieurs schémas, chaque schéma pouvant alors comporter une ou plusieurs références à un actif de données (jeux de données, vues, tables temporaires, etc.). Ces références incluent toutes les relations ou associations entre les jeux de données.

Consultez le [guide d’utilisation de Query Editor](../ui/user-guide.md) pour obtenir des conseils détaillés sur l’utilisation de l’interface utilisateur de Query Service pour créer des requêtes SQL.

Les éléments SQL suivants permettant d’organiser logiquement les jeux de données dans un sandbox sont pris en charge.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

L’exemple (légèrement tronqué pour des raisons de concision) illustre cette méthodologie où `databaseA` contient des `schema1` de schéma.

## Association de ressources de données à un schéma

Une fois qu’un schéma a été créé pour servir de conteneur aux ressources de données, chaque jeu de données peut être associé à un ou plusieurs schémas dans la base de données à l’aide de la syntaxe SQL ALTER TABLE standard.

L’exemple suivant ajoute `dataset1`, `dataset2`, `dataset3` et `v1` au conteneur `databaseA.schema1` créé dans l’exemple précédent.

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## Accès aux ressources de données à partir du conteneur de données

En qualifiant correctement le nom de la base de données, tout client [!DNL PostgreSQL] peut se connecter à l’une des structures de données que vous avez créées à l’aide du mot-clé SHOW. Pour plus d’informations sur le mot-clé SHOW, reportez-vous à la section [SHOW de la documentation sur la syntaxe SQL](../sql/syntax.md#show).

« all » est le nom de base de données par défaut qui contient chaque base de données et conteneur de schéma dans un sandbox. Lorsque vous établissez une connexion [!DNL PostgreSQL] à l’aide de `dbname="all"`, vous pouvez accéder à la base de données et au schéma **n’importe lequel** que vous avez créés pour organiser logiquement vos données.

La liste de toutes les bases de données sous `dbname="all"` affiche trois bases de données disponibles.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

La liste de tous les schémas sous `dbname="all"` affiche les trois schémas associés à chaque base de données dans le sandbox.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Lorsque vous établissez une connexion [!DNL PostgreSQL] à l’aide de `dbname="databaseA"`, vous pouvez accéder à n’importe quel schéma associé à cette base de données spécifique, comme illustré dans l’exemple ci-dessous.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

La notation par points vous permet d’accéder à chaque table associée à un schéma spécifique connecté à la base de données de votre choix. Lorsque vous vous connectez à `DBNAME = databaseA.schema1;`, toutes les tables associées à ce schéma spécifique (`schema1`) s’affichent. Cela fournit des informations sur le jeu de données qui contient la table.

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## Mettre à jour ou supprimer des ressources de données d’un conteneur de données

À mesure que la quantité de ressources de données dans votre organisation (ou sandbox) augmente, il devient nécessaire de mettre à jour ou de supprimer des ressources de données d’un conteneur de données. Les ressources individuelles peuvent être supprimées du conteneur d’organisation en référençant la base de données et le nom de schéma appropriés à l’aide de la notation par points. Le tableau et la vue (`t1` et `v1` respectivement) ajoutés à `databaseA.schema1` dans le premier exemple sont supprimés à l’aide de la syntaxe dans l’exemple suivant.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Suppression de ressources de données

La fonction [DROP TABLE](../sql/syntax.md#drop-table) ne supprime physiquement une ressource de données du [!DNL Data Lake] que lorsqu’une seule référence à la table existe dans toutes les bases de données de votre organisation.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Supprimer un conteneur de ressources de données

La base de données et le schéma peuvent également être supprimés à l’aide des fonctions SQL standard.

#### Supprimer une base de données

S’il existe d’autres références à des ressources de données associées à la base de données, la fonction renvoie une erreur lors de la tentative de suppression de la base de données.

```sql
DROP DATABASE databaseA;
```

#### Suppression d’un schéma

Trois points importants doivent être pris en compte lors de la suppression d’un schéma :

- La suppression d’un schéma ne supprime pas physiquement les ressources de données telles que les tables, les vues ou les tables temporaires.
- S’il existe des ressources de données référencées dans le schéma cible et que le mode est RESTREINDRE, une exception est générée.
- Si des ressources de données sont référencées dans le schéma cible et que le mode est CASCADE, le système supprime toutes les ressources de données référencées par le conteneur de schéma, puis supprime le conteneur de schéma.

```sql
DROP SCHEMA databaseA.schema2;
```

## Étapes suivantes

Grâce à la lecture de ce document, vous avez maintenant une meilleure compréhension des bonnes pratiques concernant l’organisation et la structure de vos ressources de données à utiliser avec Adobe Experience Platform Query Service. Il est recommandé de continuer à découvrir les bonnes pratiques de Query Service en consultant la [documentation sur la déduplication des données](../key-concepts/deduplication.md).
