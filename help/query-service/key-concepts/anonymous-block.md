---
title: Bloc anonyme dans Query Service
description: Le bloc anonyme est une syntaxe SQL prise en charge par Adobe Experience Platform Query Service, qui permet d’exécuter efficacement une séquence de requêtes.
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 65eeeb1df1d512c4cd6c67892905a63cc1cc4fc5
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 69%

---

# Bloc anonyme dans Query Service

Adobe Experience Platform Query Service prend en charge les blocs anonymes. La fonction de bloc anonyme vous permet d’enchaîner une ou plusieurs instructions SQL exécutées de manière séquentielle. Les blocs anonymes permettent également de gérer les exceptions.

La fonction de bloc anonyme est un moyen efficace d’effectuer une séquence d’opérations ou de requêtes. La chaîne de requêtes au sein du bloc peut être enregistrée comme modèle et planifiée pour s’exécuter à un moment ou à un intervalle spécifique. Ces requêtes peuvent être utilisées pour écrire et ajouter des données afin de créer un jeu de données. Elles sont généralement utilisées avec une dépendance.

Le tableau ci-dessous présente la répartition des principales sections du bloc : exécution et gestion des exceptions. Les sections sont définies par les mots-clés `BEGIN`, `END` et `EXCEPTION`.

| section | description |
|---|---|
| exécution | Une section exécutable commence par le mot-clé `BEGIN` et se termine par le mot-clé `END`. Tout ensemble d’instructions inclus dans les mots-clés `BEGIN` et `END` est exécuté dans l’ordre et garantit que les requêtes suivantes ne s’exécutent pas tant que la requête précédente n’est pas terminée. |
| gestion des exceptions | La section facultative de gestion des exceptions commence par le mot-clé `EXCEPTION`. Il contient le code permettant de capturer et de gérer les exceptions en cas d’échec de l’une des instructions SQL de la section d’exécution. Si l’une des requêtes échoue, le bloc entier est arrêté. |

Il est intéressant de noter qu’un bloc est une instruction exécutable et peut donc être imbriqué dans d’autres blocs.

>[!NOTE]
>
> Il est vivement recommandé de tester vos requêtes sur des jeux de données plus petits et de s’assurer qu’elles fonctionnent comme prévu. Si une requête contient une erreur de syntaxe, cela entraîne la génération de l’exception et l’arrêt du boc entier. Une fois que vous avez vérifié l’intégrité des requêtes, vous pouvez commencer à les lier. Cela garantit que le bloc fonctionne comme prévu avant de le mettre en service.

## Exemples de requêtes en blocs anonymes

La requête suivante illustre un exemple de chaîne d’instructions SQL. Reportez-vous au document [Syntaxe SQL dans Query Service](../sql/syntax.md) pour plus d’informations sur les syntaxes SQL utilisées.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

Dans l’exemple ci-dessous, `SET` conserve le résultat d’une requête `SELECT` dans la variable locale spécifiée. La variable est étendue sur le bloc anonyme.

L’ID d’instantané est stocké en tant que variable locale (`@current_sid`). Il est ensuite utilisé dans la requête suivante pour renvoyer les résultats en fonction de l’SNAPSHOT du même jeu de données/tableau. Pour plus d’[informations sur la clause d’instantané](../sql/syntax.md#SNAPSHOT-clause), consultez la documentation sur la syntaxe SQL.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Bloc anonyme avec clients tiers {#third-party-clients}

Certains clients tiers peuvent avoir besoin d’un identifiant distinct avant et après un bloc SQL pour indiquer qu’une partie du script doit être traitée comme une seule instruction. Si vous recevez un message d’erreur lors de l’utilisation de Query Service avec un client tiers, vous devez vous référer à la documentation du client tiers concernant l’utilisation d’un bloc SQL.

Par exemple, **DbVisualizer** nécessite que le délimiteur soit le seul texte sur la ligne. Dans DbVisualizer, la valeur par défaut de l’identifiant de début est `--/` et, pour l’identifiant de fin, elle est `/`. Vous trouverez ci-dessous un exemple de bloc anonyme dans DbVisualizer :

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

Pour DbVisualizer en particulier, il existe également une option dans l’interface utilisateur de &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. Pour plus d’informations, consultez la [documentation de DbVisualizer](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer) .

## Étapes suivantes

En lisant ce document, vous avez aquis une compréhension claire des blocs anonymes et de leur structure. Pour plus d’informations sur l’écriture de requêtes, consultez le [guide d’exécution de requête](../best-practices/writing-queries.md) .

Vous devez également consulter la section [ sur l’utilisation des blocs anonymes avec le modèle de conception de charge incrémentielle ](./incremental-load.md) pour augmenter l’efficacité des requêtes.
