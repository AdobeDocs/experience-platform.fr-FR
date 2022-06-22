---
title: Attributs dérivés
description: Les attributs dérivés vous permettent de calculer des attributs à un rythme normal et éventuellement de publier ces attributs dérivés dans Real-time Customer Profile en tant qu’attributs de profil. Ce document présente l’utilisation de Query Service pour créer des attributs dérivés à utiliser avec vos données de profil.
hide: true
hidefromtoc: true
source-git-commit: fc2d2e7dadb95460f5d735ba33e5f106880a0198
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 7%

---

# Attributs dérivés

Les attributs dérivés vous permettent de calculer des attributs à un rythme normal et éventuellement de publier ces attributs dérivés dans Real-time Customer Profile en tant qu’attributs de profil.

Les attributs dérivés, tels que ceux créés avec des données de décile, sont nécessaires pour divers cas d’utilisation qui analysent les données de profil. En utilisant des données déciles, vous pouvez créer des audiences à partir de segments en fonction de leur percentile ou du classement d’un attribut donné. Par exemple, les cas d’utilisation potentiels peuvent inclure :

* Identification des 10 % d’abonnés les plus bas en fonction de l’audience par canal. Cela permet aux marketeurs de cibler une audience particulière et de vendre un nouveau module d’abonné.
* Identification d’une audience qui se trouve dans le top 10 % des tracts en fonction de leur nombre total de kilomètres parcourus et dont le statut est &quot;prospectus&quot; Cette audience peut être utilisée pour cibler de manière sélective la vente d’une nouvelle offre de carte de crédit.

## Prise en main

Cette présentation nécessite une compréhension pratique de [Appels API Platform](../landing/api-guide.md) et les composants suivants de Adobe Experience Platform :

* [Présentation de Real-time Customer Profile](../profile/home.md): Fournit un profil client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [Principes de base de la composition des schémas](../xdm/schema/composition.md): Cette section présente les schémas de modèle de données d’expérience (XDM) et les blocs de création, les principes et les bonnes pratiques pour la composition de schémas.
* [Comment activer un schéma pour Real-time Customer Profile](../profile/tutorials/add-profile-data.md): Ce tutoriel décrit les étapes nécessaires à l’ajout de données à Real-time Customer Profile.

## Prise en charge SQL des attributs dérivés

Pour définir le classement des déciles en fonction d’une dimension particulière (catégorie) et d’une mesure correspondante (recettes, points, durée de visionnage, etc.), un schéma doit être conçu pour permettre le groupement des déciles. Ce schéma peut être utilisé dans le cadre du schéma de profil plus vaste.

### Création d’un espace de noms d’identité pour le schéma de profil {#identity-namespace}

Les espaces de noms d’identité sont des composants d’[Identity Service](../identity-service/home.md) qui servent d’indicateurs du contexte auquel une identité se rapporte. Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms. Lors de la correspondance et de la fusion des données d’enregistrement entre les fragments de profil, la valeur d’identité et l’espace de noms doivent correspondre.

