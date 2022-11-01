---
keywords: Experience Platform;accueil;rubriques populaires;éditeur de requêtes;éditeur de requêtes;service de requête;service de requête;
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Editor
topic-legacy: query editor
description: Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service qui vous permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur de l’Experience Platform. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 283c6ba323a327b0c525343a96a45a2412baa67b
workflow-type: tm+mt
source-wordcount: '2081'
ht-degree: 26%

---

# Guide de l’interface utilisateur du [!DNL Query Editor]

[!DNL Query Editor] est un outil interactif fourni par Adobe . Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. [!DNL Query Service][!DNL Experience Platform] [!DNL Query Editor] prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans [!DNL Experience Platform].

Pour plus d’informations sur les concepts et les fonctionnalités de [!DNL Query Service], reportez-vous à la section [Présentation de Query Service](../home.md). Pour en savoir plus sur la navigation dans l’interface utilisateur de Query Service sur [!DNL Platform], reportez-vous à la section [Présentation de l’interface utilisateur de Query Service](./overview.md).

## Prise en main {#getting-started}

[!DNL Query Editor]En se connectant à permet une exécution flexible des requêtes, possible uniquement tant que cette connexion est active.[!DNL Query Service]

### Connexion à [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] prend quelques secondes pour l’initialisation et la connexion à [!DNL Query Service] lorsqu’il est ouvert. La console vous indique quand elle est connectée, comme illustré ci-dessous. Si vous tentez d’exécuter une requête avant que l’éditeur ne soit connecté, l’exécution est retardée jusqu’à ce que la connexion soit établie.

![Sortie de console de l’éditeur de requêtes lors de la connexion initiale.](../images/ui/query-editor/connect.png)

### Exécution des requêtes à partir de [!DNL Query Editor] {#run-a-query}

Requêtes exécutées depuis [!DNL Query Editor] s’exécuter de manière interactive. Cela signifie que la requête sera annulée si vous fermez le navigateur ou quittez l’éditeur. Cela concerne également les requêtes visant à générer des jeux de données à partir de sorties de requête.

## Création de requêtes à l’aide de [!DNL Query Editor] {#query-authoring}

Utilisation [!DNL Query Editor], vous pouvez écrire, exécuter et enregistrer des requêtes pour les données d’expérience client. Toutes les requêtes exécutées ou enregistrées dans [!DNL Query Editor] sont disponibles pour tous les utilisateurs de votre entreprise ayant accès à [!DNL Query Service].

### Accéder à [!DNL Query Editor] {#accessing-query-editor}

Dans le [!DNL Experience Platform] Interface utilisateur, sélectionnez **[!UICONTROL Requêtes]** dans le menu de navigation de gauche pour ouvrir la [!DNL Query Service] workspace. Ensuite, sélectionnez **[!UICONTROL Créer une requête]** en haut à droite de l’écran pour commencer à écrire des requêtes. Ce lien est disponible à partir de n’importe quelle page de la [!DNL Query Service] workspace.

