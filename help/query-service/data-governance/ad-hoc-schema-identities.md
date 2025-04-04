---
title: Définition d’identités de Principal dans un jeu de données ad hoc
description: Adobe Experience Platform Query Service vous permet de définir une identité ou une identité principale pour les champs de jeux de données de schéma ad hoc directement via la commande SQL ALTER TABLE. Le document explique comment utiliser la commande ALTER TABLE pour définir une identité principale ou une identité secondaire.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Définition des identités principales dans un jeu de données ad hoc

Adobe Experience Platform Query Service vous permet de marquer les colonnes de jeux de données comme identités principales ou secondaires à l’aide de contraintes pour la commande SQL `ALTER TABLE`. Vous pouvez utiliser cette fonctionnalité pour vous assurer que les champs marqués sont conformes aux exigences de confidentialité des données. Cette commande vous permet d’ajouter ou de supprimer des contraintes pour les colonnes de table d’identités principale et secondaire directement via SQL.

## Commencer

Étiqueter les colonnes du jeu de données comme identité principale ou secondaire nécessite une compréhension de la commande SQL `ALTER TABLE` et une bonne compréhension des exigences en matière de confidentialité des données. Avant de poursuivre avec ce document, consultez la documentation suivante :

* [Guide de syntaxe SQL de la commande `ALTER TABLE`](../sql/syntax.md).
* [Présentation de la gouvernance des données](../../data-governance/home.md) pour plus d’informations.

## Ajouter des contraintes {#add-constraints}

La commande `ALTER TABLE` vous permet d’étiqueter une colonne de jeu de données comme identité d’une personne, puis d’utiliser ce libellé comme identité principale en mettant à jour les métadonnées associées à l’aide de SQL. Cela s’avère particulièrement utile lorsque les jeux de données sont créés via SQL plutôt que directement à partir d’un schéma via l’interface utilisateur d’Experience Platform. La commande peut être utilisée pour vous assurer que vos opérations de données dans Experience Platform sont conformes aux politiques d’utilisation des données.

**Exemples**

L&#39;exemple suivant ajoute une contrainte au tableau `t1` existant. Les valeurs de la colonne `id` sont désormais marquées comme identités principales sous l’espace de noms `IDFA` . Un espace de noms d’identité est un mot-clé qui déclare le type de données d’identité que le champ représente.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Le deuxième exemple garantit que la colonne `id` est marquée comme identité secondaire.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Supprimer les contraintes {#drop-constraints}

Les contraintes peuvent également être supprimées des colonnes du tableau à l’aide de la commande `ALTER TABLE`.

**Exemples**

L&#39;exemple suivant supprime l&#39;exigence que la colonne `c1` soit étiquetée comme identité principale dans la table `t1` existante.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Comme illustré ci-dessous, la même syntaxe est utilisée pour lors de la suppression d’une contrainte d’identité.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Afficher les identités

Utilisez la `show identities` de commande des métadonnées de l’interface de ligne de commande pour afficher un tableau avec chaque attribut affecté en tant qu’identité.

```shell
> show identities;
```

Un exemple de tableau renvoyé est affiché ci-dessous.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## Limites de XDM {#limitations}

La liste suivante explique les points importants à prendre en compte pour la mise à jour des identités dans les jeux de données existants lors de l’utilisation de XDM.

* Pour définir une colonne en tant qu’identité, vous **devez** également définir l’espace de noms à conserver en tant que métadonnées pour la colonne.
* XDM ne prend pas en charge la spécification d’un nom de colonne dans l’attribut espace de noms .
* Si votre schéma utilise le champ XDM `identityMap`, l’objet `identityMap` racine ou de niveau supérieur **doit** doit être étiqueté comme identité ou identité principale.
