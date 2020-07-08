---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l'éditeur de Requête Adobe Experience Platform Requête Service
topic: query editor
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# Guide de l’utilisateur de l’éditeur de Requêtes

Requête Editor est un outil interactif fourni par Adobe Experience Platform Requête Service qui vous permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur Experience Platform. Requête Editor prend en charge les requêtes de développement pour l’analyse et l’exploration des données. Il permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans l’Experience Platform.

Pour plus d&#39;informations sur les concepts et les fonctionnalités de Requête Service, consultez la présentation [de][query-service-overview]Requête Service. Pour en savoir plus sur la navigation dans l’interface utilisateur de Requête Service sur Platform, consultez la présentation [de l’interface utilisateur de][query-service-ui]Requête Service.

## Prise en main

L&#39;éditeur de Requêtes permet une exécution flexible des requêtes en se connectant à Requête Service, et les requêtes ne s&#39;exécuteront que lorsque cette connexion est active.

### Connexion au service de Requête

L’éditeur de Requête prend quelques secondes pour initialiser et se connecter à Requête Service à son ouverture. La console vous indique quand elle est connectée, comme illustré ci-dessous. Si vous tentez d’exécuter une requête avant que l’éditeur ne se connecte, l’exécution est retardée jusqu’à ce que la connexion soit terminée.

![Image](../images/queries/query-editor-overview/initializing-connection.png)

### Exécution des requêtes à partir de l’éditeur de Requêtes

Les Requêtes exécutées à partir de l’éditeur de Requêtes s’exécutent de manière interactive. Cela signifie que si vous fermez le navigateur ou que vous quittez le navigateur, la requête est annulée. Cela est également vrai pour les requêtes créées pour générer des jeux de données à partir de sorties de requête.

## Création de Requêtes à l’aide de l’éditeur de Requête

L’éditeur de Requêtes vous permet d’écrire, d’exécuter et d’enregistrer des requêtes pour les données d’expérience client. Toutes les requêtes exécutées dans l’éditeur de Requêtes, ou enregistrées, sont accessibles à tous les utilisateurs de votre organisation qui ont accès à Requête Service.

### Accès à l’éditeur de Requêtes

Dans l’interface utilisateur de l’Experience Platform, cliquez sur **Requêtes** dans le menu de navigation de gauche pour ouvrir l’espace de travail Requête Service. Cliquez ensuite sur **Créer une Requête** en haut à droite de l’écran pour afficher les requêtes d’écriture de début. Ce lien est disponible à partir de n’importe quelle page de l’espace de travail Requête Service.

![Image](../images/queries/query-editor-overview/create-query.png)

### Ecriture de requêtes

Requête Editor est organisé pour rendre les requêtes d&#39;écriture aussi faciles que possible. La capture d’écran ci-dessous montre comment l’éditeur s’affiche dans l’interface utilisateur, le bouton **Lecture** et le champ d’entrée SQL étant mis en surbrillance.

![Image](../images/queries/query-editor-overview/editor.png)

Pour réduire le temps de développement, il est recommandé de développer des requêtes avec des limites sur les lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête génère la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie.

### Création d’outils dans l’éditeur de Requêtes

- **Mise en surbrillance automatique de la syntaxe :** Facilite la lecture et l&#39;organisation de SQL.

![Image](../images/queries/query-editor-overview/syntax-highlight.png)

- **Remplissage automatique du mot clé SQL :** Début de saisie de votre requête, utilisez les touches fléchées pour accéder au terme souhaité et appuyez sur **Entrée**.

![Image](../images/queries/query-editor-overview/syntax-auto.png)

- **Remplissage automatique du tableau et du champ :** Début de saisie du nom de la table à `SELECT` partir de laquelle vous voulez accéder, puis d&#39;utilisation des touches fléchées pour accéder à la table que vous recherchez, puis appuyez sur **Entrée**. Une fois qu’un tableau est sélectionné, la saisie semi-automatique reconnaît les champs de ce tableau.

![Image](../images/queries/query-editor-overview/tables-auto.png)

### Détection des erreurs

L’éditeur de Requêtes valide automatiquement une requête au fur et à mesure que vous l’écrivez, en fournissant une validation SQL générique et une validation d’exécution spécifique. Si un trait de soulignement rouge apparaît sous la requête (comme illustré dans l’image ci-dessous), il représente une erreur dans la requête.

