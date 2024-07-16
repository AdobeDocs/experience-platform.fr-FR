---
title: Cas d’utilisation des jeux de données dérivés basés sur des déciles
description: Ce guide décrit les étapes requises pour utiliser Query Service afin de créer des jeux de données dérivés basés sur des déciles à utiliser avec vos données Profile.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 2ffb8724b2aca54019820335fb21038ec7e69a7f
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 2%

---

# Cas d’utilisation des jeux de données dérivés basés sur le décile

Les jeux de données dérivés facilitent des cas d’utilisation complexes pour l’analyse de données provenant du lac de données qui peuvent être utilisées avec d’autres services Platform en aval ou publiées dans vos données Real-time Customer Profile.

Cet exemple de cas d’utilisation montre comment créer des jeux de données dérivés basés sur des déciles à utiliser avec vos données Real-time Customer Profile. En prenant l’exemple d’un scénario de fidélité des compagnies aériennes, ce guide vous explique comment créer un jeu de données qui utilise des déciles catégoriques pour segmenter et créer des audiences en fonction d’attributs de classement.

Les concepts clés suivants sont illustrés :

* Création de schémas pour le groupement des déciles.
* Création catégorielle de décile.
* Création de jeux de données dérivés complexes.
* Calcul des déciles sur une période de recherche arrière.
* Exemple de requête pour démontrer l’agrégation, le classement et l’ajout d’identités uniques afin de permettre la génération d’audiences sur la base de ces compartiments déciles.

## Commencer

Ce guide nécessite une compréhension pratique de l’ [exécution de requête dans Query Service](../best-practices/writing-queries.md) et des composants suivants de Adobe Experience Platform :

