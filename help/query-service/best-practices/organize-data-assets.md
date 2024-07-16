---
title: Bonnes pratiques pour l’organisation des ressources de données dans Query Service
description: Ce document décrit un moyen logique d’organiser les données pour faciliter leur utilisation avec Query Service.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# Organisation des ressources de données dans Query Service

Ce document fournit des conseils sur les bonnes pratiques relatives à l’organisation des ressources de données, notamment les jeux de données, les vues et les tableaux temporaires, en vue de leur utilisation avec Adobe Experience Platform Query Service. Il explique comment structurer vos données et comment accéder à ces informations, les mettre à jour et les supprimer.

Il est important d’organiser logiquement vos ressources de données dans la plateforme [!DNL Data Lake] au fur et à mesure de leur développement. Query Service étend les constructions SQL qui vous permettent de regrouper logiquement les ressources de données dans un environnement de test. Cette méthode d’organisation permet le partage de ressources de données entre les schémas sans avoir à les déplacer physiquement.

## Commencer

Avant de poursuivre ce document, vous devez bien comprendre les fonctionnalités de [Query Service](../home.md) et avoir lu le [ guide de l’interface utilisateur](../ui/user-guide.md).

## Organisation des données dans Query Service

Les exemples suivants montrent les éléments disponibles par le biais de Adobe Experience Platform Query Service pour organiser logiquement vos données à l’aide de la syntaxe SQL standard. Vous devez commencer par créer une base de données qui servira de conteneur à vos points de données. Une base de données peut contenir un ou plusieurs schémas, et chaque schéma peut alors comporter une ou plusieurs références à une ressource de données (jeux de données, vues, tables temporaires, etc.). Ces références incluent toute relation ou association entre les jeux de données.

Consultez le [guide d’utilisation de Query Editor](../ui/user-guide.md) pour obtenir des instructions détaillées sur l’utilisation de l’interface utilisateur de Query Service pour créer des requêtes SQL.

Les éléments SQL suivants pour organiser logiquement les jeux de données dans un environnement de test sont pris en charge.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

L’exemple (légèrement tronqué pour la concision) illustre cette méthodologie où `databaseA` contient le schéma `schema1`.

## Association de ressources de données à un schéma

Une fois qu’un schéma a été créé pour agir comme conteneur pour les ressources de données, chaque jeu de données peut être associé à un ou plusieurs schémas de la base de données en utilisant la syntaxe SQL ALTER TABLE standard.

L’exemple suivant ajoute `dataset1`, `dataset2`, `dataset3` et `v1` au conteneur `databaseA.schema1` créé dans l’exemple précédent.

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## Accès aux ressources de données à partir du conteneur de données

En qualifiant correctement le nom de la base de données, tout client [!DNL PostgreSQL] peut se connecter à l’une des structures de données que vous avez créées à l’aide du mot-clé SHOW. Pour plus d’informations sur le mot-clé SHOW, reportez-vous à la section [SHOW dans la documentation sur la syntaxe SQL](../sql/syntax.md#show).

&quot;all&quot; est le nom de base de données par défaut qui contient chaque conteneur de base de données et de schéma dans un environnement de test. Lorsque vous établissez une connexion [!DNL PostgreSQL] à l’aide de `dbname="all"`, vous pouvez accéder à la base de données et au schéma **n’importe quelle** que vous avez créés pour organiser logiquement vos données.

La liste de toutes les bases de données sous `dbname="all"` affiche trois bases de données disponibles.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

La liste de tous les schémas sous `dbname="all"` affiche les trois schémas associés à chaque base de données dans l’environnement de test.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Lorsque vous établissez une connexion [!DNL PostgreSQL] à l’aide de `dbname="databaseA"`, vous pouvez accéder à tout schéma associé à cette base de données spécifique, comme illustré dans l’exemple ci-dessous.

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

La notation par points permet d&#39;accéder à chaque table associée à un schéma spécifique connecté à la base de données de votre choix. En se connectant à `DBNAME = databaseA.schema1;`, toutes les tables associées à ce schéma spécifique (`schema1`) s’affichent. Vous obtenez ainsi des informations sur le jeu de données contenant le tableau.

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

## Mise à jour ou suppression de ressources de données d’un conteneur de données

À mesure que le nombre de ressources de données de votre entreprise (ou sandbox) augmente, il devient nécessaire de mettre à jour ou de supprimer des ressources de données d’un conteneur de données. Les ressources individuelles peuvent être supprimées du conteneur de l’organisation en référençant la base de données et le nom de schéma appropriés à l’aide de la notation par points. La table et la vue (`t1` et `v1` respectivement) ajoutées à `databaseA.schema1` dans le premier exemple sont supprimées à l’aide de la syntaxe de l’exemple suivant.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Suppression de ressources de données

La fonction [DROP TABLE](../sql/syntax.md#drop-table) supprime physiquement une ressource de données de [!DNL Data Lake] uniquement lorsqu’il existe une référence unique à la table dans toutes les bases de données de votre organisation.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Suppression d’un conteneur de ressources de données

La base de données et le schéma peuvent également être supprimés à l’aide de fonctions SQL standard.

#### Suppression d’une base de données

Si d’autres références aux ressources de données sont associées à la base de données, la fonction renvoie une erreur lors de la tentative de suppression de la base de données.

```sql
DROP DATABASE databaseA;
```

#### Suppression d’un schéma

Trois points importants doivent être pris en compte lors de la suppression d’un schéma :

- La suppression d’un schéma ne supprime pas physiquement les ressources de données telles que les tables, les vues ou les tables temporaires.
- Si des ressources de données sont référencées dans le schéma cible et que le mode est RESTRICT, une exception est générée.
- Si des ressources de données sont référencées dans le schéma cible et que le mode est CASCADE, le système supprime toutes les ressources de données référencées par le conteneur de schémas, puis supprime le conteneur de schémas.

```sql
DROP SCHEMA databaseA.schema2;
```

## Étapes suivantes

En lisant ce document, vous comprenez mieux les bonnes pratiques concernant l’organisation et la structure de vos ressources de données à utiliser avec Adobe Experience Platform Query Service. Il est recommandé de continuer à en apprendre davantage sur les bonnes pratiques de Query Service en lisant la [documentation sur la déduplication des données](../key-concepts/deduplication.md).
