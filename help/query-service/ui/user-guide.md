---
keywords: Experience Platform;accueil;rubriques populaires;éditeur de requêtes;éditeur de requêtes;service de requête;service de requête;
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Editor
topic-legacy: query editor
description: Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service qui vous permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur de l’Experience Platform. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: c8b3b22b678622c31462ba0baa2f50fbe89b00d5
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 37%

---

# Guide de l’interface utilisateur du [!DNL Query Editor]

[!DNL Query Editor] est un outil interactif fourni par Adobe . Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. [!DNL Query Service][!DNL Experience Platform] [!DNL Query Editor] prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans [!DNL Experience Platform].

Pour plus d’informations sur les concepts et les fonctionnalités de [!DNL Query Service], reportez-vous à la section [Présentation de Query Service](../home.md). Pour en savoir plus sur la navigation dans l’interface utilisateur de Query Service sur [!DNL Platform], reportez-vous à la section [Présentation de l’interface utilisateur de Query Service](./overview.md).

## Prise en main {#getting-started}

[!DNL Query Editor]En se connectant à permet une exécution flexible des requêtes, possible uniquement tant que cette connexion est active.[!DNL Query Service]

### Connexion à [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] prend quelques secondes pour l’initialisation et la connexion à [!DNL Query Service] lorsqu’il est ouvert. La console vous indique quand elle est connectée, comme illustré ci-dessous. Si vous tentez d’exécuter une requête avant que l’éditeur ne soit connecté, l’exécution est retardée jusqu’à ce que la connexion soit établie.

![Image](../images/ui/query-editor/connect.png)

### Exécution des requêtes à partir de [!DNL Query Editor] {#run-a-query}

Requêtes exécutées depuis [!DNL Query Editor] s’exécuter de manière interactive. Cela signifie que la requête sera annulée si vous fermez le navigateur ou quittez l’éditeur. Cela concerne également les requêtes visant à générer des jeux de données à partir de sorties de requête.

## Création de requêtes à l’aide de [!DNL Query Editor] {#query-authoring}

Utilisation [!DNL Query Editor], vous pouvez écrire, exécuter et enregistrer des requêtes pour les données d’expérience client. Toutes les requêtes exécutées ou enregistrées dans [!DNL Query Editor] sont disponibles pour tous les utilisateurs de votre entreprise ayant accès à [!DNL Query Service].

### Accéder à [!DNL Query Editor] {#accessing-query-editor}

Dans le [!DNL Experience Platform] Interface utilisateur, sélectionnez **[!UICONTROL Requêtes]** dans le menu de navigation de gauche pour ouvrir la [!DNL Query Service] workspace. Ensuite, sélectionnez **[!UICONTROL Créer une requête]** en haut à droite de l’écran pour commencer à écrire des requêtes. Ce lien est disponible à partir de n’importe quelle page de la [!DNL Query Service] workspace.

![Image](../images/ui/query-editor/create-query.png)

### Rédaction de requêtes {#writing-queries}

[!UICONTROL Query Editor est organisé de façon à rendre l’écriture de requête aussi facile que possible. ] La capture d’écran ci-dessous présente l’affichage de l’éditeur dans l’interface utilisateur. Le bouton **Lire** et le champ d’entrée SQL sont mis en surbrillance.

![Image](../images/ui/query-editor/editor.png)

