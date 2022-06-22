---
keywords: Experience Platform;service de requête;service de requête;structures de données imbriquées;données imbriquées;aplatir;aplatir les données imbriquées;
title: Aplatissement Des Structures De Données Imbriquées À Utiliser Avec Les Outils BI
description: Ce document explique comment aplatir les schémas XDM pour tous les tableaux et vues au cours d’une session lors de l’utilisation d’outils de BI tiers avec Query Service.
source-git-commit: 3c9a1f552760b34bfb2c4246382fcb2d66e563d0
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 1%

---

# Aplatissement des structures de données imbriquées à utiliser avec des outils de BI tiers

Adobe Experience Platform Query Service prend en charge `FLATTEN` lors de la connexion à une base de données par le biais d’outils de BI tiers. Cette fonctionnalité aplatit les structures de données imbriquées dans les outils de BI tiers afin d’améliorer leur convivialité et de réduire la charge de travail requise pour récupérer, analyser, transformer et générer des rapports sur les données.

De nombreux outils de BI comme [!DNL Tableau] et [!DNL Power BI] ne prennent pas en charge les structures de données imbriquées en mode natif. Le `FLATTEN` supprime la nécessité de créer des vues SQL sur vos données pour fournir une version plate ou d’utiliser Query Service. `CTAS` ou `INSERT INTO` tâches pour dupliquer vos jeux de données en versions aplaties lors de l’utilisation de schémas ad hoc.

Le `FLATTEN` extrait la structure de chaque champ feuille dans la racine de la table et nomme le champ après l’espace de noms d’origine. Vous pouvez ainsi utiliser la notation par points pour faire correspondre un champ à son chemin d’accès XDM (Experience Data Model) tout en préservant le contexte du champ.

## Conditions préalables

En utilisant la variable `FLATTEN` Cette configuration nécessite une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Système XDM](../../xdm/home.md): Présentation générale de XDM et de son implémentation dans Experience Platform.

   * [Création d’un schéma ad hoc](../../xdm/tutorials/ad-hoc.md): Un schéma XDM avec des champs dont l’espace de noms n’est utilisé que par un seul jeu de données est appelé schéma ad hoc. Les schémas ad hoc sont utilisés dans divers workflows d’ingestion de données pour les Experience Platform et pour la création de certains types de connexions source.

* [Environnements de test](../../sandboxes/home.md): Experience Platform fournit des environnements de test virtuels qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

* [Structures de données imbriquées](./nested-data-structures.md): Ce document fournit des exemples de création, de traitement ou de transformation de jeux de données avec des types de données complexes, y compris des structures de données imbriquées.

## Connexion à une base de données à l’aide du paramètre d’effacement {#connect-with-flatten}

Le `FLATTEN` la définition de aplatit les structures de données imbriquées dans des colonnes distinctes où le nom de l’attribut devient le nom de la colonne qui contient les valeurs de ligne. Lorsque vous utilisez des données dans des outils de BI qui ne prennent pas en charge les structures de données imbriquées, ce paramètre améliore la convivialité des schémas ad hoc et réduit la charge de travail nécessaire.

Lorsque vous vous connectez à Query Service avec le client tiers de votre choix, ajoutez le `FLATTEN` sur le nom de la base de données. Pour plus d’informations sur la connexion à un outil de BI spécifique, consultez sa documentation respective dans la section [Présentation de la connexion des clients à Query Service](../clients/overview.md). La chaîne de connexion doit contenir :

* Nom de l’environnement de test.
* Deux-points suivis de `all` ou un identifiant de jeu de données, un identifiant d’affichage ou un nom de base de données spécifique.
* Un point d’interrogation (?) suivie de la fonction `FLATTEN` mot-clé.

L’entrée doit avoir le format suivant :

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Voici un exemple de chaîne de connexion :

```terminal
prod:all?FLATTEN
```

## Exemple {#example}

L’exemple de schéma utilisé dans ce guide utilise le groupe de champs standard. [!UICONTROL Détails du commerce], qui utilise la variable `commerce` la structure de l’objet et `productListItems` tableau. Consultez la documentation XDM pour [en savoir plus sur la [!UICONTROL Détails du commerce] groupe de champs](../../xdm/field-groups/event/commerce-details.md). Une représentation de la structure du schéma est visible dans l’image ci-dessous.

![Schéma du groupe de champs Détails du commerce comprenant le `commerce` et `productListItems` structures.](../images/best-practices/final-subscription-schema.png)

Si votre outil de BI ne prend pas en charge les structures de données imbriquées, il peut être difficile de référencer des champs imbriqués s’ils contiennent des valeurs sérialisées (comme `commerce` et `productListItems` dans l’exemple de schéma). Ces valeurs peuvent apparaître sous la forme de parties d’un seul encodage. `commerce` champ de chaîne et ne sont pas réalisablement inutilisables.

Les valeurs suivantes représentent `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) et `commerce.purchases.value`(1.0) dans les champs imbriqués mal formatés.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

En utilisant la variable `FLATTEN` , vous pouvez accéder à des champs distincts dans votre schéma ou à des sections entières de la structure de données imbriquées à l’aide de la notation par points et de leur nom de chemin d’accès d’origine. Exemple de ce format utilisant le `commerce` Le groupe de champs est donné ci-dessous.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

Le `FLATTEN` présente certaines limites lors de l’utilisation d’autres structures de données. Vous trouverez des détails complets dans la section [section limitations](#limitations).

### Utilisation de guillemets pour les champs dans les requêtes {#quotation-marks}

Les champs racine aplatis utilisent désormais la notation par points pour correspondre à leurs chemins XDM. Lorsqu’ils sont utilisés dans une requête, les champs doivent être placés entre guillemets (&quot; &quot;).

L’exemple SQL ci-dessous affiche l’état d’origine de la requête imbriquée :

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Lors de l’utilisation des champs de données aplaties, la requête est écrite à l’aide de la notation par points et entre guillemets, comme dans l’exemple ci-dessous :

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Limites {#limitations}

Le `FLATTEN` n’aplatit pas actuellement les structures de données suivantes :

| Structure des données | Limite |
|---|---|
| Tableaux | Utilisez un index de tableau explicite pour la variable `EXPLODE` pour accéder aux tableaux. |
| Cartes | Utilisez la clé string pour accéder à une valeur sous une carte pour accéder aux cartes. |

Pour résoudre les limitations à la fois des cartes et des tableaux, vous devez utiliser les outils de BI pour l’édition SQL brute, comme les Options avancées -> Instruction SQL dans Power BI.

Les outils de BI tels que la modification SQL brute sont nécessaires pour résoudre les limitations de mappage et de tableau. Consultez le guide sur la façon de [utiliser des options avancées Power BI pour saisir une requête SQL personnalisée ;](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html#import-tables-using-custom-sql) dans la section Instruction SQL .

## Étapes suivantes

Ce document explique comment aplatir les structures de données imbriquées pour les utiliser avec des outils de BI tiers. Si vous n’avez pas encore connecté votre client, reportez-vous à la section [Présentation de la connexion client](../clients/overview.md) pour obtenir une liste des clients tiers pris en charge.
