---
title: Exemples de requêtes de bloc anonymes
description: 'Le bloc anonyme est une syntaxe SQL prise en charge par Adobe Experience Platform Query Service, qui vous permet d’exécuter efficacement une séquence de requêtes. '
source-git-commit: dffa03d9ab8e26e2c99a359ae000022d6d469572
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Exemples de requêtes pour le bloc Anonymous

Adobe Experience Platform Query Service prend en charge les blocs anonymes. La fonction de bloc anonyme vous permet d’enchaîner une ou plusieurs instructions SQL exécutées en séquence. Ils permettent également de gérer les exceptions.

La fonctionnalité de bloc anonyme est un moyen efficace d’effectuer une séquence d’opérations ou de requêtes. La chaîne de requêtes au sein du bloc peut être enregistrée comme modèle et planifiée pour s&#39;exécuter à un moment ou un intervalle spécifique. Ces requêtes peuvent être utilisées pour écrire et ajouter des données afin de créer un jeu de données. Elles sont généralement utilisées avec une dépendance.

Le tableau ci-dessous présente la répartition des principales sections du bloc : exécution et gestion des exceptions. Les sections sont définies par les mots-clés `BEGIN`, `END` et `EXCEPTION`.

| section | description |
|---|---|
| execution | Une section exécutable commence par le mot-clé `BEGIN` et se termine par le mot-clé `END`. Tout ensemble d’instructions incluses dans les mots-clés `BEGIN` et `END` sera exécuté dans l’ordre et garantit que les requêtes suivantes ne s’exécuteront pas tant que la requête précédente de la séquence n’aura pas été terminée. |
| gestion des exceptions | La section facultative de gestion des exceptions commence par le mot-clé `EXCEPTION`. Il contient le code permettant de capturer et de gérer les exceptions en cas d’échec de l’une des instructions SQL de la section d’exécution. Si l’une des requêtes échoue, le bloc entier est arrêté. |

Il est intéressant de noter qu’un bloc est une instruction exécutable et peut donc être imbriqué dans d’autres blocs.

>[!NOTE]
>
> Il est vivement recommandé de tester vos requêtes sur des jeux de données plus petits et de s’assurer qu’elles fonctionnent comme prévu. Si une requête contient une erreur de syntaxe, l&#39;exception est générée et le bloc entier est abandonné. Une fois que vous avez vérifié l’intégrité des requêtes, vous pouvez commencer à les attacher. Cela garantit que le bloc fonctionne comme prévu avant de le mettre en service.

## Exemples de requêtes bloquées anonymes

La requête suivante illustre un exemple de chaîne d’instructions SQL. Consultez le document [Syntaxe SQL dans Query Service](../sql/syntax.md) pour plus d’informations sur l’une des syntaxes SQL utilisées.

```SQL
$$BEGIN
     
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
     
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
     
END$$;
```

<!-- The block below uses `SET` to persist the result of a select query with a variable. It is used in the anonymous block to store the response from a query as a local variable for use with the `SNAPSHOT` feature. -->

Dans l’exemple ci-dessous, `SET` conserve le résultat d’une requête `SELECT` dans la variable locale spécifiée. La variable est portée sur le bloc anonyme.

L’ID d’instantané est stocké en tant que variable locale (`@current_sid`). Il est ensuite utilisé dans la requête suivante pour renvoyer les résultats en fonction de l’SNAPSHOT du même jeu de données/tableau.

Un instantané de base de données est une vue statique en lecture seule d’une base de données SQL Server. Pour plus d’[informations sur la clause d’instantané](../sql/syntax.md#SNAPSHOT-clause), consultez la documentation sur la syntaxe SQL.

```SQL
$$BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                                     
END$$;
```

## Étapes suivantes

En lisant ce document, vous avez maintenant une compréhension claire des blocs anonymes et de leur structure. [Pour plus d’informations sur l’exécution](./writing-queries.md) des requêtes, consultez le guide sur l’exécution des requêtes dans Query Service.

Pour plus d’exemples de requêtes pouvant être utilisées dans Query Service, consultez les guides sur les [exemples de requêtes Adobe Analytics](./adobe-analytics.md), [exemples de requêtes Adobe Target](./adobe-target.md) ou [exemples de requêtes ExperienceEvent](./experience-event-queries.md).
