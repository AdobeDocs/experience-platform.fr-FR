---
title: Définition des identités Principal dans un jeu de données ad hoc
description: Adobe Experience Platform Query Service vous permet de définir une identité ou une identité Principale pour les champs de jeu de données de schéma ad hoc directement via la commande SQL ALTER TABLE. Le document explique comment utiliser la commande ALTER TABLE pour définir une identité Principale ou une identité secondaire.
source-git-commit: bf51fc3e0c9635c0555f87f3389fb4a9542c092d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Définition d’identités Principales dans un jeu de données ad hoc

Adobe Experience Platform Query Service vous permet de marquer les colonnes de jeux de données comme identités Principales ou secondaires à l’aide de contraintes pour SQL. `ALTER TABLE` . Vous pouvez utiliser cette fonction pour vous assurer que les champs marqués sont conformes aux exigences de confidentialité des données. Cette commande vous permet d’ajouter ou de supprimer des contraintes pour les colonnes de table d’identités Principales et secondaires directement via SQL.

## Prise en main

L’étiquetage des colonnes de jeux de données comme identité Principale ou secondaire nécessite une compréhension de la `ALTER TABLE` la commande SQL et une bonne compréhension des exigences en matière de confidentialité des données. Avant de poursuivre avec ce document, veuillez consulter la documentation suivante :

* [Le guide de syntaxe SQL pour la variable `ALTER TABLE` command](../sql/syntax.md).
* [Présentation de la gouvernance des données](../../data-governance/home.md) pour plus d’informations.

## Ajouter des contraintes {#add-constraints}

Le `ALTER TABLE` vous permet d’étiqueter une colonne de jeu de données en tant qu’identité d’une personne, puis d’utiliser cette étiquette en tant qu’identité Principale en mettant à jour les métadonnées associées à l’aide de SQL. Cela s’avère particulièrement utile lorsque des jeux de données sont créés via SQL plutôt que directement à partir d’un schéma via l’interface utilisateur de Platform. La commande peut être utilisée pour vous assurer que vos opérations de données dans Platform sont conformes aux stratégies d’utilisation des données.

**Exemples**

L’exemple suivant ajoute une contrainte à la variable `t1` table. Les valeurs de la variable `id` sont désormais marquées comme identités Principales sous la variable `IDFA` espace de noms. Un espace de noms d’identité est un mot-clé qui déclare le type de données d’identité que le champ représente.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Le deuxième exemple garantit que la variable `id` est marquée comme identité secondaire.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Contraintes de perte {#drop-constraints}

Les contraintes peuvent également être supprimées des colonnes du tableau à l’aide de la variable `ALTER TABLE` .

**Exemples**

L’exemple suivant supprime l’obligation que la variable `c1` être étiquetée comme identité Principale dans la `t1` table.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Comme illustré ci-dessous, la même syntaxe est utilisée lors de la suppression d’une contrainte d’identité.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Afficher les identités

Utilisation de la commande de métadonnées `show identities` depuis l’interface de ligne de commande pour afficher un tableau avec tous les attributs affectés en tant qu’identité.

```shell
> show identities;
```

Un exemple de tableau renvoyé est présenté ci-dessous.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## Limites XDM {#limitations}

La liste suivante explique les points importants à prendre en compte pour la mise à jour des identités dans les jeux de données existants lors de l’utilisation de XDM.

* Pour définir une colonne comme identité, vous devez **must** définissez également l’espace de noms à conserver en tant que métadonnées pour la colonne.
* XDM ne prend pas en charge la spécification d’un nom de colonne dans l’attribut d’espace de noms.
* Si votre schéma utilise la variable `identityMap` Champ XDM, racine ou niveau supérieur `identityMap` objet **must** être étiquetées comme identité ou identité Principale.
