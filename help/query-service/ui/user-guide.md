---
keywords: Experience Platform ; accueil ; rubriques populaires ; éditeur de Requêtes ; éditeur de requêtes ; service de Requête ; service de requête ;
solution: Experience Platform
title: Guide de l’interface utilisateur de l’éditeur de requêtes
topic-legacy: query editor
description: L’éditeur de Requêtes est un outil interactif fourni par Adobe Experience Platform Requête Service, qui vous permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur Experience Platform. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
translation-type: tm+mt
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 64%

---

# [!DNL Query Editor] Guide de l’interface

[!DNL Query Editor] est un outil interactif fourni par Adobe . Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. [!DNL Query Service][!DNL Experience Platform] [!DNL Query Editor] prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans [!DNL Experience Platform].

Pour plus d&#39;informations sur les concepts et les fonctionnalités de [!DNL Query Service], consultez la [présentation de Requête Service][query-service-overview]. Pour en savoir plus sur la manière de naviguer dans l&#39;interface utilisateur de Requête Service sur [!DNL Platform], consultez la [Présentation de l&#39;interface utilisateur de Requête Service][query-service-ui].

## Prise en main

[!DNL Query Editor]En se connectant à permet une exécution flexible des requêtes, possible uniquement tant que cette connexion est active.[!DNL Query Service]

### Connexion à [!DNL Query Service]

[!DNL Query Editor] prend quelques secondes pour initialiser et se connecter à  [!DNL Query Service] quand il est ouvert. La console vous indique qu’il est connecté, comme illustré ci-dessous. Si vous tentez d’exécuter une requête avant que l’éditeur ne soit connecté, l’exécution est retardée jusqu’à ce que la connexion soit établie.

![Image](../images/ui/query-editor/connect.png)

### Exécution des requêtes à partir de [!DNL Query Editor]

Les requêtes exécutées à partir de [!DNL Query Editor] s’exécutent de manière interactive. Cela signifie que la requête sera annulée si vous fermez le navigateur ou quittez l’éditeur. Cela concerne également les requêtes visant à générer des jeux de données à partir de sorties de requête.

## Création de requêtes à l’aide de [!DNL Query Editor]

[!DNL Query Editor] vous permet d’écrire, d’exécuter et d’enregistrer des requêtes pour les données d’expérience client. Toutes les requêtes exécutées dans [!DNL Query Editor], ou enregistrées, sont accessibles à tous les utilisateurs de votre organisation ayant accès à [!DNL Query Service].

### Accéder aux [!DNL Query Editor]

Dans l&#39;interface utilisateur [!DNL Experience Platform], sélectionnez **[!UICONTROL Requêtes]** dans le menu de navigation de gauche pour ouvrir l&#39;espace de travail [!DNL Query Service]. Ensuite, sélectionnez **[!UICONTROL Créer une Requête]** en haut à droite de l&#39;écran pour afficher les requêtes d&#39;écriture de début. Ce lien est disponible à partir de n&#39;importe quelle page de l&#39;espace de travail [!DNL Query Service].

![Image](../images/ui/query-editor/create-query.png)

### Rédaction de requêtes

[!UICONTROL Query Editor est organisé de façon à rendre l’écriture de requête aussi facile que possible. ] La capture d’écran ci-dessous présente l’affichage de l’éditeur dans l’interface utilisateur. Le bouton **Lire** et le champ d’entrée SQL sont mis en surbrillance.

![Image](../images/ui/query-editor/editor.png)