Pour réduire le temps de développement, nous vous recommandons de développer vos requêtes en fixant des limites sur les lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête produit la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT`, afin de générer un jeu de données avec la sortie.

### Outils d’écriture dans [!DNL Query Editor] {#writing-tools}

- **Mise en surbrillance automatique de la syntaxe :** facilite la lecture et l’organisation SQL.

![Image](../images/ui/query-editor/syntax-highlight.png)

- **Saisie automatique des mots-clés SQL :** Commencez à saisir votre requête, puis utilisez les touches fléchées pour accéder au terme souhaité et appuyez sur **Entrée**.

![Image](../images/ui/query-editor/syntax-auto.png)

- **Saisie automatique de tableau et de champ :** commencez à saisir le nom du tableau auquel vous souhaitez appliquer `SELECT`, puis utilisez les touches fléchées pour accéder au tableau recherché et appuyez sur **Entrée**. Une fois le tableau sélectionné, la saisie automatique reconnaît les champs de ce tableau.

![Image](../images/ui/query-editor/tables-auto.png)

### Détection des erreurs {#error-detection}

[!DNL Query Editor] valide automatiquement la requête au fur et à mesure que vous l’écrivez grâce à une validation SQL générique et une validation d’exécution spécifique. Si un trait de soulignement rouge apparaît sous la requête (comme illustré dans l’image ci-dessous), il indique une erreur dans la requête.

![Image](../images/ui/query-editor/syntax-error-highlight.png)

Lorsque des erreurs sont détectées, vous pouvez afficher les messages d’erreur spécifiques en survolant le code SQL avec la souris.

![Image](../images/ui/query-editor/linting-error.png)

### Détails de la requête {#query-details}

Lorsque vous affichez une requête dans [!DNL Query Editor], la variable **[!UICONTROL Détails de la requête]** fournit des outils pour gérer la requête sélectionnée.

![Image](../images/ui/query-editor/query-details.png)

Ce panneau vous permet de générer un jeu de données de sortie directement à partir de l’interface utilisateur, de supprimer ou de nommer la requête affichée, et d’ajouter un planning à la requête.

Ce panneau présente également des métadonnées utiles, telles que la dernière fois où la requête a été modifiée et qui l’a modifiée, le cas échéant. Pour générer un jeu de données, sélectionnez **[!UICONTROL Jeu de données de sortie]**. La boîte de dialogue **[!UICONTROL Jeu de données de sortie]** s’affiche. Saisissez un nom et une description, puis sélectionnez **[!UICONTROL Exécuter la requête]**. Le nouveau jeu de données s’affiche dans l’onglet **[!UICONTROL Jeux de données]**[!DNL Query Service] de l’interface utilisateur de dans [!DNL Platform].

### Requêtes planifiées {#scheduled-queries}

>[!IMPORTANT]
>
>Vous trouverez ci-dessous une liste des limites relatives aux requêtes planifiées lors de l’utilisation de Query Editor. Elles ne s’appliquent pas au [!DNL Query Service] API :<br/>Vous pouvez uniquement ajouter un planning à une requête qui a déjà été créée, enregistrée et exécutée.<br/>You **cannot** ajoutez un planning à une requête paramétrée.<br/>Requêtes planifiées **cannot** contiennent un bloc anonyme.

Pour ajouter un planning à une requête, sélectionnez **[!UICONTROL Ajouter un planning]**.

![Image](../images/ui/query-editor/add-schedule.png)

Le **[!UICONTROL Détails de la planification]** s’affiche. Sur cette page, vous pouvez choisir la fréquence de la requête planifiée, les dates d’exécution de la requête planifiée, ainsi que le jeu de données vers lequel exporter la requête.

![Image](../images/ui/query-editor/schedule-details.png)

Vous pouvez choisir les options suivantes pour **[!UICONTROL Fréquence]**:

- **[!UICONTROL Horaire]**: La requête planifiée s’exécute toutes les heures pour la période que vous avez sélectionnée.
- **[!UICONTROL Quotidien]**: La requête planifiée s’exécute tous les X jours à l’heure et à la période que vous avez sélectionnée. Notez que l’heure sélectionnée est indiquée dans **UTC**, et non votre fuseau horaire local.
- **[!UICONTROL Hebdomadaire]**: La requête sélectionnée s’exécute les jours de la semaine, de l’heure et de la période que vous avez sélectionnée. Notez que l’heure sélectionnée est indiquée dans **UTC**, et non votre fuseau horaire local.
- **[!UICONTROL Mensuel]**: La requête sélectionnée s’exécute tous les mois au jour, à l’heure et à la période que vous avez sélectionnée. Notez que l’heure sélectionnée est indiquée dans **UTC**, et non votre fuseau horaire local.
- **[!UICONTROL Annuel]**: La requête sélectionnée s’exécute chaque année au jour, au mois, à l’heure et à la période que vous avez sélectionnée. Notez que l’heure sélectionnée est indiquée dans **UTC**, et non votre fuseau horaire local.

Pour le jeu de données, vous avez la possibilité d’utiliser un jeu de données existant ou de créer un nouveau jeu de données.

>[!IMPORTANT]
>
> Puisque vous utilisez un jeu de données existant ou que vous en créez, vous procédez comme suit : **not** Vous devez inclure : `INSERT INTO` ou `CREATE TABLE AS SELECT` dans le cadre de la requête, puisque les jeux de données sont déjà définis. Y compris l’une ou l’autre `INSERT INTO` ou `CREATE TABLE AS SELECT` dans le cadre de vos requêtes planifiées, une erreur se produira.

Après avoir confirmé tous ces détails, sélectionnez **[!UICONTROL Enregistrer]** pour créer un planning.

La page des détails de la requête réapparaît. Elle affiche désormais les détails du nouveau planning, y compris l’identifiant du planning, le planning lui-même et le jeu de données de sortie du planning. Vous pouvez utiliser l’ID de planning pour rechercher plus d’informations sur les exécutions de la requête planifiée elle-même. Pour en savoir plus, veuillez lire le [guide des points de fin d’exécution de requête planifiée](../api/runs-scheduled-queries.md).

>[!NOTE]
>
> Vous pouvez uniquement planifier **one** modèle de requête à l’aide de l’interface utilisateur. Si vous souhaitez ajouter des plannings supplémentaires à un modèle de requête, vous devez utiliser l’API . Si un planning a déjà été ajouté à l’aide de l’API, vous serez **not** peuvent ajouter des plannings supplémentaires à l’aide de l’interface utilisateur. Si plusieurs planifications sont déjà jointes à un modèle de requête, seule la planification la plus ancienne s’affiche. Pour savoir comment ajouter des plannings à l’aide de l’API, veuillez lire le [guide de point de terminaison des requêtes planifiées](../api/scheduled-queries.md).
>
> En outre, vous devez actualiser la page si vous souhaitez vous assurer que vous disposez de l’état le plus récent pour le planning que vous consultez.

#### Suppression d’un planning {#delete-schedule}

Vous pouvez supprimer un planning en sélectionnant **[!UICONTROL Suppression d’un planning]**.

![Image](../images/ui/query-editor/delete-schedule.png)

>[!IMPORTANT]
>
> Si vous souhaitez supprimer un planning pour une requête, vous devez d’abord désactiver ce planning.

### Enregistrement des requêtes {#saving-queries}

[!DNL Query Editor] dispose d’une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Pour enregistrer une requête, sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit de [!DNL Query Editor]. Avant de pouvoir enregistrer une requête, vous devez lui donner un nom à l’aide du panneau **[!UICONTROL Détails]**.

>[!NOTE]
>
>Les requêtes nommées et enregistrées dans à l’aide de l’éditeur de requêtes sont disponibles sous forme de modèles dans le tableau de bord Requête . [!UICONTROL Parcourir] . Voir [documentation sur les modèles](./query-templates.md) pour plus d’informations.

### Accès aux requêtes précédentes {#previous-queries}

Toutes les requêtes exécutées depuis [!DNL Query Editor] sont capturés dans le tableau Journal. Vous pouvez utiliser la fonctionnalité de recherche dans l’onglet **[!UICONTROL Journal]** pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans l’onglet **[!UICONTROL Parcourir]**.

Pour plus d’informations, reportez-vous à la [Présentation de l’interface utilisateur de Query Service](./overview.md).

>[!NOTE]
>
>Les requêtes non exécutées ne sont pas enregistrées dans le journal. Pour que la requête soit disponible dans [!DNL Query Service], il doit être exécuté ou enregistré dans [!DNL Query Editor].

## Exécution de requête à l’aide de Query Editor {#executing-queries}

Pour exécuter une requête dans [!DNL Query Editor], vous pouvez saisir du code SQL dans l’éditeur ou charger une requête précédente à partir de la fonction **[!UICONTROL Journal]** ou **[!UICONTROL Parcourir]** et sélectionnez **Play**. L’état de l’exécution de la requête s’affiche dans l’onglet **[!UICONTROL Console]** ci-dessous et les données de sortie s’affichent dans l’onglet **[!UICONTROL Résultats]**.

### Console {#console}

La console fournit des informations sur l’état et le fonctionnement de [!DNL Query Service]. La console affiche l’état de la connexion à [!DNL Query Service], les opérations de requête en cours d’exécution et les messages d’erreur qui en résultent.

![Image](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l’exécution d’une requête. Elle n’affiche pas les erreurs de validation de requête avant l’exécution de la requête.

### Résultats de requête {#query-results}

Une fois la requête terminée, les résultats s’affichent dans la variable **[!UICONTROL Résultats]** en regard de l’onglet **[!UICONTROL Console]** . Cet affichage indique la sortie tabulaire de votre requête (jusqu’à 100 lignes). Il vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées, puis exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le [tutoriel sur la génération de jeux de données](./create-datasets.md) pour apprendre à générer un jeu de données à partir des résultats de requête dans [!DNL Query Editor].

![Image](../images/ui/query-editor/query-results.png)

## Exécuter des requêtes avec [!DNL Query Service] tutoriel vidéo {#query-tutorial-video}

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. De plus, l’utilisation de propriétés individuelles dans un objet XDM, l’utilisation de fonctions définies par l’Adobe et l’utilisation de CREATE TABLE AS SELECT (CTAS) sont illustrées.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Étapes suivantes

Maintenant que vous savez quelles fonctionnalités sont disponibles dans [!DNL Query Editor] et comment naviguer dans l’application, vous pouvez commencer à créer vos propres requêtes directement dans [!DNL Platform]. Pour plus d’informations sur l’exécution de requêtes SQL par rapport à des jeux de données dans [!DNL Data Lake], reportez-vous au guide sur la [exécution de requêtes](../best-practices/writing-queries.md).
