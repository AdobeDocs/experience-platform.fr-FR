---
title: Requêtes paramétrées
description: Découvrez comment utiliser des requêtes paramétrées dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 13%

---

# Requêtes paramétrées {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Requêtes paramétrées"
>abstract="Utilisez des requêtes paramétrées pour ajouter des valeurs de paramètre au moment de l’exécution. Vous pouvez ainsi travailler avec des données dynamiques et réutiliser des requêtes pour différents cas d’utilisation. Utilisez la préface `'$'` pour saisir un paramètre de requête dans l’éditeur de texte. Ajoutez ensuite une valeur pour la clé dans la section Paramètres de requête sous l’éditeur."

Query Service prend en charge l’utilisation de requêtes paramétrées dans Query Editor. Avec les requêtes paramétrées, vous pouvez désormais utiliser des espaces réservés pour les paramètres et ajouter les valeurs de paramètre au moment de l’exécution. Les espaces réservés vous permettent d’utiliser des données dynamiques dans lesquelles vous ne savez pas quelles seront les valeurs tant que l’instruction n’est pas exécutée. Vous pouvez également préparer vos requêtes à l’avance et les réutiliser à des fins similaires. La réutilisation de requêtes permet d’économiser un effort considérable, car vous évitez de créer des requêtes SQL distinctes pour chaque cas d’utilisation.

## Conditions préalables

Avant de poursuivre avec ce guide, lisez le [guide de l’interface utilisateur de Query Editor](./user-guide.md). Le guide Query Editor fournit des informations détaillées sur la manière d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur de l’Experience Platform.

>[!NOTE]
>
>Dans l’interface utilisateur de Adobe Experience Platform, les requêtes paramétrées ne sont prises en charge qu’au niveau parent des modèles intégrés. Cela signifie que les requêtes paramétrées ne fonctionnent que lorsqu’elles sont utilisées dans le modèle d’origine. Les modèles enfants doivent être un modèle statique et ne peuvent pas comporter de paramètres dynamiques. Pour en savoir plus, consultez la [documentation sur les modèles intégrés](../key-concepts/inline-templates.md) .

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

## Créer une requête paramétrée {#create}

Pour créer votre requête paramétrée dans l’interface utilisateur, accédez à l’éditeur de requêtes. Pour plus d’informations, reportez-vous à la section sur l’ [accès à l’éditeur de requêtes](./user-guide.md#accessing-query-editor) .

Utilisez la préface `'$'` pour saisir un paramètre de requête dans l’éditeur de texte. Ensuite, sélectionnez l’onglet **[!UICONTROL Paramètres de requête]** en regard de la [!UICONTROL Console] pour ajouter la valeur manquante pour la clé. La requête ne peut pas être exécutée si vous négligez d’ajouter une valeur à l’une des clés requises. Icône d’alerte (![ icône d’alerte.](/help/images/icons/alert.png)) apparaît dans la section Paramètres de requête en regard des champs d’entrée [!UICONTROL Valeur] vides.

>[!NOTE]
>
>Si votre requête ne prend pas de paramètres, vous pouvez toujours saisir des paramètres inutiles dans l’éditeur de requêtes. L’éditeur de requêtes ignore toutes les paires clé-valeur inutiles et elles n’ont aucun effet sur l’exécution ou les résultats de la requête.

![L’éditeur de requêtes avec une requête paramétrée et la section Paramètres de requête mise en surbrillance.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Remplacez les onglets de [!UICONTROL Paramètres de requête] par [!UICONTROL Console] pour afficher la sortie console de la requête.

## Utiliser les détails des logs de requête pour vérifier les valeurs des paramètres {#check-parameter-values}

Vous ne pouvez pas enregistrer de paramètres dans les modèles, car les valeurs utilisées ne sont pas persistantes. Cependant, vous pouvez consulter la page [!UICONTROL Détails du journal de requête] pour trouver les valeurs de paramètre utilisées dans une exécution de requête. Dans ce cas, les logs n&#39;indiquent pas que la requête était paramétrée. Pour obtenir des instructions sur la recherche des valeurs utilisées, reportez-vous à la [documentation sur les journaux de requête](./query-logs.md).

![La vue des logs de requête avec le SQL d&#39;une requête paramétrée mise en surbrillance dans la section des détails.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Planification d’une requête paramétrée {#schedule}

Les valeurs des paramètres sont enregistrées lorsque vous planifiez une requête paramétrée. Pour planifier une requête paramétrée, suivez le processus type pour créer une requête planifiée comme décrit dans le guide [créer un planning de requête](./query-schedules.md#create-schedule), puis saisissez les valeurs de paramètre à utiliser dans l’exécution de la requête. Cette section de l’interface utilisateur s’affiche uniquement pour les requêtes paramétrées. Pour obtenir des instructions spécifiques, reportez-vous à la section sur la [définition des paramètres pour une requête paramétrée planifiée](./query-schedules.md#set-parameters) .

>[!TIP]
>
>Query Service prend en charge les instructions préparées à l’aide de requêtes paramétrées. Pour plus d’informations sur la syntaxe SQL impliquée, consultez le [guide de syntaxe d’instructions préparées](../sql/prepared-statements.md) .

## Étapes suivantes

En lisant ce document, vous avez appris à paramétrer des requêtes dans l’interface utilisateur de Adobe Experience Platform et à les utiliser dans des exécutions de requêtes planifiées. Le document a également mis en évidence la manière de vérifier les journaux pour les valeurs de paramètre utilisées dans les exécutions de requête.

Ensuite, il est recommandé de lire le guide sur la [surveillance des requêtes planifiées](./monitor-queries.md) pour mieux comprendre l’état de toutes les tâches de requête via l’interface utilisateur de Platform.
