---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide sur Query Editor d’Adobe Experience Platform Query Service
topic: query editor
translation-type: tm+mt
source-git-commit: cc101b1a439408861961c6fcd0899ca7c48bfa04
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 95%

---


# Guide d’utilisation de Query Editor

Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service. Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans Experience Platform.

Pour plus d’informations sur les concepts et les fonctionnalités de Query Service, consultez la [Présentation de Query Service][query-service-overview]. Pour en savoir plus sur la navigation dans l’interface utilisateur de Query Service sur Platform, consultez la [Présentation de l’interface utilisateur de Query Service][query-service-ui].

## Prise en main

En se connectant à Query Service, Query Editor permet une exécution flexible des requêtes, possible uniquement tant que cette connexion est active.

### Connexion à Query Service

Query Editor ne prend que quelques secondes pour l’initialisation et, une fois ouvert, se connecte à Query Service. La console vous indique qu’il est connecté, comme illustré ci-dessous. Si vous tentez d’exécuter une requête avant que l’éditeur ne soit connecté, l’exécution est retardée jusqu’à ce que la connexion soit établie.

![Image](../images/queries/query-editor-overview/initializing-connection.png)

### Exécution des requêtes depuis Query Editor

Dans Query Editor, les requêtes sont exécutées de manière interactive. Cela signifie que la requête sera annulée si vous fermez le navigateur ou quittez l’éditeur. Cela concerne également les requêtes visant à générer des jeux de données à partir de sorties de requête.

## Création de requête à l’aide de Query Editor

Avec Query Editor, vous pouvez écrire, exécuter et enregistrer des requêtes de données d’expérience client. Toutes les requêtes enregistrées ou exécutées dans Query Editor sont accessibles à tous les utilisateurs de votre organisation bénéficiant d’un accès à Query Service.

### Accès à Query Editor

Pour ouvrir l’espace de travail Query Service, cliquez sur **Requêtes** dans le menu de navigation à gauche de l’interface utilisateur d’Experience Platform. Cliquez ensuite sur **Créer une requête** dans la partie supérieure droite de l’écran pour commencer à écrire des requêtes. Ce lien est disponible depuis n’importe quelle page de l’espace de travail Query Service.

![Image](../images/queries/query-editor-overview/create-query.png)

### Rédaction de requêtes

Query Editor est organisé de façon à rendre l’écriture de requête aussi facile que possible. La capture d’écran ci-dessous présente l’affichage de l’éditeur dans l’interface utilisateur. Le bouton **Lire** et le champ d’entrée SQL sont mis en surbrillance.

![Image](../images/queries/query-editor-overview/editor.png)