Pour réduire le temps de développement, nous vous recommandons de développer vos requêtes en fixant des limites sur les lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête produit la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT`, afin de générer un jeu de données avec la sortie.

### Outils d&#39;écriture dans [!DNL Query Editor]

- **Mise en surbrillance automatique de la syntaxe :** facilite la lecture et l’organisation SQL.

![Image](../images/ui/query-editor/syntax-highlight.png)

- **Saisie automatique de mot-clé SQL :** commencez à saisir votre requête, puis utiliser les touches fléchées pour accéder au terme souhaité et appuyez sur **Entrée**.

![Image](../images/ui/query-editor/syntax-auto.png)

- **Saisie automatique de tableau et de champ :** commencez à saisir le nom du tableau auquel vous souhaitez appliquer `SELECT`, puis utilisez les touches fléchées pour accéder au tableau recherché et appuyez sur **Entrée**. Une fois le tableau sélectionné, la saisie automatique reconnaît les champs de ce tableau.

![Image](../images/ui/query-editor/tables-auto.png)

### Détection des erreurs

[!DNL Query Editor] valide automatiquement la requête au fur et à mesure que vous l’écrivez grâce à une validation SQL générique et une validation d’exécution spécifique. Si un trait de soulignement rouge apparaît sous la requête (comme illustré dans l’image ci-dessous), il indique une erreur dans la requête.

![Image](../images/ui/query-editor/syntax-error-highlight.png)

Lorsque des erreurs sont détectées, vous pouvez afficher les messages d’erreur spécifiques en survolant le code SQL avec la souris.

![Image](../images/ui/query-editor/linting-error.png)

### Détails de la requête

Lorsque vous consultez une requête dans [!DNL Query Editor], le panneau **[!UICONTROL Détails de la Requête]** fournit des outils pour gérer la requête sélectionnée.

![Image](../images/ui/query-editor/query-details.png)

Ce panneau vous permet de générer un jeu de données de sortie directement depuis l’interface utilisateur, de supprimer ou de nommer la requête affichée, et d’afficher le code SQL dans un format facile à copier dans l’onglet **[!UICONTROL Requête SQL]**. Ce panneau présente également des métadonnées utiles, telles que la dernière fois où la requête a été modifiée et qui l’a modifiée, le cas échéant. Pour générer un jeu de données, sélectionnez **[!UICONTROL Output Dataset]**. La boîte de dialogue **[!UICONTROL Jeu de données de sortie]** s’affiche. Saisissez un nom et une description, puis sélectionnez **[!UICONTROL Exécuter la Requête]**. Le nouveau jeu de données s’affiche dans l’onglet **[!UICONTROL Jeux de données]**[!DNL Query Service] de l’interface utilisateur de dans [!DNL Platform].

### Enregistrement des requêtes

[!DNL Query Editor] dispose d’une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Pour enregistrer une requête, sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit de [!DNL Query Editor]. Avant de pouvoir enregistrer une requête, vous devez lui donner un nom à l’aide du panneau **[!UICONTROL Détails]**.

### Accès aux requêtes précédentes

Toutes les requêtes exécutées à partir de [!DNL Query Editor] sont capturées dans la table Journal. Vous pouvez utiliser la fonctionnalité de recherche dans l’onglet **[!UICONTROL Journal]** pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans l’onglet **[!UICONTROL Parcourir]**.

Pour plus d’informations, reportez-vous à la [Présentation de l’interface utilisateur de Query Service][query-service-ui].

>[!NOTE]
>
>Les requêtes non exécutées ne sont pas enregistrées dans le journal. Pour que la requête soit disponible dans [!DNL Query Service], elle doit être exécutée ou enregistrée dans [!DNL Query Editor].

## Exécution de requête à l’aide de Query Editor

Pour exécuter une requête dans [!DNL Query Editor], vous pouvez entrer SQL dans l&#39;éditeur ou charger une requête précédente à partir de l&#39;onglet **[!UICONTROL Journal]** ou **[!UICONTROL Parcourir]**, puis sélectionner **Lecture**. L’état de l’exécution de la requête s’affiche dans l’onglet **[!UICONTROL Console]** ci-dessous et les données de sortie s’affichent dans l’onglet **[!UICONTROL Résultats]**.

### Console

La console fournit des informations sur l’état et le fonctionnement de [!DNL Query Service]. La console affiche l&#39;état de la connexion à [!DNL Query Service], les opérations de requête en cours d&#39;exécution et les messages d&#39;erreur qui en résultent.

![Image](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l’exécution d’une requête. Elle n’affiche pas les erreurs de validation de requête avant l’exécution de la requête.

### Résultats de requête

Une fois la requête terminée, les résultats s’affichent dans l’onglet **[!UICONTROL Résultats]**, en regard de l’onglet **[!UICONTROL Console]**. Cet affichage indique la sortie tabulaire de votre requête (jusqu’à 100 lignes). Il vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées, puis exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le [tutoriel sur la génération de jeux de données][query-service-create-datasets] pour apprendre à générer un jeu de données à partir des résultats de requête dans [!DNL Query Editor].

![Image](../images/ui/query-editor/query-results.png)

## Exécuter des requêtes avec [!DNL Query Service] vidéo didacticiel

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. En outre, l&#39;utilisation de propriétés individuelles dans un objet XDM, l&#39;utilisation de fonctions définies par Adobe et l&#39;utilisation de CREATE TABLE AS SELECT (CTAS) sont démontrées.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Étapes suivantes

Maintenant que vous savez quelles fonctionnalités sont disponibles dans [!DNL Query Editor] et comment naviguer dans l&#39;application, vous pouvez début de créer vos propres requêtes directement dans [!DNL Platform]. Pour plus d&#39;informations sur l&#39;exécution de requêtes SQL par rapport à des jeux de données dans [!DNL Data Lake], consultez le guide sur [l&#39;exécution de requêtes][query-service-running-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../best-practices/writing-queries.md
[query-service-create-datasets]: ./create-datasets.md
