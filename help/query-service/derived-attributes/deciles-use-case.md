---
title: Cas d’utilisation des attributs dérivés basés sur des déciles
description: Ce guide décrit les étapes requises pour utiliser Query Service afin de créer des attributs dérivés basés sur des déciles à utiliser avec vos données de profil.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: c1ec6f949bd0ab9ec3b1ccc58baf74d8c71deca0
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 3%

---

# Cas d’utilisation des attributs dérivés basés sur un décile

Les attributs dérivés facilitent les cas d’utilisation complexes pour l’analyse de données du lac de données qui peuvent être utilisées avec d’autres services Platform en aval ou publiées dans vos données Real-time Customer Profile.

Cet exemple de cas d’utilisation montre comment créer des attributs dérivés basés sur des déciles à utiliser avec vos données Real-time Customer Profile. En prenant l’exemple d’un scénario de fidélité des compagnies aériennes, ce guide vous explique comment créer un jeu de données qui utilise des déciles catégoriques pour segmenter et créer des audiences en fonction d’attributs de classement.

Les concepts clés suivants sont illustrés :

* Création de schémas pour le groupement des déciles.
* Création catégorielle de décile.
* Création d’attributs dérivés complexes.
* Calcul des déciles sur une période de recherche arrière.
* Exemple de requête pour démontrer l’agrégation, le classement et l’ajout d’identités uniques afin de permettre la génération d’audiences sur la base de ces compartiments déciles.

## Prise en main

Ce guide nécessite une compréhension pratique de [exécution de requête dans Query Service](../best-practices/writing-queries.md) et les composants suivants de Adobe Experience Platform :

* [Présentation de Real-time Customer Profile](../../profile/home.md): Fournit un profil client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [Principes de base de la composition des schémas](../../xdm/schema/composition.md): Cette section présente les schémas de modèle de données d’expérience (XDM) et les blocs de création, les principes et les bonnes pratiques pour la composition de schémas.
* [Comment activer un schéma pour Real-time Customer Profile](../../profile/tutorials/add-profile-data.md): Ce tutoriel décrit les étapes nécessaires à l’ajout de données à Real-time Customer Profile.
* [Définition d’un type de données personnalisé](../../xdm/api/data-types.md): Les types de données sont utilisés comme champs de type référence dans des classes ou des groupes de champs de schéma et permettent l’utilisation cohérente d’une structure à plusieurs champs qui peut être incluse n’importe où dans le schéma.

## Objectifs

L’exemple donné dans ce document utilise des déciles pour créer des attributs dérivés pour classer les données d’un schéma de fidélité des compagnies aériennes. Les attributs dérivés permettent d’optimiser l’utilité de vos données en identifiant une audience en fonction du n % supérieur pour une catégorie choisie.

## Création d’attributs dérivés basés sur des déciles

Pour définir le classement des déciles en fonction d’une dimension spécifique et d’une mesure correspondante, un schéma doit être conçu pour permettre le groupement des déciles.

Ce guide utilise un jeu de données de fidélité des compagnies aériennes pour démontrer comment utiliser Query Service pour créer des déciles basés sur les kilomètres parcourus au cours de différentes périodes de recherche arrière.

## Utilisation de Query Service pour créer des décimales

Grâce à Query Service, vous pouvez créer un jeu de données contenant des déciles catégoriels, qui peuvent ensuite être segmentés pour créer des audiences en fonction du classement des attributs. Les concepts affichés dans les exemples suivants peuvent être appliqués pour créer d’autres jeux de données de compartiment à décile, à condition qu’une catégorie soit définie et qu’une mesure soit disponible.

L’exemple de données sur la fidélité des compagnies aériennes utilise une variable [Classe XDM ExperienceEvents](../../xdm/classes/experienceevent.md). Chaque événement est un enregistrement d’une transaction commerciale pour le kilométrage, qu’il soit crédité ou débité, et l’état de fidélité de l’appartenance à &quot;flyer&quot;, &quot;Fréquent&quot;, &quot;Argent&quot; ou &quot;Or&quot;. Le champ d’identité Principal est : `membershipNumber`.

### Exemples de jeux de données