* [Présentation de Real-Time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : présentation des schémas de modèle de données d’expérience (XDM) et des blocs de création, principes et bonnes pratiques pour la composition de schémas.
* [Comment activer un schéma pour Real-time Customer Profile](../../profile/tutorials/add-profile-data.md) : ce tutoriel décrit les étapes nécessaires pour ajouter des données à Real-Time Customer Profile.
* [Comment définir un type de données personnalisé](../../xdm/api/data-types.md) : les types de données sont utilisés comme champs de type référence dans les classes ou les groupes de champs de schéma et permettent l’utilisation cohérente d’une structure à plusieurs champs qui peut être incluse n’importe où dans le schéma.

## Objectifs

L’exemple donné dans ce document utilise des déciles pour créer des jeux de données dérivés afin de classer les données d’un schéma de fidélité des compagnies aériennes. Les jeux de données dérivés vous permettent de maximiser l’utilité de vos données en identifiant une audience en fonction du n % supérieur pour une catégorie choisie.

## Création de jeux de données dérivés basés sur des déciles

Pour définir le classement des déciles en fonction d’une dimension spécifique et d’une mesure correspondante, un schéma doit être conçu pour permettre le groupement des déciles.

Ce guide utilise un jeu de données de fidélité des compagnies aériennes pour démontrer comment utiliser Query Service pour créer des déciles basés sur les kilomètres parcourus au cours de différentes périodes de recherche arrière.

## Utilisation de Query Service pour créer des décimales

Grâce à Query Service, vous pouvez créer un jeu de données contenant des déciles catégoriels, qui peuvent ensuite être segmentés pour créer des audiences en fonction du classement des attributs. Les concepts affichés dans les exemples suivants peuvent être appliqués pour créer d’autres jeux de données de compartiment à décile, à condition qu’une catégorie soit définie et qu’une mesure soit disponible.

L’exemple de données de fidélité de la compagnie aérienne utilise une [classe XDM ExperienceEvents](../../xdm/classes/experienceevent.md). Chaque événement est un enregistrement d’une transaction commerciale pour le kilométrage, qu’il soit crédité ou débité, et l’état de fidélité de l’appartenance à &quot;flyer&quot;, &quot;Fréquent&quot;, &quot;Argent&quot; ou &quot;Or&quot;. Le champ d’identité principal est `membershipNumber`.

### Exemples de jeux de données

Le jeu de données initial sur la fidélité des compagnies aériennes pour cet exemple est &quot;Données sur la fidélité des compagnies aériennes&quot; et comporte le schéma suivant. Notez que l’identité principale du schéma est `_profilefoundationreportingstg.membershipNumber`.

![Schéma du schéma de données de fidélité des compagnies aériennes.](../images/use-cases/airline-loyalty-data.png)

**Exemple de données**

Le tableau suivant affiche les exemples de données contenus dans l’objet `_profilefoundationreportingstg` utilisé pour cet exemple. Il fournit un contexte pour l’utilisation de compartiments déciles pour créer des jeux de données dérivés complexes.

>[!NOTE]
>
>Pour plus de concision, l’ID de client `_profilefoundationreportingstg` a été omis depuis le début de l’espace de noms dans les titres de colonne et les mentions suivantes dans tout le document.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | Nouveau membre | 5000 | FLYER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | SILVER |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Nouvelle carte de crédit | 10000 | FLYER |

{style="table-layout:auto"}

## Génération de jeux de données de décile

Dans les données de fidélité de la compagnie aérienne vues ci-dessus, la valeur `.mileage` contient le nombre de miles parcourus par un membre pour chaque vol individuel effectué. Ces données sont utilisées pour créer des déciles pour le nombre de kilomètres parcourus pendant la durée de vie des recherches en amont et pendant diverses périodes de recherche en amont. À cette fin, un jeu de données est créé qui contient des déciles dans un type de données map pour chaque période de recherche arrière et un décile approprié pour chaque période de recherche arrière affectée sous `membershipNumber`.

Créez un &quot;schéma de décision de fidélité aérienne&quot; pour créer un jeu de données de décile à l’aide de Query Service.

![ Diagramme du schéma &quot;Airline Loyalty Decile Schema&quot;.](../images/use-cases/airline-loyalty-decile-schema.png)

### Activation du schéma pour Real-time Customer Profile

Les données ingérées dans Experience Platform pour être utilisées par Real-Time Customer Profile doivent être conformes à [un schéma de modèle de données d’expérience (XDM) activé pour Profile](../../xdm/ui/resources/schemas.md). Pour qu’un schéma soit activé pour Profile, il doit implémenter la classe XDM ExperienceEvent ou XDM Individual Profile.

[Activez votre schéma pour l’utiliser dans Real-Time Customer Profile à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md) ou de l’ [ interface utilisateur de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md).  Vous trouverez des instructions détaillées sur l’activation d’un schéma pour Profile dans leur documentation respective.

Créez ensuite un type de données à réutiliser pour tous les groupes de champs liés aux déciles. La création du groupe de champs de décile est une étape unique par environnement de test. Il peut également être réutilisé pour tous les schémas en décile.

### Créer un espace de noms d’identité et le marquer comme identifiant principal {#identity-namespace}

Une identité principale doit être affectée à tout schéma créé pour utilisation avec des déciles. Vous pouvez [définir un champ d’identité dans l’interface utilisateur des schémas Adobe Experience Platform](../../xdm/ui/fields/identity.md#define-an-identity-field) ou via l’ [ API Schema Registry](../../xdm/api/descriptors.md#create).

Query Service vous permet également de définir une identité ou une identité principale pour les champs de jeux de données de schémas ad hoc directement via SQL. Pour plus d’informations, consultez la documentation sur la [définition d’une identité secondaire et d’une identité principale dans les identités de schéma ad hoc](../data-governance/ad-hoc-schema-identities.md) .

### Créer une requête pour calculer les déciles sur une période de recherche arrière {#create-a-query}

L’exemple suivant illustre la requête SQL pour calculer un décile sur une période de recherche arrière.

Un modèle peut être créé à l’aide de Query Editor dans l’interface utilisateur ou via l’ [API Query Service](../api/query-templates.md#create-a-query-template).

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

Le bloc est répété deux fois dans le modèle (`summed_miles_3` et `summed_miles_6`) avec une modification du calcul de date afin de générer les données pour les autres périodes de recherche en amont.

Il est important de noter les colonnes d’identité, de dimension et de mesure pour la requête (`membershipNumber`, `loyaltyStatus` et `totalMiles` respectivement).

#### Classement

Les déciles vous permettent d’effectuer un regroupement catégorique. Pour créer le numéro de classement, la fonction `NTILE` est utilisée avec un paramètre `10` dans une FENÊTRE regroupée par le champ `loyaltyStatus` . Cela donne un classement de 1 à 10. Définissez la clause `ORDER BY` de `WINDOW` sur `DESC` pour vous assurer qu’une valeur de classement de `1` est donnée à la mesure **plus** dans la dimension.

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

Avec plusieurs périodes de recherche arrière, vous devez créer au préalable les zones de compartiment à décile à l’aide des fonctions `MAP_FROM_ARRAYS` et `COLLECT_LIST`. Dans l’exemple de fragment de code, `MAP_FROM_ARRAYS` crée une carte avec une paire de clés (`loyaltyStatus`) et des tableaux de valeurs (`decileBucket`). `COLLECT_LIST` renvoie un tableau avec toutes les valeurs de la colonne spécifiée.

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

La liste des identités uniques (`membershipNumber`) est requise pour créer une liste unique de tous les membres.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Si le classement des déciles n’est requis que pour une durée de vie, cette étape peut être omise et l’agrégation par `membershipNumber` peut être effectuée à l’étape finale.

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

Exécutez la requête pour renseigner le jeu de données de décile. Vous pouvez également enregistrer la requête en tant que modèle et la planifier pour qu’elle s’exécute à un rythme. Lors de l’enregistrement en tant que modèle, la requête peut également être mise à jour afin d’utiliser le modèle de création et d’insertion qui fait référence à la commande `table_exists`. Vous trouverez plus d’informations sur l’utilisation de la commande `table_exists`dans le [guide de syntaxe SQL](../sql/syntax.md#table-exists).

## Étapes suivantes

L’exemple de cas d’utilisation fourni ci-dessus met en évidence les étapes permettant de rendre des jeux de données dérivés de déciles disponibles dans Real-time Customer Profile. Cela permet à Segmentation Service, soit par le biais d’une interface utilisateur, soit via une API RESTful, de générer des audiences en fonction de ces compartiments déciles. Pour plus d’informations sur la création, l’évaluation et l’accès aux segments, consultez la [présentation de Segmentation Service](../../segmentation/home.md) .
