---
keywords: Experience Platform;service de requête;service de requête;structures de données imbriquées;données imbriquées;
title: Utilisation de structures de données imbriquées dans Query Service
description: Ce document fournit un exemple de travail pour le traitement et la transformation des champs de données imbriqués à l’aide des instructions CTAS et INSERT INTO .
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: b2b292dba0cf9ab9adbdff26aa61ef5a2cd5fe86
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 2%

---

# Utilisation de structures de données imbriquées dans Query Service

Adobe Experience Platform Query Service prend en charge l’utilisation de champs de données imbriqués. La complexité des structures de données d’entreprise peut rendre la transformation ou le traitement de ces données compliqué. Ce document fournit des exemples de création, de traitement ou de transformation de jeux de données avec des types de données complexes, y compris des structures de données imbriquées.

Query Service fournit une interface PostgreSQL permettant d’exécuter des requêtes SQL sur tous les jeux de données gérés par Experience Platform. Platform prend en charge l’utilisation de types de données primitifs ou complexes dans les colonnes de tableau comme struct, les tableaux, les cartes et les structs, les tableaux et les mappages profondément imbriqués. Les jeux de données peuvent également contenir des structures imbriquées dans lesquelles le type de données de colonne peut être aussi complexe qu’un tableau de structures imbriquées, ou une carte de mappages dans laquelle la valeur d’une paire clé-valeur peut être une structure avec plusieurs niveaux d’imbrication.

## Prise en main

Ce tutoriel nécessite l’utilisation d’un client PSQL tiers ou de l’outil Query Editor pour écrire, valider et exécuter des requêtes dans l’interface utilisateur de l’Experience Platform. Vous trouverez des informations complètes sur l’exécution des requêtes via l’interface utilisateur dans la section [Guide de l’interface utilisateur de Query Editor](../ui/user-guide.md). Pour obtenir une liste détaillée des clients de bureau tiers qui peuvent se connecter à Query Service, reportez-vous à la section [présentation des connexions client](../clients/overview.md).

Vous devriez également avoir une bonne compréhension de la variable `INSERT INTO` et `CTAS` syntaxe. Vous trouverez des informations spécifiques sur leur utilisation dans la section [`INSERT INTO`](../sql/syntax.md#insert-into) et [`CTAS`](../sql/syntax.md#create-table-as-select) des sections [Documentation de référence sur la syntaxe SQL](../sql/syntax.md).

## Création d’un jeu de données

Query Service fournit la méthode Create Table As Select (`CTAS`) pour créer un tableau en fonction de la sortie d’un `SELECT` , ou comme dans ce cas, en utilisant une référence à un schéma XDM existant dans Adobe Experience Platform. Le schéma XDM affiché ci-dessous pour `Final_subscription` créé pour cet exemple.

![Schéma du schéma final_subscription.](../images/best-practices/final-subscription-schema.png)

L’exemple suivant illustre le langage SQL utilisé pour créer la variable `final_subscription_test2` jeu de données. `final_subscription_test2` est créé à l’aide de la fonction `Final_subscription` schéma. Les données sont extraites de la source à l’aide d’un `SELECT` pour renseigner certaines lignes.

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

Dans le jeu de données initial `final_subscription_test2`, le type de données struct est utilisé pour contenir à la fois la variable `subscription` et le champ `userid` qui est propre à chaque utilisateur. Le `subscription` décrit les abonnements aux produits pour un utilisateur. Il peut y avoir plusieurs abonnements, mais un tableau ne peut contenir que les informations d’un abonnement par ligne.

## Utilisez INSERT INTO pour mettre à jour les champs de données imbriqués

Après la `final_subscription_test2` le jeu de données a été créé, le `INSERT INTO` sert à ajouter des données supplémentaires au tableau. Lors de la copie de données, les types de données dans la source et la cible doivent correspondre. Sinon, le type de données source doit être `CAST` au type de données cible. Les données incrémentielles sont ensuite ajoutées au jeu de données cible à l’aide du code SQL suivant.

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## Traitement des données d’un jeu de données imbriqué

Pour trouver la liste des principaux abonnements d’un utilisateur à partir d’un jeu de données, vous devez écrire une requête qui sépare les éléments d’un tableau en plusieurs lignes et colonnes. Pour ce faire, vous devez d’abord comprendre la forme du modèle de données, car les informations d’abonnement sont conservées dans un tableau imbriqué dans le jeu de données.

PSQL `\d` est utilisée pour naviguer niveau par niveau vers les données d’abonnement requises. Les tableaux illustrent la structure de la variable `final_subscription_test2` jeu de données. Les types de données complexes peuvent être reconnus en un coup d’oeil, car il ne s’agit pas de valeurs de type standard telles que le texte, le booléen, l’horodatage, etc.

| Colonne | Type |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

Les champs de la colonne suivante sont affichés à l’aide de la variable `\d final_subscription_test2__lumaservices3` .

| Colonne | Type |
|---------|-------|
| `userid` | text |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` est un tableau d’éléments struct. Ses champs s’affichent à l’aide de la propriété `\d _lumaservices3_subscription_e[]` .

| Colonne | Type |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | text |
| `offer_id` | text |
| `subscription_id` | text |

Pour interroger les champs imbriqués de l’abonnement, vous devez d’abord séparer les éléments de la variable `subscription` tableau en plusieurs lignes et renvoyez les résultats à l’aide de la fonction explode . L’exemple SQL suivant renvoie l’abonnement principal d’un utilisateur en fonction de `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

Cet exemple simplifié de solution ne permet qu’un abonnement principal à un utilisateur. En réalité, il peut y avoir de nombreux abonnements principaux pour un seul utilisateur. L&#39;exemple suivant modifie la requête précédente pour permettre plusieurs abonnements principaux simultanés.

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

Malgré la complexité croissante de cet exemple SQL, la variable `collect_list` pour les abonnements principaux, ne garantit pas que la sortie sera dans le même ordre que la source. Pour créer une liste d&#39;abonnements principaux pour un utilisateur, vous devez utiliser le regroupement GROUP BY ou le regroupement des résultats de la liste.

## Étapes suivantes

En lisant ce document, vous comprenez désormais comment traiter ou transformer des jeux de données qui utilisent des types de données complexes dans Adobe Experience Platform Query Service. Veuillez consulter la [guide d’exécution des requêtes](./writing-queries.md) pour plus d’informations sur l’exécution de requêtes SQL sur des jeux de données dans le lac de données.