Le jeu de données initial sur la fidélité des compagnies aériennes pour cet exemple est &quot;Données sur la fidélité des compagnies aériennes&quot; et comporte le schéma suivant. Notez que l’identité Principale du schéma est `_profilefoundationreportingstg.membershipNumber`.

![Schéma des données de fidélité des compagnies aériennes.](../images/derived-attributes/deciles-use-case/airline-loyalty-data.png)

**Données d’exemple**

Le tableau suivant affiche les exemples de données contenus dans la variable `_profilefoundationreportingstg` utilisé pour cet exemple. Il fournit un contexte pour l’utilisation de compartiments déciles pour créer des attributs dérivés complexes.

>[!NOTE]
>
>Pour plus de concision, l’identifiant du client `_profilefoundationreportingstg` a été omis au début de l’espace de noms dans les titres des colonnes et les mentions suivantes dans tout le document.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | Nouveau membre | 5 000 | FLYER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5 000 | SILVER |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Nouvelle carte de crédit | 10000 | FLYER |

{style=&quot;table-layout:auto&quot;}

## Génération de jeux de données de décile

Dans les données de fidélité de la compagnie aérienne vues ci-dessus, la variable `.mileage` contient le nombre de milles parcourus par un membre pour chaque vol effectué. Ces données sont utilisées pour créer des déciles pour le nombre de kilomètres parcourus pendant la durée de vie des recherches en amont et pendant diverses périodes de recherche en amont. À cette fin, un jeu de données est créé qui contient des déciles dans un type de données map pour chaque période de recherche arrière et un décile approprié pour chaque période de recherche arrière affectée sous `membershipNumber`.

Créez un &quot;schéma de décision de fidélité aérienne&quot; pour créer un jeu de données de décile à l’aide de Query Service.

![Schéma du &quot;Schéma Loyalty Decile&quot; de la compagnie aérienne.](../images/derived-attributes/deciles-use-case/airline-loyalty-decile-schema.png)

### Activation du schéma pour Real-time Customer Profile

Les données ingérées dans Experience Platform pour être utilisées par Real-time Customer Profile doivent être conformes à [un schéma de modèle de données d’expérience (XDM) activé pour Profile ;](../../xdm/ui/resources/schemas.md). Pour qu’un schéma soit activé pour Profile, il doit implémenter la classe XDM ExperienceEvent ou XDM Individual Profile.

[Activation de votre schéma pour une utilisation dans Real-time Customer Profile à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md) ou le [Interface utilisateur de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md).  Vous trouverez des instructions détaillées sur l’activation d’un schéma pour Profile dans leur documentation respective.

Créez ensuite un type de données à réutiliser pour tous les groupes de champs liés aux déciles. La création du groupe de champs de décile est une étape unique par environnement de test. Il peut également être réutilisé pour tous les schémas en décile.

### Créer un espace de noms d’identité et le marquer comme identifiant Principal {#identity-namespace}

