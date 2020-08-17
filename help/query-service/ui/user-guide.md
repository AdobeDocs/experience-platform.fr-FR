---
keywords: Experience Platform;home;popular topics;Query editor;query editor
solution: Experience Platform
title: Guide d’utilisation de Query Editor
topic: query editor
description: Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service. Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans Experience Platform.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 72%

---


# [!DNL Query Editor] guide de l&#39;utilisateur

[!DNL Query Editor] est un outil interactif fourni par Adobe . Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. [!DNL Query Service][!DNL Experience Platform] [!DNL Query Editor] prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans [!DNL Experience Platform].

For more information about the concepts and features of [!DNL Query Service], see the [Query Service overview][query-service-overview]. To learn more about how to navigate the Query Service user interface on [!DNL Platform], see the [Query Service UI overview][query-service-ui].

## Prise en main

[!DNL Query Editor]En se connectant à permet une exécution flexible des requêtes, possible uniquement tant que cette connexion est active.[!DNL Query Service]

### Connecting to [!DNL Query Service]

[!DNL Query Editor] prend quelques secondes pour initialiser et se connecter à [!DNL Query Service] quand il est ouvert. La console vous indique qu’il est connecté, comme illustré ci-dessous. Si vous tentez d’exécuter une requête avant que l’éditeur ne soit connecté, l’exécution est retardée jusqu’à ce que la connexion soit établie.

![Image](../images/queries/query-editor-overview/initializing-connection.png)

### How queries are run from [!DNL Query Editor]

Queries executed from [!DNL Query Editor] run interactively. Cela signifie que la requête sera annulée si vous fermez le navigateur ou quittez l’éditeur. Cela concerne également les requêtes visant à générer des jeux de données à partir de sorties de requête.

## Query authoring using [!DNL Query Editor]

Using [!DNL Query Editor], you can write, execute, and save queries for customer experience data. All queries executed in [!DNL Query Editor], or saved, are available to all users in your organization with access to [!DNL Query Service].

### Accéder aux [!DNL Query Editor]

In the [!DNL Experience Platform] UI, click **[!UICONTROL Queries]** in the left navigation menu to open the [!DNL Query Service] workspace. Cliquez ensuite sur **[!UICONTROL Créer une requête]** dans la partie supérieure droite de l’écran pour commencer à écrire des requêtes. This link is available from any of the pages in the [!DNL Query Service] workspace.

![Image](../images/queries/query-editor-overview/create-query.png)

### Rédaction de requêtes

[!UICONTROL Query Editor est organisé de façon à rendre l’écriture de requête aussi facile que possible. ] La capture d’écran ci-dessous présente l’affichage de l’éditeur dans l’interface utilisateur. Le bouton **Lire** et le champ d’entrée SQL sont mis en surbrillance.

![Image](../images/queries/query-editor-overview/editor.png)

