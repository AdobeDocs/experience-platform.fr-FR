---
title: Cas d’utilisation de jeux de données dérivés basés sur des déciles
description: Ce guide décrit les étapes requises pour utiliser Query Service afin de créer des jeux de données dérivés basés sur des déciles à utiliser avec vos données de profil.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 2%

---

# Cas d’utilisation de jeux de données dérivés basés sur des déciles

Les jeux de données dérivés facilitent les cas d’utilisation complexes d’analyse des données du lac de données qui peuvent être utilisés avec d’autres services Experience Platform en aval ou publiés dans vos données du profil client en temps réel.

Cet exemple de cas d’utilisation montre comment créer des jeux de données dérivés basés sur des déciles à utiliser avec vos données du profil client en temps réel. En prenant comme exemple un scénario de fidélité à une compagnie aérienne, ce guide vous informe sur la création d’un jeu de données qui utilise des déciles catégoriels pour segmenter et créer des audiences en fonction d’attributs de classement.

Les concepts clés suivants sont illustrés :

* Création de schémas pour le regroupement des déciles.
* Création de déciles catégoriels.
* Création de jeux de données dérivés complexes.
* Calcul des déciles sur une période de recherche en amont.
* Exemple de requête pour démontrer l’agrégation, le classement et l’ajout d’identités uniques afin de permettre la génération d’audiences en fonction de ces intervalles de déciles.

## Commencer

Ce guide nécessite une compréhension pratique de [l’exécution de requêtes dans Query Service](../best-practices/writing-queries.md) et des composants suivants de Adobe Experience Platform :