Pour réduire le temps de développement, nous vous recommandons de développer vos requêtes en fixant des limites sur les lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête produit la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT`, afin de générer un jeu de données avec la sortie.

### Outils d’écriture dans Query Editor

- **Mise en surbrillance automatique de la syntaxe :** facilite la lecture et l’organisation SQL.

![Image](../images/queries/query-editor-overview/syntax-highlight.png)

- **Saisie automatique de mot-clé SQL :** commencez à saisir votre requête, puis utiliser les touches fléchées pour accéder au terme souhaité et appuyez sur **Entrée**.

![Image](../images/queries/query-editor-overview/syntax-auto.png)

- **Saisie automatique de tableau et de champ :** commencez à saisir le nom du tableau auquel vous souhaitez appliquer `SELECT`, puis utilisez les touches fléchées pour accéder au tableau recherché et appuyez sur **Entrée**. Une fois le tableau sélectionné, la saisie automatique reconnaît les champs de ce tableau.

![Image](../images/queries/query-editor-overview/tables-auto.png)

### Détection des erreurs

Query Editor valide automatiquement la requête au fur et à mesure que vous l’écrivez grâce à une validation SQL générique et une validation d’exécution spécifique. Si un trait de soulignement rouge apparaît sous la requête (comme illustré dans l’image ci-dessous), il indique une erreur dans la requête.

![Image](../images/queries/query-editor-overview/syntax-error-highlight.png)

Lorsque des erreurs sont détectées, vous pouvez afficher les messages d’erreur spécifiques en survolant le code SQL avec la souris.

![Image](../images/queries/query-editor-overview/linting-error.png)

### Détails de la requête

Lorsque vous affichez une requête dans Query Editor, le panneau *Détails de la requête* vous fournit des outils pour gérer la requête sélectionnée.

![Image](../images/queries/query-editor-overview/query-details.png)

Ce panneau vous permet de générer un jeu de données de sortie directement depuis l’interface utilisateur, de supprimer ou de nommer la requête affichée, et d’afficher le code SQL dans un format facile à copier dans l’onglet *Requête SQL*. Ce panneau présente également des métadonnées utiles, telles que la dernière fois où la requête a été modifiée et qui l’a modifiée, le cas échéant. Pour générer un jeu de données, cliquez sur **Jeu de données de sortie**. La boîte de dialogue *Jeu de données de sortie* s’affiche. Saisissez un nom et une description, puis cliquez sur **Exécuter la requête**. Le nouveau jeu de données s’affiche dans l’onglet *Jeux de données* de l’interface utilisateur de Query Service dans Platform.

### Enregistrement des requêtes

Query Editor dispose d’une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Pour enregistrer une requête, cliquez sur **Enregistrer** dans le coin supérieur droit de Query Editor. Avant de pouvoir enregistrer une requête, vous devez lui donner un nom à l’aide du panneau *Détails*.

### Accès aux requêtes précédentes

Toutes les requêtes exécutées depuis Query Editor sont capturées dans le tableau Journal. Vous pouvez utiliser la fonctionnalité de recherche dans l’onglet *Journal* pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans l’onglet *Parcourir*.

Pour plus d’informations, reportez-vous à la [Présentation de l’interface utilisateur de Query Service][query-service-ui].

>[!NOTE]
>
>Les requêtes non exécutées ne sont pas enregistrées dans le journal. Pour que la requête soit disponible dans Query Service, elle doit être exécutée ou enregistrée dans Query Editor.

## Exécution de requête à l’aide de Query Editor

Pour exécuter une requête dans Query Editor, vous pouvez saisir du langage SQL dans l’éditeur ou charger une requête précédente depuis l’onglet *Journal* ou l’onglet *Parcourir*, puis cliquer sur **Lire**. L’état de l’exécution de la requête s’affiche dans l’onglet *Console* ci-dessous et les données de sortie s’affichent dans l’onglet *Résultats*.

### Console

La console fournit des informations sur l’état et le fonctionnement de Query Service. La console affiche l’état de la connexion à Query Service, les opérations des requêtes en cours d’exécution et tout message d’erreur résultant de ces requêtes.

![Image](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l’exécution d’une requête. Elle n’affiche pas les erreurs de validation de requête avant l’exécution de la requête.

### Résultats de requête

Une fois la requête terminée, les résultats s’affichent dans l’onglet *Résultats*, en regard de l’onglet *Console*. Cet affichage indique la sortie tabulaire de votre requête (jusqu’à 100 lignes). Il vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées, puis exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le [tutoriel sur la génération de jeux de données][query-service-create-datasets] pour apprendre à générer un jeu de données à partir des résultats de requête dans Query Editor.

![Image](../images/queries/query-editor-overview/query-results.png)

## Vidéo sur l’exécution de requêtes avec Requête Service

La vidéo suivante montre comment exécuter des requêtes dans l&#39;interface d&#39;Adobe Experience Platform et dans un client PSQL. En outre, l&#39;utilisation de propriétés individuelles dans un objet XDM, l&#39;utilisation de fonctions définies par Adobe et l&#39;utilisation de CREATE TABLE AS SELECT (CTAS) sont démontrées.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Étapes suivantes

Maintenant que vous connaissez les fonctionnalités disponibles dans Query Editor et que vous savez naviguer dans l’application, vous pouvez commencer à créer vos requêtes directement dans Platform. Pour plus d’informations sur l’exécution de requêtes SQL par rapport à des jeux de données de lac de données, consultez le guide sur l’[exécution de requêtes][query-service-running-queries]. Pour obtenir un exemple de requête SQL avec des données d’Adobe Analytics et d’Adobe Target, consultez la [référence d’exemples de requête][query-service-sample-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