Pour réduire le temps de développement, nous vous recommandons de développer vos requêtes en fixant des limites sur les lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête produit la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT`, afin de générer un jeu de données avec la sortie.

### Writing tools in [!DNL Query Editor]

- **Mise en surbrillance automatique de la syntaxe :** facilite la lecture et l’organisation SQL.

![Image](../images/queries/query-editor-overview/syntax-highlight.png)

- **Saisie automatique de mot-clé SQL :** commencez à saisir votre requête, puis utiliser les touches fléchées pour accéder au terme souhaité et appuyez sur **Entrée**.

![Image](../images/queries/query-editor-overview/syntax-auto.png)

- **Saisie automatique de tableau et de champ :** commencez à saisir le nom du tableau auquel vous souhaitez appliquer `SELECT`, puis utilisez les touches fléchées pour accéder au tableau recherché et appuyez sur **Entrée**. Une fois le tableau sélectionné, la saisie automatique reconnaît les champs de ce tableau.

![Image](../images/queries/query-editor-overview/tables-auto.png)

### Détection des erreurs

[!DNL Query Editor] valide automatiquement la requête au fur et à mesure que vous l’écrivez grâce à une validation SQL générique et une validation d’exécution spécifique. Si un trait de soulignement rouge apparaît sous la requête (comme illustré dans l’image ci-dessous), il indique une erreur dans la requête.

![Image](../images/queries/query-editor-overview/syntax-error-highlight.png)

Lorsque des erreurs sont détectées, vous pouvez afficher les messages d’erreur spécifiques en survolant le code SQL avec la souris.

![Image](../images/queries/query-editor-overview/linting-error.png)

### Détails de la requête

While you are viewing a query in [!DNL Query Editor], the *[!UICONTROL Query Details]* panel provides tools to manage the selected query.

![Image](../images/queries/query-editor-overview/query-details.png)

Ce panneau vous permet de générer un jeu de données de sortie directement depuis l’interface utilisateur, de supprimer ou de nommer la requête affichée, et d’afficher le code SQL dans un format facile à copier dans l’onglet *[!UICONTROL Requête SQL]*. Ce panneau présente également des métadonnées utiles, telles que la dernière fois où la requête a été modifiée et qui l’a modifiée, le cas échéant. Pour générer un jeu de données, cliquez sur **[!UICONTROL Jeu de données de sortie]**. La boîte de dialogue *[!UICONTROL Jeu de données de sortie]* s’affiche. Saisissez un nom et une description, puis cliquez sur **[!UICONTROL Exécuter la requête]**. Le nouveau jeu de données s’affiche dans l’onglet *[!UICONTROL Jeux de données]*[!DNL Query Service] de l’interface utilisateur de dans [!DNL Platform].

### Enregistrement des requêtes

[!DNL Query Editor] dispose d’une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Pour enregistrer une requête, cliquez sur **[!UICONTROL Enregistrer]** dans le coin supérieur droit de [!DNL Query Editor]. Avant de pouvoir enregistrer une requête, vous devez lui donner un nom à l’aide du panneau *[!UICONTROL Détails]*.

### Accès aux requêtes précédentes

All queries executed from [!DNL Query Editor] are captured in the Log table. Vous pouvez utiliser la fonctionnalité de recherche dans l’onglet *[!UICONTROL Journal]* pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans l’onglet *[!UICONTROL Parcourir]*.

Pour plus d’informations, reportez-vous à la [Présentation de l’interface utilisateur de Query Service][query-service-ui].

>[!NOTE]
>
>Les requêtes non exécutées ne sont pas enregistrées dans le journal. In order for the query to be available in [!DNL Query Service], it must be run or saved in [!DNL Query Editor].

## Exécution de requête à l’aide de Query Editor

To run a query in [!DNL Query Editor], you can enter SQL in the editor or load a previous query from the *Log* or *[!UICONTROL Browse]* tab, and click **Play**. L’état de l’exécution de la requête s’affiche dans l’onglet *[!UICONTROL Console]* ci-dessous et les données de sortie s’affichent dans l’onglet *[!UICONTROL Résultats]*.

### Console

La console fournit des informations sur l’état et le fonctionnement de [!DNL Query Service]. The console displays the connection status to [!DNL Query Service], query operations being executed, and any error messages that result from those queries.

![Image](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l’exécution d’une requête. Elle n’affiche pas les erreurs de validation de requête avant l’exécution de la requête.

### Résultats de requête

Une fois la requête terminée, les résultats s’affichent dans l’onglet *[!UICONTROL Résultats]*, en regard de l’onglet *[!UICONTROL Console]*. Cet affichage indique la sortie tabulaire de votre requête (jusqu’à 100 lignes). Il vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées, puis exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le [tutoriel sur la génération de jeux de données][query-service-create-datasets] pour apprendre à générer un jeu de données à partir des résultats de requête dans [!DNL Query Editor].

![Image](../images/queries/query-editor-overview/query-results.png)

## Exécution de requêtes avec une vidéo [!DNL Query Service] didacticiel

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. En outre, l&#39;utilisation de propriétés individuelles dans un objet XDM, l&#39;utilisation de fonctions définies par Adobe et l&#39;utilisation de CREATE TABLE AS SELECT (CTAS) sont démontrées.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Étapes suivantes

Now that you know what features are available in [!DNL Query Editor] and how to navigate the application, you can start authoring your own queries directly in [!DNL Platform]. For more information about running SQL queries against datasets in [!DNL Data Lake], see the guide on [running queries][query-service-running-queries]. Pour obtenir un exemple de requête SQL avec des données d’Adobe Analytics et d’Adobe Target, consultez la [référence d’exemples de requête][query-service-sample-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
