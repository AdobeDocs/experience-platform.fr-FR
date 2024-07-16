---
title: Définition d’identités de Principal dans un jeu de données ad hoc
description: Adobe Experience Platform Query Service vous permet de définir une identité ou une identité principale pour les champs de jeu de données de schéma ad hoc directement via la commande SQL ALTER TABLE. Le document explique comment utiliser la commande ALTER TABLE pour définir une identité principale ou une identité secondaire.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Définition des identités principales dans un jeu de données ad hoc

Adobe Experience Platform Query Service vous permet de marquer les colonnes de jeux de données comme identités primaires ou secondaires à l’aide de contraintes pour la commande SQL `ALTER TABLE`. Vous pouvez utiliser cette fonction pour vous assurer que les champs marqués sont conformes aux exigences de confidentialité des données. Cette commande vous permet d’ajouter ou de supprimer des contraintes pour les colonnes de table d’identités primaire et secondaire directement via SQL.

## Commencer

L’étiquetage des colonnes de jeux de données comme identité principale ou secondaire nécessite une compréhension de la commande SQL `ALTER TABLE` et une bonne compréhension des exigences en matière de confidentialité des données. Avant de poursuivre avec ce document, veuillez consulter la documentation suivante :

* [Guide de syntaxe SQL pour la commande `ALTER TABLE`](../sql/syntax.md).
* [Présentation de la gouvernance des données](../../data-governance/home.md) pour plus d’informations.

## Ajouter des contraintes {#add-constraints}

La commande `ALTER TABLE` vous permet de libeller une colonne de jeu de données en tant qu’identité d’une personne, puis d’utiliser cette étiquette en tant qu’identité principale en mettant à jour les métadonnées associées à l’aide de SQL. Cela s’avère particulièrement utile lorsque des jeux de données sont créés via SQL plutôt que directement à partir d’un schéma via l’interface utilisateur de Platform. La commande peut être utilisée pour vous assurer que vos opérations de données dans Platform sont conformes aux stratégies d’utilisation des données.

**Exemples**

L’exemple suivant ajoute une contrainte à la table `t1` existante. Les valeurs de la colonne `id` sont désormais marquées comme identités principales sous l’espace de noms `IDFA`. Un espace de noms d’identité est un mot-clé qui déclare le type de données d’identité que le champ représente.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Le deuxième exemple garantit que la colonne `id` est marquée comme une identité secondaire.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Contraintes de perte {#drop-constraints}

Les contraintes peuvent également être supprimées des colonnes de tableau à l’aide de la commande `ALTER TABLE`.

**Exemples**

L’exemple suivant supprime l’obligation que la colonne `c1` soit étiquetée comme identité principale dans la table `t1` existante.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Comme illustré ci-dessous, la même syntaxe est utilisée lors de la suppression d’une contrainte d’identité.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Afficher les identités

Utilisez la commande de métadonnées `show identities` de l’interface de ligne de commande pour afficher un tableau avec tous les attributs affectés en tant qu’identité.

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

* Pour spécifier une colonne comme identité, vous **devez** définir également l’espace de noms à conserver en tant que métadonnées pour la colonne.
* XDM ne prend pas en charge la spécification d’un nom de colonne dans l’attribut d’espace de noms.
* Si votre schéma utilise le champ XDM `identityMap`, la racine ou l’objet `identityMap` de niveau supérieur **doit** être étiqueté comme identité ou identité principale.
