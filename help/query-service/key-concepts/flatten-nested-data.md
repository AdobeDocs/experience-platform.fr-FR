---
keywords: Experience Platform;service de requête;Service de requête;structures de données imbriquées;données imbriquées;aplatir;aplatir les données imbriquées;
title: Aplatir les structures de données imbriquées à utiliser avec les outils BI
description: Ce document explique comment aplatir les schémas XDM pour toutes les tables et vues au cours d’une session lors de l’utilisation d’outils BI tiers avec le service de requête.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: fc98b111aa15cdeb64eacdc05cac33a00ee98d80
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 93%

---

# Aplatir les structures de données imbriquées à utiliser avec des outils BI tiers

Le service de requête Adobe Experience Platform prend en charge le paramètre `FLATTEN` lors de la connexion à une base de données par le biais d’outils BI tiers. Cette fonctionnalité aplatit les structures de données imbriquées dans des outils BI tiers pour améliorer leur utilisation et réduire la charge de travail requise pour récupérer, analyser, transformer et présenter des données.

De nombreux outils BI comme [!DNL Tableau] et [!DNL Power BI] ne prennent pas en charge les structures de données imbriquées de manière native. Le paramètre `FLATTEN` supprime la nécessité de créer des vues SQL en plus de vos données pour fournir une version aplatie ou d’utiliser les tâches `CTAS` ou `INSERT INTO` du service de requête pour dupliquer vos jeux de données en versions aplaties lors de l’utilisation de schémas ad hoc.

Le paramètre `FLATTEN` extrait la structure de chaque champ feuille dans la racine de la table et nomme le champ selon l’espace de noms d’origine. Vous pouvez ainsi utiliser la notation par points pour faire correspondre un champ à son chemin d’accès de modèle de données d’expérience (XDM) tout en préservant le contexte du champ.

## Conditions préalables

L’utilisation du paramètre `FLATTEN` nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système XDM](../../xdm/home.md) : présentation de XDM et de sa mise en œuvre dans Experience Platform.

   * [Création d’un schéma ad hoc](../../xdm/tutorials/ad-hoc.md) : un schéma XDM avec des champs dont l’espace de noms n’est utilisé que par un seul jeu de données est appelé schéma ad hoc. Les schémas ad hoc sont utilisés dans divers workflows d’ingestion de données pour Experience Platform et pour la création de certains types de connexions source.

* [Sandbox](../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

* [Structures de données imbriquées](./nested-data-structures.md) : ce document fournit des exemples de création, de traitement ou de transformation de jeux de données avec des types de données complexes, y compris des structures de données imbriquées.

## Connexion à une base de données à l’aide du paramètre FLATTEN {#connect-with-flatten}

Le paramètre `FLATTEN` aplatit les structures de données imbriquées dans des colonnes distinctes où le nom de l’attribut devient le nom de la colonne qui contient les valeurs de ligne. Lorsque vous utilisez des données dans des outils BI qui ne prennent pas en charge les structures de données imbriquées, ce paramètre améliore l’utilisation des schémas ad hoc et réduit la charge de travail nécessaire.

Lorsque vous vous connectez au service de requête avec le client tiers de votre choix, ajoutez le paramètre `FLATTEN` au nom de la base de données. Pour plus d’informations sur la connexion à un outil BI spécifique, consultez sa documentation respective dans la [présentation de la connexion des clients au service de requête](../clients/overview.md). La chaîne de connexion doit contenir :

* Le nom du sandbox.
* Un signe deux-points suivi de `all` ou un identifiant de jeu de données, un identifiant d’affichage ou un nom de base de données spécifique.
* Un point d’interrogation (?) suivi du mot-clé `FLATTEN`.

L’entrée doit avoir le format suivant :

```bash
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Voici un exemple de chaîne de connexion :

```bash
prod:all?FLATTEN
```

## Exemple {#example}

L’exemple de schéma utilisé dans ce guide utilise le groupe de champs standard [!UICONTROL Commerce Details], qui utilise la structure d’objet `commerce` et le tableau `productListItems` . Consultez la documentation XDM pour [plus d’informations sur le groupe de champs [!UICONTROL Commerce Details]](../../xdm/field-groups/event/commerce-details.md). Une représentation de la structure du schéma est visible dans l’image ci-dessous.

![Schéma du groupe de champs Détails du commerce comprenant les structures `commerce` et `productListItems`.](../images/key-concepts/commerce-details.png)

Si votre outil BI ne prend pas en charge les structures de données imbriquées, il peut être difficile de référencer des champs imbriqués s’ils contiennent des valeurs sérialisées (comme `commerce` et `productListItems` dans l’exemple de schéma). Ces valeurs peuvent apparaître sous la forme de parties d’un seul champ de chaîne `commerce` encodée et ne sont pas inutilisables de manière réalistique.

Les valeurs suivantes représentent `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) et `commerce.purchases.value`(1.0) dans les champs imbriqués mal formatés.

```bash
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

En utilisant le paramètre `FLATTEN`, vous pouvez accéder à des champs distincts dans votre schéma ou à des sections entières de la structure de données imbriquées à l’aide de la notation par points et de leur nom de chemin d’accès d’origine. Un exemple de ce format utilisant le group de champs `commerce` est donné ci-dessous.

```bash
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

Le paramètre `FLATTEN` présente certaines limites lors de l’utilisation d’autres structures de données. Vous trouverez des détails complets dans la [section sur les limites](#limitations).

### Utiliser des guillemets pour les champs dans les requêtes {#quotation-marks}

Les champs racine aplatis utilisent désormais la notation par points pour correspondre à leurs chemins XDM. Lorsqu’ils sont utilisés dans une requête, les champs doivent être placés entre guillemets (&quot; &quot;).

L’exemple SQL ci-dessous affiche le statut d’origine de la requête imbriquée :

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Lors de l’utilisation des champs de données aplaties, la requête est écrite à l’aide de la notation par points et mise entre guillemets, comme dans l’exemple ci-dessous :

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Limites {#limitations}

Le paramètre `FLATTEN` n’aplatit actuellement pas les structures de données suivantes :

| Structure des données | Limite |
|---|---|
| Tableaux | Utilisez un index de tableau explicite pour la fonction `EXPLODE` afin d’accéder aux tableaux. |
| Mappages | Utilisez la clé de chaîne pour accéder à une valeur sous un mappage pour accéder aux mappages. |

Pour résoudre les limites des mappages et des tableaux, vous devez utiliser les outils BI tels que l’édition SQL brute, comme les Options avancées -> Instruction SQL dans Power BI.

Les outils BI tels que l’édition SQL brute sont nécessaires pour résoudre les limites de mappages et de tableaux. Consultez le guide sur la façon d’[utiliser les options avancées de Power BI pour saisir une requête SQL personnalisée](../clients/power-bi.md#import-tables-using-custom-sql) dans la section Instruction SQL.

## Étapes suivantes

Ce document explique comment aplatir les structures de données imbriquées pour les utiliser avec des outils BI tiers. Si vous n’avez pas encore connecté votre client, consultez la [présentation de la connexion client](../clients/overview.md) pour obtenir une liste des clients tiers pris en charge.
