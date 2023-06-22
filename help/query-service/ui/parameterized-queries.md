---
title: Requêtes paramétrées
description: Découvrez comment utiliser des requêtes paramétrées dans l’interface utilisateur de Adobe Experience Platform.
source-git-commit: e9deabe1e0514f44be085e558fd2fdbf54956f3e
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# Requêtes paramétrées

>[!IMPORTANT]
>
>La fonction d’IU de requête paramétrée est disponible dans une **version limitée uniquement** et n’est pas disponible pour tous les clients.

Query Service prend en charge l’utilisation de requêtes paramétrées dans Query Editor. Avec les requêtes paramétrées, vous pouvez désormais utiliser des espaces réservés pour les paramètres et ajouter les valeurs de paramètre au moment de l’exécution. Les espaces réservés vous permettent d’utiliser des données dynamiques dans lesquelles vous ne savez pas quelles seront les valeurs tant que l’instruction n’est pas exécutée. Vous pouvez également préparer vos requêtes à l’avance et les réutiliser à des fins similaires. La réutilisation de requêtes permet d’économiser un effort considérable, car vous évitez de créer des requêtes SQL distinctes pour chaque cas d’utilisation.

## Conditions préalables

Avant de poursuivre avec ce guide, lisez le [Guide de l’interface utilisateur de Query Editor](./user-guide.md). Le guide Query Editor fournit des informations détaillées sur la manière d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur de l’Experience Platform.

>[!NOTE]
>
>Dans l’interface utilisateur de Adobe Experience Platform, les requêtes paramétrées ne sont prises en charge qu’au niveau parent des modèles intégrés. Cela signifie que les requêtes paramétrées ne fonctionnent que lorsqu’elles sont utilisées dans le modèle d’origine. Les modèles enfants doivent être un modèle statique et ne peuvent pas comporter de paramètres dynamiques. Voir [documentation sur les modèles en ligne](../essential-concepts/inline-templates.md) pour en savoir plus.

## Syntaxe de requête paramétrée {#syntax}

Les requêtes paramétrées utilisent le format `'$YOUR_PARAMETER_NAME'` et peuvent être concaténés à l’aide de la notation par points. Vous trouverez ci-dessous un exemple d’instruction SQL qui utilise des requêtes paramétrées.

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

Pour créer votre requête paramétrée dans l’interface utilisateur, accédez à l’éditeur de requêtes. Voir la section sur [Accès à Query Editor](./user-guide.md#accessing-query-editor) pour plus d’instructions.

Utilisez la variable `'$'` pour saisir un paramètre de requête dans votre requête dans l’éditeur de texte. Ajoutez ensuite la valeur manquante pour la clé dans la variable [!UICONTROL Paramètres de requête] sous l’éditeur. La requête ne peut pas être exécutée si vous négligez d’ajouter une valeur à l’une des clés requises. Icône d’alerte (![Icône d’alerte.](../images/ui/parameterized-queries/alert-icon.png)) apparaît dans la section Paramètres de requête en regard de tout élément vide [!UICONTROL Valeur] champs de saisie.

![L’éditeur de requêtes avec une requête paramétrée et la section Paramètres de requête sont surlignés.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Modifier les onglets depuis [!UICONTROL Paramètres de requête] to [!UICONTROL Console] pour visualiser la sortie console de la requête.

Si vous supprimez un paramètre et tentez de relancer la requête après son exécution, un message d’erreur s’affiche dans la variable [!UICONTROL Paramètres de requête] pour vous alerter.

![L’éditeur de requêtes avec un champ de valeur vide et l’erreur des paramètres de requête mise en surbrillance.](../images/ui/parameterized-queries/query-parameter-error.png)

## Utiliser les détails des logs de requête pour vérifier les valeurs des paramètres {#check-parameter-values}

Vous ne pouvez pas enregistrer de paramètres dans les modèles, car les valeurs utilisées ne sont pas persistantes. Vous pouvez toutefois vérifier la variable [!UICONTROL Détails du journal de requête] pour rechercher les valeurs de paramètre utilisées dans une exécution de requête. Dans ce cas, les logs n&#39;indiquent pas que la requête était paramétrée. Voir [documentation sur les journaux de requête](./query-logs.md) pour obtenir des instructions sur la manière de trouver les valeurs utilisées.

![La vue des logs de requête avec le SQL d’une requête paramétrée mise en surbrillance dans la section détails.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Planification d’une requête paramétrée {#schedule}

Les valeurs des paramètres sont enregistrées lorsque vous planifiez une requête paramétrée. Pour planifier une requête paramétrée, suivez le processus type pour créer une requête planifiée comme décrit dans le guide de [création d’un planning de requête](./query-schedules.md#create-schedule), puis saisissez les valeurs de paramètre à utiliser dans l’exécution de la requête. Cette section de l’interface utilisateur s’affiche uniquement pour les requêtes paramétrées. Voir la section sur [définition des paramètres d’une requête planifiée](./query-schedules.md#set-parameters) pour obtenir des instructions spécifiques.

>[!TIP]
>
>Query Service prend en charge les instructions préparées à l’aide de requêtes paramétrées. Voir [guide de syntaxe des instructions préparées](../sql/prepared-statements.md) pour plus d’informations sur la syntaxe SQL impliquée.

## Étapes suivantes

En lisant ce document, vous avez appris à paramétrer des requêtes dans l’interface utilisateur de Adobe Experience Platform et à les utiliser dans des exécutions de requêtes planifiées. Le document a également mis en évidence la manière de vérifier les journaux pour les valeurs de paramètre utilisées dans les exécutions de requête.

Si ce n’est déjà fait, il est recommandé de lire le guide sur la [surveillance des requêtes planifiées](./monitor-queries.md) pour mieux comprendre l’état de toutes les tâches de requête via l’interface utilisateur de Platform.