![Image](../images/queries/query-editor-overview/syntax-error-highlight.png)

Lorsque des erreurs sont détectées, vous pouvez vue les messages d&#39;erreur spécifiques en passant la souris sur le code SQL.

![Image](../images/queries/query-editor-overview/linting-error.png)

### Détails de la Requête

Lorsque vous consultez une requête dans l’éditeur de Requêtes, le panneau Détails *de la* Requête fournit des outils pour gérer la requête sélectionnée.

![Image](../images/queries/query-editor-overview/query-details.png)

Ce panneau vous permet de générer un jeu de données de sortie directement à partir de l&#39;interface utilisateur, de supprimer ou de nommer la requête affichée et de vue du code SQL dans un format facile à copier sur l&#39;onglet Requête ** SQL. Ce panneau présente également des métadonnées utiles, telles que la dernière modification de la requête et la personne qui l’a modifiée, le cas échéant. Pour générer un jeu de données, cliquez sur **Output Dataset**. La boîte de dialogue *Output Dataset* (Jeu de données de sortie) s’affiche. Saisissez un nom et une description, puis cliquez sur **Exécuter la Requête**. Le nouveau jeu de données s’affiche dans l’onglet *Datasets* de l’interface utilisateur de Requête Service sur Platform.

### Enregistrement des requêtes

L’éditeur de Requêtes fournit une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y travailler ultérieurement. Pour enregistrer une requête, cliquez sur **Enregistrer** dans le coin supérieur droit de l’éditeur de Requêtes. Avant de pouvoir enregistrer une requête, un nom doit être fourni pour la requête à l’aide du panneau Détails *de la* Requête.

### Comment trouver les requêtes précédentes

Toutes les requêtes exécutées à partir de l&#39;éditeur de Requêtes sont capturées dans le tableau Journal. Vous pouvez utiliser la fonctionnalité de recherche de l&#39;onglet *Journal* pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans l’onglet *Parcourir* .

Pour plus d’informations, consultez la présentation [de l’interface utilisateur de][query-service-ui] Requête Service.

>[!NOTE]
>
>Les Requêtes qui ne sont pas exécutées ne sont pas enregistrées par le journal. Pour que la requête soit disponible dans Requête Service, elle doit être exécutée ou enregistrée dans l’éditeur de Requêtes.

## Exécution de requêtes à l’aide de l’éditeur de Requêtes

Pour exécuter une requête dans l’éditeur de Requêtes, vous pouvez entrer SQL dans l’éditeur ou charger une requête précédente à partir de l’onglet *Journal* ou *Parcourir* , puis cliquer sur **Lecture**. L’état d’exécution de la requête s’affiche dans l’onglet *Console* ci-dessous et les données de sortie s’affichent dans l’onglet *Résultats* .

### Console

La console fournit des informations sur l’état et le fonctionnement de Requête Service. La console affiche l&#39;état de la connexion à Requête Service, les opérations de requête en cours d&#39;exécution et les messages d&#39;erreur qui en résultent.

![Image](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l’exécution d’une requête. Il n’affiche pas les erreurs de validation de requête avant l’exécution d’une requête.

### Résultats de la Requête

Une fois la requête terminée, les résultats s’affichent dans l’onglet *Résultats* , en regard de l’onglet *Console* . Cette vue affiche la sortie tabulaire de votre requête, affichant jusqu’à 100 lignes. Cette vue vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées et exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le didacticiel [sur la][query-service-create-datasets] génération de jeux de données pour savoir comment générer un jeu de données à partir des résultats de la requête dans l&#39;éditeur de Requêtes.

![Image](../images/queries/query-editor-overview/query-results.png)

## Étapes suivantes

Maintenant que vous savez quelles fonctions sont disponibles dans l’éditeur de Requêtes et comment naviguer dans l’application, vous pouvez début de créer vos propres requêtes directement dans Platform. Pour plus d&#39;informations sur l&#39;exécution de requêtes SQL par rapport à des jeux de données dans Data Lake, consultez le guide sur l&#39; [exécution de requêtes][query-service-running-queries]. Pour obtenir des exemples de requêtes SQL pour l&#39;utilisation des données Analytics et des Adobes Target d&#39;Adobe, reportez-vous à la référence [des][query-service-sample-queries]exemples de requêtes.

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