* [Présentation du profil client en temps réel](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : présentation des schémas XDM ainsi que des blocs de création, principes et bonnes pratiques pour la composition de schémas.
* [Comment activer un schéma pour le profil client en temps réel ](../../profile/tutorials/add-profile-data.md) : ce tutoriel décrit les étapes nécessaires pour ajouter des données au profil client en temps réel.
* [Comment définir un type de données personnalisé ](../../xdm/api/data-types.md) : les types de données sont utilisés comme champs de type référence dans les classes ou les groupes de champs de schéma et permettent l’utilisation cohérente d’une structure à plusieurs champs pouvant être incluse n’importe où dans le schéma.

## Objectifs

L’exemple donné dans ce document utilise des déciles pour créer des jeux de données dérivés afin de classer les données d’un schéma de fidélité de compagnie aérienne. Les jeux de données dérivés vous permettent de maximiser l’utilité de vos données en identifiant une audience en fonction du % supérieur « n » pour une catégorie choisie.

## Créer des jeux de données dérivés basés sur des déciles

Pour définir le classement des déciles en fonction d’une dimension particulière et d’une mesure correspondante, un schéma doit être conçu pour permettre le regroupement des déciles.

Ce guide utilise un jeu de données de fidélité des compagnies aériennes pour démontrer comment utiliser Query Service afin de créer des déciles en fonction des miles parcourus au cours de diverses périodes de recherche en amont.

## Utilisation de Query Service pour créer des déciles

À l’aide de Query Service, vous pouvez créer un jeu de données contenant des déciles catégoriels, qui peuvent ensuite être segmentés pour créer des audiences en fonction du classement des attributs. Les concepts affichés dans les exemples suivants peuvent être appliqués pour créer d’autres jeux de données de compartiments de déciles, à condition qu’une catégorie soit définie et qu’une mesure soit disponible.

L’exemple de données de fidélité à une compagnie aérienne utilise une classe [XDM ExperienceEvents](../../xdm/classes/experienceevent.md). Chaque événement est un enregistrement d’une transaction commerciale pour le kilométrage, crédité ou débité, et le statut de fidélité de l’abonnement est soit « Flyer », « Fréquent », « Argent » ou « Or ». Le champ Identité principale est `membershipNumber`.

### Exemples de jeux de données

Le jeu de données de fidélité initial de la compagnie aérienne pour cet exemple est « Données de fidélité de la compagnie aérienne » et possède le schéma suivant. Notez que l’identité principale du schéma est `_profilefoundationreportingstg.membershipNumber`.

![Diagramme du schéma Données de fidélité des compagnies aériennes.](../images/use-cases/airline-loyalty-data.png)

**Exemples de données**

Le tableau suivant affiche les exemples de données contenus dans l’objet `_profilefoundationreportingstg` utilisé pour cet exemple. Elle fournit un contexte pour l’utilisation des intervalles de déciles pour créer des jeux de données dérivés complexes.

>[!NOTE]
>
>Par souci de concision, l’ID client `_profilefoundationreportingstg` a été omis au début de l’espace de noms dans les titres des colonnes et les mentions suivantes dans tout le document.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | Nouveau membre | 5 000 | FLYER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | ARGENTÉ |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | ARGENTÉ |
| B789279247 | pgalton32n@barnesandnoble.com | 10/02/2022 | AWARD_MILES | FRA-JFK | 5 000 | ARGENTÉ |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Nouvelle carte de crédit | 10000 | FLYER |

{style="table-layout:auto"}

## Générer des jeux de données de déciles

Dans les données de fidélité de la compagnie aérienne présentées ci-dessus, la valeur `.mileage` contient le nombre de miles parcourus par un membre pour chaque vol individuel effectué. Ces données sont utilisées pour créer des déciles pour le nombre de kilomètres parcourus au cours de la durée de vie des recherches en amont et de diverses périodes de recherche en amont. À cet effet, un jeu de données est créé qui contient des déciles dans un type de données de mappage pour chaque période de recherche en amont et un décile approprié pour chaque période de recherche en amont affectée sous `membershipNumber`.

Créez un « Schéma de déciles de fidélité de la compagnie aérienne » pour créer un jeu de données de déciles à l’aide de Query Service.

![Diagramme du « Schéma des déciles de fidélité des compagnies aériennes ».](../images/use-cases/airline-loyalty-decile-schema.png)

### Activer le schéma pour le profil client en temps réel

Les données en cours d’ingestion dans Experience Platform pour être utilisées par le profil client en temps réel doivent être conformes [à un schéma de modèle de données d’expérience (XDM) activé pour Profile](../../xdm/ui/resources/schemas.md). Pour qu’un schéma soit activé pour Profile, il doit implémenter la classe XDM ExperienceEvent ou XDM Individual Profile.

[Activez votre schéma à utiliser dans le profil client en temps réel à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md) ou de l’interface utilisateur [Éditeur de schéma](../../xdm/tutorials/create-schema-ui.md).  Des instructions détaillées sur la manière d’activer un schéma pour Profile sont disponibles dans leur documentation respective.

Créez ensuite un type de données à réutiliser pour tous les groupes de champs liés aux déciles. La création du groupe de champs décile est une étape unique par sandbox. Elle peut également être réutilisée pour tous les schémas liés aux déciles.

### Créer un espace de noms d&#39;identité et le marquer comme identifiant principal {#identity-namespace}

Une identité principale doit être affectée à tout schéma créé pour être utilisé avec des déciles. Vous pouvez [définir un champ d’identité dans l’interface utilisateur des schémas de Adobe Experience Platform](../../xdm/ui/fields/identity.md#define-an-identity-field) ou via l’[API Schema Registry](../../xdm/api/descriptors.md#create).

Query Service vous permet également de définir une identité ou une identité principale pour les champs de jeux de données de schéma ad hoc directement via SQL. Pour plus d’informations, consultez la documentation sur la [définition d’une identité secondaire et d’une identité principale dans les identités de schéma ad hoc](../data-governance/ad-hoc-schema-identities.md).

### Créer une requête pour le calcul des déciles sur une période de recherche en amont {#create-a-query}

L’exemple suivant illustre la requête SQL de calcul d’un décile sur une période de recherche en amont.

Un modèle peut être créé à l’aide du Query Editor dans l’interface utilisateur ou par le biais de l’[API Query Service](../api/query-templates.md#create-a-query-template).

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

### Révision des requêtes

Les sections de l’exemple de requête sont examinées plus en détail ci-dessous.

#### Périodes de recherche en amont

Le type de données décile contient un compartiment pour les recherches en amont de 1, 3, 6, 9, 12 et durée de vie. La requête utilise des périodes de recherche en amont de 1, 3 et 6 mois. Par conséquent, chaque section contient des requêtes « répétées » afin de créer des tables temporaires pour chaque période de recherche en amont.

>[!NOTE]
>
>Si les données sources ne disposent pas d’une colonne pouvant être utilisée pour déterminer une période de recherche en amont, tous les classements de classe de décile sont effectués sous `decileMonthAll`.

#### Agrégation

Utilisez des expressions de table communes (CTE) pour agréger le kilométrage ensemble avant de créer des intervalles de déciles. Cela fournit le nombre total de miles pour une période de recherche en amont spécifique. Les CTE existent temporairement et ne sont utilisables que dans le cadre de la requête plus volumineuse.

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

Les déciles vous permettent d’effectuer un regroupement catégoriel. Pour créer le numéro de classement, la fonction `NTILE` est utilisée avec un paramètre de `10` dans une FENÊTRE regroupée par le champ `loyaltyStatus` . Il en résulte un classement de 1 à 10. Définissez la clause `ORDER BY` de la `WINDOW` sur `DESC` pour vous assurer qu’une valeur de classement de `1` est donnée à la mesure **la plus grande** dans la dimension.

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

Avec plusieurs périodes de recherche en amont, vous devez créer d’avance les mappages de déciles et de compartiments à l’aide des fonctions `MAP_FROM_ARRAYS` et `COLLECT_LIST` . Dans l’exemple de fragment de code, `MAP_FROM_ARRAYS` crée un mappage avec une paire de tableaux de clés (`loyaltyStatus`) et de valeurs (`decileBucket`). `COLLECT_LIST` renvoie un tableau contenant toutes les valeurs de la colonne spécifiée.

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
>L’agrégation des cartes n’est pas nécessaire si le classement par déciles n’est nécessaire que pour une période de vie.

#### Identités uniques

La liste des identités uniques (`membershipNumber`) est nécessaire pour créer une liste unique de tous les abonnements.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Si le classement par déciles n’est nécessaire que pour une période de vie, cette étape peut être omise et l’agrégation par `membershipNumber` peut être effectuée à l’étape finale.

#### Assembler toutes les données temporaires

La dernière étape consiste à rassembler toutes les données temporaires sous une forme identique à la structure des déciles dans le groupe de champs .

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

Si seules des données de durée de vie sont disponibles, votre requête se présente comme suit :

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

Grâce à l’utilisation de déciles, une corrélation entre le numéro de classement et le centile est garantie dans les résultats de la requête. Chaque rang équivaut à 10 %. Par conséquent, l’identification d’une audience en fonction des 30 % supérieurs ne doit cibler que les rangs 1, 2 et 3.

### Exécuter le modèle de requête

Exécutez la requête pour renseigner le jeu de données de décile. Vous pouvez également enregistrer la requête en tant que modèle et planifier son exécution à une cadence donnée. Une fois enregistrée en tant que modèle, la requête peut également être mise à jour afin d’utiliser le modèle de création et d’insertion qui référence la commande `table_exists`. Vous trouverez plus d’informations sur l’utilisation de la commande `table_exists` dans le guide de syntaxe [SQL](../sql/syntax.md#table-exists).

## Étapes suivantes

L’exemple de cas d’utilisation fourni ci-dessus illustre les étapes à suivre pour rendre les jeux de données dérivés basés sur des déciles disponibles dans le profil client en temps réel. Cela permet à Segmentation Service, par le biais d’une interface utilisateur ou d’une API RESTful, de générer des audiences en fonction de ces intervalles de déciles. Consultez la [ présentation de Segmentation Service ](../../segmentation/home.md) pour plus d’informations sur la création, l’évaluation et l’accès aux segments.