![L&#39;onglet Présentation de l&#39;espace de travail Requêtes avec l&#39;option Créer une requête mise en surbrillance.](../images/ui/query-editor/create-query.png)

### Rédaction de requêtes {#writing-queries}

[!UICONTROL Query Editor est organisé de façon à rendre l’écriture de requête aussi facile que possible. ] La capture d’écran ci-dessous montre l’affichage de l’éditeur dans l’interface utilisateur, avec le champ d’entrée SQL et **Play** surlignée.

![Éditeur de requêtes avec le champ d’entrée SQL et Lecture en surbrillance.](../images/ui/query-editor/editor.png)

Pour réduire le temps de développement, nous vous recommandons de développer vos requêtes en fixant des limites sur les lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête produit la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT`, afin de générer un jeu de données avec la sortie.

### Outils d’écriture dans [!DNL Query Editor] {#writing-tools}

- **Mise en surbrillance automatique de la syntaxe :** facilite la lecture et l’organisation SQL.

![Une instruction SQL dans l’éditeur de requêtes présentant une mise en surbrillance des couleurs de syntaxe.](../images/ui/query-editor/syntax-highlight.png)

- **Saisie automatique des mots-clés SQL :** Commencez à saisir votre requête, puis utilisez les touches fléchées pour accéder au terme souhaité et appuyez sur **Entrée**.

![Quelques caractères SQL avec le menu déroulant de saisie automatique qui fournit des options de l’éditeur de requêtes.](../images/ui/query-editor/syntax-auto.png)

- **Saisie automatique de tableau et de champ :** commencez à saisir le nom du tableau auquel vous souhaitez appliquer `SELECT`, puis utilisez les touches fléchées pour accéder au tableau recherché et appuyez sur **Entrée**. Une fois le tableau sélectionné, la saisie automatique reconnaît les champs de ce tableau.

![L’entrée de l’éditeur de requêtes affiche les suggestions de noms de tableau déroulant.](../images/ui/query-editor/tables-auto.png)

### Bascule de configuration de l’interface utilisateur à saisie automatique {#auto-complete}

Le [!DNL Query Editor] suggère automatiquement des mots-clés SQL potentiels ainsi que des détails de tableau ou de colonne pour la requête au fur et à mesure que vous l’écrivez. La fonction de saisie automatique est activée par défaut et peut être désactivée ou activée à tout moment en sélectionnant l’option [!UICONTROL Saisie automatique de la syntaxe] basculez sur le coin supérieur droit de l’éditeur de requêtes.

Le paramètre de configuration de saisie automatique est défini par utilisateur et mémorisé pour les connexions consécutives de cet utilisateur.

![Éditeur de requêtes avec la bascule de saisie automatique de la syntaxe mise en surbrillance.](../images/ui/query-editor/auto-complete-toggle.png)

La désactivation de cette fonction empêche le traitement de plusieurs commandes de métadonnées et fournit des recommandations qui profitent généralement à la vitesse de l’auteur lors de la modification des requêtes.

Lorsque vous utilisez le bouton d’activation/désactivation pour activer la fonction de saisie semi-automatique, les suggestions recommandées pour les noms de tableau et de colonne ainsi que les mots-clés SQL deviennent disponibles après une courte pause. Un message de réussite dans la console sous l’éditeur de requêtes indique que la fonctionnalité est principale.

Si vous désactivez la fonction de saisie semi-automatique, une actualisation de page est nécessaire pour que cette dernière soit appliquée. Une boîte de dialogue de confirmation s’affiche avec trois options lorsque vous désactivez la fonction [!UICONTROL Saisie automatique de la syntaxe] bascule :

- [!UICONTROL Annuler]
- [!UICONTROL Enregistrer les modifications et actualiser]
- [!UICONTROL Actualiser sans enregistrer les modifications]

>[!IMPORTANT]
>
>Si vous écrivez ou modifiez une requête lors de la désactivation de cette fonction, vous devez enregistrer les modifications apportées à votre requête avant d’actualiser la page, sinon toute progression sera perdue.

![Boîte de dialogue de confirmation permettant de désactiver la fonction de saisie semi-automatique.](../images/ui/query-editor/confirmation-dialog.png)

Sélectionnez l’option appropriée pour désactiver la fonction de saisie semi-automatique.

### Détection des erreurs {#error-detection}

[!DNL Query Editor] valide automatiquement la requête au fur et à mesure que vous l’écrivez grâce à une validation SQL générique et une validation d’exécution spécifique. Si un trait de soulignement rouge apparaît sous la requête (comme illustré dans l’image ci-dessous), il indique une erreur dans la requête.

![La saisie de l’éditeur de requêtes affichant le style SQL souligné en rouge indique une erreur.](../images/ui/query-editor/syntax-error-highlight.png)

Lorsque des erreurs sont détectées, vous pouvez afficher les messages d’erreur spécifiques en survolant le code SQL avec la souris.

![Boîte de dialogue contenant un message d’erreur.](../images/ui/query-editor/linting-error.png)

### Détails de la requête {#query-details}

Sélectionnez un modèle enregistré dans la [!UICONTROL Modèles] pour l’afficher dans Query Editor. Le panneau Détails de la requête fournit des informations et des outils supplémentaires pour gérer la requête sélectionnée.

![Éditeur de requêtes avec le panneau des détails de la requête mis en surbrillance.](../images/ui/query-editor/query-details.png)

Ce panneau vous permet de générer un jeu de données de sortie directement à partir de l’interface utilisateur, de supprimer ou de nommer la requête affichée, et d’ajouter un planning à la requête.

Ce panneau présente également des métadonnées utiles, telles que la dernière fois où la requête a été modifiée et qui l’a modifiée, le cas échéant. Pour générer un jeu de données, sélectionnez **[!UICONTROL Jeu de données de sortie]**. La boîte de dialogue **[!UICONTROL Jeu de données de sortie]** s’affiche. Saisissez un nom et une description, puis sélectionnez **[!UICONTROL Exécuter la requête]**. Le nouveau jeu de données s’affiche dans l’onglet **[!UICONTROL Jeux de données]**[!DNL Query Service] de l’interface utilisateur de dans [!DNL Platform].

### Requêtes planifiées {#scheduled-queries}

>[!IMPORTANT]
>
>Vous trouverez ci-dessous une liste des limites relatives aux requêtes planifiées lors de l’utilisation de Query Editor. Elles ne s’appliquent pas au [!DNL Query Service] API :<br/>Vous pouvez uniquement ajouter un planning à une requête qui a déjà été créée, enregistrée et exécutée.<br/>You **cannot** ajoutez un planning à une requête paramétrée.<br/>Requêtes planifiées **cannot** contiennent un bloc anonyme.

Les planifications sont définies à partir de l’éditeur de requêtes. Toutefois, seules les requêtes qui ont déjà été enregistrées en tant que modèle peuvent être planifiées. Pour ajouter un planning à une requête, sélectionnez un modèle de requête dans l’une des options suivantes : [!UICONTROL Modèles] ou le [!UICONTROL Requêtes planifiées] pour accéder à l’éditeur de requêtes.

Pour savoir comment ajouter des plannings à l’aide de l’API, veuillez lire le [guide de point de terminaison des requêtes planifiées](../api/scheduled-queries.md).

Lorsqu’une requête enregistrée est accessible à partir de l’éditeur de requêtes, la variable [!UICONTROL Planifications] s’affiche sous le nom de la requête. Sélectionner **[!UICONTROL Planifications]**.

![Éditeur de requêtes avec l’onglet Planifications en surbrillance.](../images/ui/query-editor/schedules-tab.png)

L’espace de travail des planifications s’affiche. Sélectionner **[!UICONTROL Ajouter une planification]** pour créer un planning.

![Espace de travail Planification de l’éditeur de requêtes avec l’option Ajouter un planning mise en surbrillance.](../images/ui/query-editor/add-schedule.png)

La page Détails du planning s’affiche. Sur cette page, vous pouvez choisir la fréquence de la requête planifiée, la date de début et de fin, le jour de la semaine où la requête planifiée s’exécutera, ainsi que le jeu de données vers lequel exporter la requête.

![Le panneau Détails du planning est mis en surbrillance.](../images/ui/query-editor/schedule-details.png)

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

Après avoir confirmé tous ces détails, sélectionnez **[!UICONTROL Enregistrer]** pour créer un planning. L’espace de travail des planifications vous renvoie alors aux détails du nouveau planning, y compris l’identifiant du planning, le planning lui-même et le jeu de données de sortie du planning. Vous pouvez utiliser l’ID de planning pour rechercher plus d’informations sur les exécutions de la requête planifiée elle-même. Pour en savoir plus, veuillez lire le [guide des points de fin d’exécution de requête planifiée](../api/runs-scheduled-queries.md).

![Espace de travail des plannings avec la nouvelle planification mise en surbrillance.](../images/ui/query-editor/schedules-workspace.png)

#### Suppression ou désactivation d’un planning {#delete-schedule}

Vous pouvez supprimer ou désactiver une planification dans l’espace de travail des planifications. Vous devez sélectionner un modèle de requête à partir de l’un des [!UICONTROL Modèles] ou le [!UICONTROL Requêtes planifiées] pour accéder à l’éditeur de requêtes et sélectionnez **[!UICONTROL Planification]** pour accéder à l’espace de travail des plannings.

Sélectionnez un planning parmi les lignes des plannings disponibles. Vous pouvez activer ou désactiver la requête planifiée à l’aide du bouton d’activation.

>[!IMPORTANT]
>
>Vous devez désactiver le planning avant de pouvoir supprimer un planning pour une requête.

Sélectionner **[!UICONTROL Suppression d’un planning]** pour supprimer le planning désactivé.

![L’espace de travail Planifications avec l’option Désactiver la planification et Supprimer la planification est surligné.](../images/ui/query-editor/delete-schedule.png)

### Enregistrement des requêtes {#saving-queries}

Le [!DNL Query Editor] fournit une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Pour enregistrer une requête, sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit de [!DNL Query Editor]. Avant de pouvoir enregistrer une requête, vous devez lui donner un nom à l’aide du panneau **[!UICONTROL Détails]**.

>[!NOTE]
>
>Les requêtes nommées et enregistrées dans à l’aide de l’éditeur de requêtes sont disponibles sous forme de modèles dans le tableau de bord Requête . [!UICONTROL Modèles] . Voir [documentation sur les modèles](./query-templates.md) pour plus d’informations.

### Accès aux requêtes précédentes {#previous-queries}

Toutes les requêtes exécutées depuis [!DNL Query Editor] sont capturés dans le tableau Journal. Vous pouvez utiliser la fonctionnalité de recherche dans l’onglet **[!UICONTROL Journal]** pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans la **[!UICONTROL Modèles]** .

Si une requête a été planifiée, la variable [!UICONTROL Requêtes planifiées] offre une meilleure visibilité via l’interface utilisateur pour ces tâches de requête. Voir [documentation sur la surveillance des requêtes](../monitor-queries.md) pour plus d’informations.

>[!NOTE]
>
>Les requêtes non exécutées ne sont pas enregistrées dans le journal. Pour que la requête soit disponible dans [!DNL Query Service], il doit être exécuté ou enregistré dans [!DNL Query Editor].

## Exécution de requête à l’aide de Query Editor {#executing-queries}

Pour exécuter une requête dans [!DNL Query Editor], vous pouvez saisir du code SQL dans l’éditeur ou charger une requête précédente à partir de la fonction **[!UICONTROL Journal]** ou **[!UICONTROL Modèles]** et sélectionnez **Play**. L’état de l’exécution de la requête s’affiche dans l’onglet **[!UICONTROL Console]** ci-dessous et les données de sortie s’affichent dans l’onglet **[!UICONTROL Résultats]**.

### Console {#console}

La console fournit des informations sur l’état et le fonctionnement de [!DNL Query Service]. La console affiche l’état de la connexion à [!DNL Query Service], les opérations de requête en cours d’exécution et les messages d’erreur qui en résultent.

![Onglet Console de la console Query Editor.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l’exécution d’une requête. Elle n’affiche pas les erreurs de validation de requête avant l’exécution de la requête.

### Résultats de requête {#query-results}

Une fois la requête terminée, les résultats s’affichent dans la variable **[!UICONTROL Résultats]** en regard de l’onglet **[!UICONTROL Console]** . Cet affichage indique la sortie tabulaire de votre requête (jusqu’à 100 lignes). Il vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées, puis exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le [tutoriel sur la génération de jeux de données](./create-datasets.md) pour apprendre à générer un jeu de données à partir des résultats de requête dans [!DNL Query Editor].

![L’onglet Résultats de la console de l’éditeur de requêtes affiche les résultats d’une exécution de requête.](../images/ui/query-editor/query-results.png)

## Exécuter des requêtes avec [!DNL Query Service] tutoriel vidéo {#query-tutorial-video}

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. De plus, l’utilisation de propriétés individuelles dans un objet XDM, l’utilisation de fonctions définies par l’Adobe et l’utilisation de CREATE TABLE AS SELECT (CTAS) sont illustrées.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Étapes suivantes

Maintenant que vous savez quelles fonctionnalités sont disponibles dans [!DNL Query Editor] et comment naviguer dans l’application, vous pouvez commencer à créer vos propres requêtes directement dans [!DNL Platform]. Pour plus d’informations sur l’exécution de requêtes SQL par rapport à des jeux de données dans [!DNL Data Lake], reportez-vous au guide sur la [exécution de requêtes](../best-practices/writing-queries.md).