Une identité Principale doit être affectée à tout schéma créé pour être utilisé avec des déciles. Vous pouvez [définition d’un champ d’identité dans l’interface utilisateur des schémas Adobe Experience Platform](../../xdm/ui/fields/identity.md#define-an-identity-field)ou au moyen de la fonction [API Schema Registry](../../xdm/api/descriptors.md#create).

Query Service vous permet également de définir une identité ou une identité Principale pour les champs de jeu de données de schémas ad hoc directement via SQL. Consultez la documentation relative à [définition d’une identité secondaire et d’une identité Principale dans les identités de schéma ad hoc](../data-governance/ad-hoc-schema-identities.md) pour plus d’informations.

### Créer une requête pour calculer les déciles sur une période de recherche arrière {#create-a-query}

L’exemple suivant illustre la requête SQL pour calculer un décile sur une période de recherche arrière.

Un modèle peut être créé à l’aide de l’éditeur de requêtes dans l’interface utilisateur ou via la fonction [API Query Service](../api/query-templates.md#create-a-query-template).

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### Examen des requêtes

Les sections de l&#39;exemple de requête sont examinées plus en détail ci-dessous.

#### Périodes de recherche en amont

Le type de données &quot;décile&quot; contient un compartiment pour les recherches en amont 1, 3, 6, 9, 12 et de durée de vie. La requête utilise des périodes de recherche arrière de 1, 3 et 6 mois, de sorte que chaque section contiendra des requêtes &quot;répétées&quot; afin de créer des tableaux temporaires pour chaque période de recherche arrière.

>[!NOTE]
>
>Si les données source ne comportent pas de colonne pouvant être utilisée pour déterminer une période de recherche arrière, tous les classements de classe de décile seront effectués sous `decileMonthAll`.

#### Agrégation

Utilisez des expressions de tableau courantes (CTE) pour agréger le kilométrage avant de créer des compartiments à déciles. Cela fournit le nombre total de kilomètres pour une période de recherche arrière spécifique. Les CTE existent temporairement et ne sont utilisables que dans le cadre de la requête plus volumineuse.

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

Le bloc est répété deux fois dans le modèle (`summed_miles_3` et `summed_miles_6`) avec un changement dans le calcul de date afin de générer les données des autres périodes de recherche en amont.

Il est important de noter les colonnes d’identité, de dimension et de mesure pour la requête (`membershipNumber`, `loyaltyStatus` et `totalMiles` ).

#### Classement

Les déciles vous permettent d’effectuer un regroupement catégorique. Pour créer le numéro de classement, le `NTILE` est utilisée avec un paramètre de `10` dans une FENÊTRE regroupée par `loyaltyStatus` champ . Cela donne un classement de 1 à 10. Définissez la variable `ORDER BY` de la clause `WINDOW` to `DESC` pour garantir que la valeur de classement de `1` est donné à la variable **most** dans la dimension.

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### Agrégation des cartes

Avec plusieurs périodes de recherche arrière, vous devez créer au préalable les feuilles de calcul du compartiment à décile à l’aide de la variable `MAP_FROM_ARRAYS` et `COLLECT_LIST` fonctions. Dans l’exemple de fragment de code, `MAP_FROM_ARRAYS` crée une carte avec une paire de clés (`loyaltyStatus`) et les valeurs (`decileBucket`). `COLLECT_LIST` renvoie un tableau contenant toutes les valeurs de la colonne spécifiée.

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>L’agrégation des cartes n’est pas nécessaire si le classement des déciles n’est nécessaire que pour une durée de vie.

#### Identités uniques

La liste des identités uniques (`membershipNumber`) est requis pour créer une liste unique de tous les membres.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Si le classement des déciles n’est requis que pour une durée de vie, cette étape peut être omise et être agrégation par `membershipNumber` peut être effectué à l’étape finale.

#### Assemblage de toutes les données temporaires

La dernière étape consiste à regrouper toutes les données temporaires dans un formulaire identique à la structure des déciles du groupe de champs.

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

Si seules les données de durée de vie sont disponibles, votre requête se présente comme suit :

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

Une corrélation entre le numéro de classement et le centile est garantie dans les résultats de la requête en raison de l’utilisation de déciles. Chaque rang est égal à 10 %. Dès lors, l’identification d’une audience basée sur les 30 % supérieurs doit uniquement cibler les 1, 2 et 3.

### Exécuter le modèle de requête

Exécutez la requête pour renseigner le jeu de données de décile. Vous pouvez également enregistrer la requête en tant que modèle et la planifier pour qu’elle s’exécute à un rythme. Lors de l’enregistrement en tant que modèle, la requête peut également être mise à jour afin d’utiliser le modèle de création et d’insertion qui fait référence au modèle `table_exists` . Plus d’informations sur l’utilisation de la variable `table_exists`se trouve dans la fonction [Guide de syntaxe SQL](../sql/syntax.md#table-exists).

## Étapes suivantes

L’exemple de cas d’utilisation fourni ci-dessus met en évidence les étapes à suivre pour rendre les attributs de décile disponibles dans Real-time Customer Profile. Cela permet à Segmentation Service, soit par le biais d’une interface utilisateur, soit via une API RESTful, de générer des audiences en fonction de ces compartiments déciles. Voir [Présentation de Segmentation Service](../../segmentation/home.md) pour plus d’informations sur la création, l’évaluation et l’accès aux segments.