Les jeux de données créés en rapport avec l’identité peuvent être regroupés en tant que groupe de données et contribuer à maintenir le cycle de vie des données. Les espaces de noms personnalisés peuvent être créés à l’aide de la variable [API Identity Service](../identity-service/api/create-custom-namespace.md) ou via l’interface utilisateur. Voir [gestion de la documentation sur les espaces de noms personnalisés](../identity-service/namespaces.md#manage-namespaces) pour obtenir des conseils sur la manière de procéder via l’interface utilisateur.

Le descripteur d’identité Principal peut être affecté à un champ de l’interface utilisateur des schémas ou peut être créé à l’aide de l’API Schema Registry. Consultez la documentation pour obtenir des instructions sur la manière de [définition d’un champ d’identité dans l’interface utilisateur de Adobe Experience Platform](../xdm/ui/fields/identity.md#define-an-identity-field)ou au moyen de la fonction [API Schema Registry](../xdm/api/descriptors.md#create).

Query Service vous permet également de définir une identité ou une identité Principale pour les champs de jeu de données de schémas ad hoc directement via SQL. Consultez la documentation relative à [définition d’une identité secondaire et d’une identité Principale dans les identités de schéma ad hoc](./data-governance/ad-hoc-schema-identities.md) pour plus d’informations.

## Création d’attributs dérivés

L’exemple de requête fourni dans ce document se concentre sur les déciles de catégorisation des jeux de données volumineux, de classement des données des valeurs les plus élevées aux valeurs les plus basses (ou vice versa), et de filtrage basé sur une période donnée.

### Déciles {#deciles}

Un décile est une méthode permettant de diviser un ensemble de données classées en 10 parties égales. Lorsque les données sont divisées en déciles, un rang de décile est attribué à chaque ligne de l’ensemble de données. Cela permet de trier les données par ordre croissant ou décroissant.

Un classement en déciles classe les données dans l’ordre du plus petit au plus élevé, sur une échelle de 1 à 10 où chaque nombre successif correspond à une augmentation de 10 points de pourcentage.

Les intervalles par déciles représentent le nombre de groupes classés et sont utilisés pour affecter un classement à une dimension (catégorie) dans le jeu de données. Le compartiment peut être un nombre ou une expression qui évalue à une valeur entière positive pour chaque partition. Les compartiments ne doivent pas avoir de valeur nulle.

Les quartile sont utilisés pour diviser la distribution par quatre et les centiles par 100.

### Création du schéma pour les compartiments déciles {#create-schema}

Le schéma créé pour les compartiments à décile comporte trois parties intégrales : un type de données, un groupe de champs pour le type de données (par jeu de données source) et un champ d’identité Principal.

>[!NOTE]
>
>Un espace de noms d’identité doit être créé avant la création du schéma. Voir [namespace d’identité](#identity-namespace) pour plus d’informations.

Adobe fournit plusieurs classes XDM standard (&quot;core&quot;), y compris XDM Individual Profile et XDM ExperienceEvent. Outre ces classes principales, vous pouvez créer vos propres classes personnalisées afin de décrire des cas d’utilisation plus spécifiques à votre organisation. Reportez-vous aux guides sur la manière de [création et modification de schémas dans l’interface utilisateur](../xdm/ui/resources/schemas.md#create) ou en utilisant la variable [point de terminaison des schémas dans l’API Schema Registry](../xdm/api/schemas.md#create) pour plus d’informations.

Les données en cours d’ingestion dans Experience Platform pour être utilisées par Real-time Customer Profile doivent être conformes à un schéma du modèle de données d’expérience (XDM) activé pour Profile. Pour qu’un schéma soit activé pour Profile, il doit implémenter la classe XDM ExperienceEvent ou XDM Individual Profile.

Vous pouvez [Activation d’un schéma à utiliser dans Real-time Customer Profile à l’aide de l’API Schema Registry](../xdm/tutorials/create-schema-api.md) ou le [Interface utilisateur de l’éditeur de schémas](../xdm/tutorials/create-schema-ui.md).  Vous trouverez des instructions détaillées sur l’activation d’un schéma pour Profile dans leur documentation respective.

### Création d’un type de données {#create-data-type}

Les types de données sont utilisés comme champs de type référence dans des classes ou des groupes de champs de schéma et permettent l’utilisation cohérente d’une structure à plusieurs champs qui peut être incluse n’importe où dans le schéma. La création du type de données est une étape unique par environnement de test, car elle peut être réutilisée pour tous les groupes de champs associés aux déciles.

Consultez la documentation pour obtenir des instructions sur la manière de [définir un type de données personnalisé ;](../xdm/api/data-types.md) en utilisant la variable [API Schema Registry](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

### Créer un groupe de champs de décile {#create-field-group}

La création du groupe de champs est une étape unique par environnement de test. Il peut également être réutilisé pour tous les schémas en décile.

Consultez la documentation pour obtenir des instructions sur la manière de [création de groupes de champs via l’interface utilisateur](../xdm/ui/resources/field-groups.md#create)

## Utilisation de Query Service pour créer des décimales

Query Service offre un moyen idéal de créer un jeu de données contenant des déciles catégoriques. Vous pouvez ensuite l’utiliser conjointement avec Segmentation Service pour créer des audiences basées sur le classement des attributs.

Les concepts affichés dans les exemples suivants peuvent être appliqués pour créer d’autres jeux de données de compartiment à décile, à condition qu’une catégorie (dimension) soit définie et qu’une mesure soit disponible. Les exemples sont basés sur les données d’un schéma de fidélité des compagnies aériennes. Les données de fidélité de la compagnie aérienne utilisent la classe Experience Events où chaque événement est un enregistrement d’une transaction commerciale pour **kilométrage**, crédité ou débit, et appartenance **état de fidélité** &quot;flyer&quot;, &quot;Fréquent&quot;, &quot;Argent&quot; ou &quot;Or&quot;. Le champ d’identité Principal est : `membershipNumber`.

### Création d’un modèle de requête {#create-a-query-template}

Le modèle peut être créé à l’aide de l’éditeur de requêtes de l’interface utilisateur ou au moyen de la fonction [API Query Service](./api/query-templates.md#create-a-query-template).

Les sections du modèle de requête affichées ci-dessous seront examinées plus en détail.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
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
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### Périodes de recherche arrière

Le type de données &quot;décile&quot; contient un compartiment pour les recherches en amont 1, 3, 6, 9, 12 et de durée de vie. La requête utilise des périodes d’analyse de 1, 3 et 6 mois. Chaque section contiendra donc des requêtes &quot;répétées&quot; afin de créer des tableaux temporaires pour chaque période d’analyse.

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

Le bloc est répété deux fois dans le modèle (`summed_miles_3` et `summed_miles_6`) avec un changement dans le calcul de date afin de générer les données des autres périodes d’analyse.

Notez les colonnes Identité, Dimension et Mesure de la requête (`membershipNumber`, `loyaltyStatus` et `totalMiles` ).

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

Avec plusieurs périodes d’analyse, vous devez créer au préalable les feuilles de calcul du compartiment à décile à l’aide de la variable `MAP_FROM_ARRAYS` et `COLLECT_LIST` fonctions. Dans l’exemple de fragment de code, `MAP_FROM_ARRAYS` crée une carte avec une paire de clés (`loyaltyStatus`) et les valeurs (`decileBucket`). `COLLECT_LIST` renvoie un tableau contenant toutes les valeurs de la colonne spécifiée.

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

### Exécuter le modèle de requête

Les requêtes peuvent être [exécutées via l’interface utilisateur](./ui/user-guide.md#executing-queries) ou le [API Query Service](./api/queries.md#create-a-query).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

Une corrélation entre le numéro de classement et le centile est garantie dans les résultats de la requête en raison de l’utilisation de déciles. Chaque rang est égal à 10 %. Dès lors, l’identification d’une audience basée sur les 30 % supérieurs doit uniquement cibler les 1, 2 et 3.

## Étapes suivantes

Segmentation Service fournit une interface utilisateur et une API RESTful qui vous permettent de générer des audiences basées sur ces compartiments déciles. Voir [Présentation de Segmentation Service](../segmentation/home.md) pour plus d’informations sur la création, l’évaluation et l’accès aux segments.

Pour plus d’informations sur la création et l’utilisation de segments dans le créateur de segments (l’implémentation de l’interface utilisateur de Segmentation Service), voir [Guide du créateur de segments](../segmentation/ui/overview.md).

Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, consultez le tutoriel sur la [création de segments ciblés à l’aide de l’API](../segmentation/tutorials/create-a-segment.md).
