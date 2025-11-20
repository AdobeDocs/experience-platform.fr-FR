---
title: Requêtes paramétrées
description: Découvrez comment utiliser des requêtes paramétrées dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 13%

---

# Requêtes paramétrées {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Requêtes paramétrées"
>abstract="Utilisez des requêtes paramétrées pour ajouter des valeurs de paramètre au moment de l’exécution. Vous pouvez ainsi travailler avec des données dynamiques et réutiliser des requêtes pour différents cas d’utilisation. Utilisez la préface `'$'` pour saisir un paramètre de requête dans l’éditeur de texte. Ajoutez ensuite une valeur pour la clé dans la section Paramètres de requête sous l’éditeur."

Query Service prend en charge l’utilisation de requêtes paramétrées dans Query Editor. Avec les requêtes paramétrées, vous pouvez désormais utiliser des espaces réservés pour les paramètres et ajouter les valeurs de paramètre au moment de l’exécution. Les espaces réservés vous permettent de travailler avec des données dynamiques dont vous ne savez pas quelles seront les valeurs tant que l’instruction n’aura pas été exécutée. Vous pouvez également préparer vos requêtes à l’avance et les réutiliser à des fins similaires. La réutilisation des requêtes permet d’économiser un effort considérable, car vous évitez de créer des requêtes SQL distinctes pour chaque cas d’utilisation.

## Conditions préalables

Avant de poursuivre avec ce guide, lisez le [&#x200B; Guide de l’interface utilisateur de Query Editor &#x200B;](./user-guide.md). Le guide de Query Editor fournit des informations détaillées sur la manière d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform.

>[!NOTE]
>
>Dans l’interface utilisateur de Adobe Experience Platform, les requêtes paramétrées ne sont prises en charge qu’au niveau parent des modèles intégrés. Cela signifie que les requêtes paramétrées ne fonctionnent que lorsqu’elles sont utilisées dans le modèle d’origine. Les modèles enfants doivent être des modèles statiques et ne peuvent pas avoir de paramètres dynamiques. Pour en savoir plus, consultez la documentation sur les [modèles intégrés](../key-concepts/inline-templates.md).

## Syntaxe de requête paramétrée {#syntax}

Les requêtes paramétrées utilisent le format `'$YOUR_PARAMETER_NAME'` et peuvent être concaténées à l’aide de la notation par points. Vous trouverez ci-dessous un exemple d’instruction SQL qui utilise des requêtes paramétrées.

```sql
INSERT INTO
   $Database_Name.Schema_Name.adwh_lkup_process_delta_log
   (process_name, merge_policy_id, process_status, process_date, create_ts, change_ts)
SELECT
   '$Table_Process_Name' process_name,
   hash('$Merge_PolicyID') merge_policy_id,
   '$process_status' process_status,
   to_date('$date_key') process_date,
   CURRENT_TIMESTAMP create_ts,
   CURRENT_TIMESTAMP change_ts;
```

## Création d’une requête paramétrée {#create}

Pour créer votre requête paramétrée dans l’interface utilisateur, accédez à l’éditeur de requêtes. Pour plus d’instructions, consultez la section relative à [accès à Query Editor](./user-guide.md#accessing-query-editor).

Utilisez la préface `'$'` pour saisir un paramètre de requête dans l’éditeur de texte. Sélectionnez ensuite l’onglet **[!UICONTROL Query parameters]** en regard de la [!UICONTROL Console] ajouter la valeur manquante pour la clé. La requête ne peut pas être exécutée si vous omettez d’ajouter une valeur à l’une des clés requises. Une icône d’alerte (![une icône d’alerte.](/help/images/icons/alert.png)) apparaît dans la section Paramètres de requête en regard des champs d’entrée de [!UICONTROL Value] vides.

>[!NOTE]
>
>Si votre requête ne prend pas de paramètres, vous pouvez toujours saisir des paramètres inutiles dans l’éditeur de requêtes. Le Query Editor ignore toutes les paires clé-valeur inutiles et elles n’ont aucun effet sur l’exécution ou les résultats de la requête.

![Query Editor avec une requête paramétrée et la section Paramètres de requête mise en surbrillance.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Remplacez les onglets [!UICONTROL Query parameters] par [!UICONTROL Console] pour afficher la sortie console de la requête.

## Utiliser les détails des journaux de requête pour vérifier les valeurs de paramètre {#check-parameter-values}

Vous ne pouvez pas enregistrer de paramètres dans les modèles, car les valeurs utilisées ne sont pas persistantes. Cependant, vous pouvez vérifier la page [!UICONTROL Query log details] pour trouver les valeurs de paramètre utilisées dans une exécution de requête. Dans ce cas, les journaux n’indiquent pas que la requête était une requête paramétrée. Consultez la [documentation sur les journaux de requêtes](./query-logs.md) pour obtenir des instructions sur la manière de trouver les valeurs utilisées.

![La vue des logs de requête avec le SQL d’une requête paramétrée mise en surbrillance dans la section détails.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Planifier une requête paramétrée {#schedule}

Les valeurs de paramètre sont enregistrées lorsque vous planifiez une requête paramétrée. Pour planifier une requête paramétrée, suivez le processus standard de création d’une requête planifiée comme décrit dans le guide de [création d’un planning de requête](./query-schedules.md#create-schedule), puis saisissez les valeurs de paramètre à utiliser dans l’exécution de la requête. Cette section de l’interface utilisateur s’affiche uniquement pour les requêtes paramétrées. Pour obtenir des instructions spécifiques, reportez-vous à la section [Définition des paramètres d’une requête paramétrée planifiée](./query-schedules.md#set-parameters).

>[!TIP]
>
>Query Service prend en charge les instructions préparées à l’aide de requêtes paramétrées. Pour plus d’informations sur la syntaxe SQL impliquée[&#x200B; consultez le &#x200B;](../sql/prepared-statements.md) guide de syntaxe des instructions préparées .

## Étapes suivantes

En lisant ce document, vous avez appris à paramétrer les requêtes dans l’interface utilisateur de Adobe Experience Platform et à les utiliser dans des exécutions de requêtes planifiées. Le document a également mis en évidence comment vérifier les journaux pour les valeurs de paramètre utilisées dans les exécutions de requête.

Nous vous recommandons ensuite de lire le guide sur la [surveillance des requêtes planifiées](./monitor-queries.md) pour mieux comprendre le statut de tous les traitements de requêtes via l’interface utilisateur d’Experience Platform.
