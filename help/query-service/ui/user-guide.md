---
keywords: Experience Platform;accueil;rubriques populaires;Query editor;query editor;Query service;query service;
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Editor
description: Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service. Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '2100'
ht-degree: 98%

---

# Guide de l’interface utilisateur de [!DNL Query Editor]

[!DNL Query Editor] est un outil interactif fourni par le [!DNL Query Service] d’Adobe Experience Platform. Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’[!DNL Experience Platform]. [!DNL Query Editor] prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans [!DNL Experience Platform].

Pour plus d’informations sur les concepts et les fonctionnalités de [!DNL Query Service], consultez la [Présentation de Query Service](../home.md). Pour en savoir plus sur la navigation dans l’interface utilisateur de Query Service sur [!DNL Platform], consultez la [Présentation de l’interface utilisateur de Query Service](./overview.md).

## Prise en main {#getting-started}

[!DNL Query Editor] offre une exécution flexible des requêtes en se connectant à [!DNL Query Service], et ces requêtes seront uniquement exécutées tant que cette connexion sera active.

### Connexion à [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] ne prend que quelques secondes pour l’initialisation et, une fois ouvert, se connecte à [!DNL Query Service]. La console vous indique qu’il est connecté, comme illustré ci-dessous. Si vous tentez d’exécuter une requête avant que l’éditeur ne soit connecté, l’exécution est retardée jusqu’à ce que la connexion soit établie.

![Sortie de console du Query Editor lors de la connexion initiale.](../images/ui/query-editor/connect.png)

### Exécution des requêtes depuis [!DNL Query Editor] {#run-a-query}

Dans [!DNL Query Editor], les requêtes sont exécutées de manière interactive. Cela signifie que la requête sera annulée si vous fermez le navigateur ou quittez l’éditeur. Cela concerne également les requêtes visant à générer des jeux de données à partir de sorties de requête.

## Création de requête à l’aide du [!DNL Query Editor] {#query-authoring}

Avec [!DNL Query Editor], vous pouvez écrire, exécuter et enregistrer des requêtes de données d’expérience client. Toutes les requêtes enregistrées ou exécutées dans [!DNL Query Editor] sont accessibles à tous les utilisateurs de votre organisation bénéficiant d’un accès à [!DNL Query Service].

### Accéder à [!DNL Query Editor] {#accessing-query-editor}

Pour ouvrir l’espace de travail [!DNL Query Service], cliquez sur **[!UICONTROL Requêtes]** dans le menu de navigation à gauche de l’interface utilisateur d’[!DNL Experience Platform]. Cliquez ensuite sur **[!UICONTROL Créer une requête]** dans la partie supérieure droite de l’écran pour commencer à écrire des requêtes. Ce lien est disponible depuis n’importe quelle page de l’espace de travail [!DNL Query Service].

![Onglet Présentation de l’espace de travail Requêtes avec l’option Créer une requête mise en surbrillance.](../images/ui/query-editor/create-query.png)

### Rédaction de requêtes {#writing-queries}

[!UICONTROL Query Editor est organisé de façon à rendre l’écriture de requête aussi facile que possible. ] La copie d’écran ci-dessous présente l’affichage de l’éditeur dans l’interface utilisateur. Le champ d’entrée SQL et le bouton **Lire** sont mis en surbrillance.

![Query Editor avec le champ d’entrée SQL et le bouton Lire en surbrillance.](../images/ui/query-editor/editor.png)

Pour réduire le temps de développement, nous vous recommandons de développer vos requêtes en fixant des limites sur les lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête produit la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT`, afin de générer un jeu de données avec la sortie.

### Outils d’écriture dans le [!DNL Query Editor] {#writing-tools}

- **Mise en surbrillance automatique de la syntaxe :** facilite la lecture et l’organisation SQL.

![Instruction SQL dans le Query Editor présentant une mise en surbrillance des couleurs de syntaxe.](../images/ui/query-editor/syntax-highlight.png)

- **Saisie automatique de mots-clés SQL :** commencez à saisir votre requête, puis utilisez les touches fléchées pour accéder au terme souhaité et appuyez sur **Entrée**.

![Quelques caractères SQL avec le menu déroulant de saisie automatique qui fournit des options du Query Editor.](../images/ui/query-editor/syntax-auto.png)

- **Saisie automatique de tableau et de champ :** commencez à saisir le nom du tableau auquel vous souhaitez appliquer `SELECT`, puis utilisez les touches fléchées pour accéder au tableau recherché et appuyez sur **Entrée**. Une fois le tableau sélectionné, la saisie automatique reconnaît les champs de ce tableau.

![Entrée du Query Editor affichant les suggestions de noms de tableau déroulant.](../images/ui/query-editor/tables-auto.png)

### (Version limitée) Bascule de configuration de l’interface utilisateur à saisie automatique {#auto-complete}

>[!IMPORTANT]
>
>Le bouton de configuration de l’interface utilisateur à saisie automatique est actuellement disponible dans une version limitée et n’est pas disponible pour tous les clients.

Le [!DNL Query Editor] suggère automatiquement des mots-clés SQL potentiels ainsi que des détails de tableau ou de colonne pour la requête au fur et à mesure que vous l’écrivez. La fonction de saisie automatique est activée par défaut et peut être désactivée ou activée à tout moment en cliquant sur le bouton (bascule) [!UICONTROL Saisie automatique de la syntaxe] dans la partie supérieure droite du Query Editor.

Le paramètre de configuration de saisie automatique est défini par utilisateur et mémorisé pour les connexions consécutives de l’utilisateur.

![Query Editor avec le bouton (bascule) de saisie automatique de la syntaxe mis en surbrillance.](../images/ui/query-editor/auto-complete-toggle.png)

La désactivation de cette fonction arrête le traitement de plusieurs commandes de métadonnées et la suggestion de recommandations qui accélère généralement la vitesse de l’auteur lors de la modification des requêtes.

Lorsque vous cliquez sur le bouton (bascule) pour activer la fonction de saisie automatique, les suggestions recommandées pour les noms de tableau et de colonne ainsi que les mots-clés SQL deviennent disponibles après une courte pause. Un message de réussite dans la console sous le Query Editor indique que la fonctionnalité est activée.

Si vous désactivez la fonction de saisie automatique, une actualisation de page est nécessaire pour que cette action soit appliquée. Une boîte de dialogue de confirmation s’affiche avec trois options lorsque vous désactivez le bouton de la [!UICONTROL Saisie automatique de la syntaxe] :

- [!UICONTROL Annuler]
- [!UICONTROL Enregistrer les modifications et actualiser]
- [!UICONTROL Actualiser sans enregistrer les modifications]

>[!IMPORTANT]
>
>Si vous écrivez ou modifiez une requête lors de la désactivation de cette fonction, vous devez enregistrer les modifications apportées à votre requête avant d’actualiser la page, sinon toute progression sera perdue.

![Boîte de dialogue de confirmation permettant de désactiver la fonction de saisie automatique.](../images/ui/query-editor/confirmation-dialog.png)

Sélectionnez l’option appropriée pour désactiver la fonction de saisie automatique.

### Détection des erreurs {#error-detection}

[!DNL Query Editor] valide automatiquement la requête au fur et à mesure que vous l’écrivez grâce à une validation SQL générique et une validation d’exécution spécifique. Si un trait de soulignement rouge apparaît sous la requête (comme illustré dans l’image ci-dessous), il indique une erreur dans la requête.

![Entrée de Query Editor affichant le style SQL souligné en rouge pour indiquer une erreur.](../images/ui/query-editor/syntax-error-highlight.png)

Lorsque des erreurs sont détectées, vous pouvez afficher les messages d’erreur spécifiques en survolant le code SQL avec la souris.

![Boîte de dialogue contenant un message d’erreur.](../images/ui/query-editor/linting-error.png)

### Détails de la requête {#query-details}

Sélectionnez un modèle enregistré dans l’onglet [!UICONTROL Modèles] pour l’afficher dans Query Editor. Le panneau des détails de la requête fournit plus d’informations et d’outils pour gérer la requête sélectionnée.

![Query Editor avec le panneau des détails de la requête mis en surbrillance.](../images/ui/query-editor/query-details.png)

Ce panneau vous permet de générer un jeu de données de sortie directement à partir de l’interface utilisateur, de supprimer ou de nommer la requête affichée, et d’ajouter un planning à la requête.

Ce panneau présente également des métadonnées utiles, telles que la dernière fois où la requête a été modifiée et qui l’a modifiée, le cas échéant. Pour générer un jeu de données, sélectionnez **[!UICONTROL Jeu de données de sortie]**. La boîte de dialogue **[!UICONTROL Jeu de données de sortie]** s’affiche. Saisissez un nom et une description, puis sélectionnez **[!UICONTROL Exécuter la requête]**. Le nouveau jeu de données s’affiche dans l’onglet **[!UICONTROL Jeux de données]** de l’interface utilisateur [!DNL Query Service] dans [!DNL Platform].

### Requêtes planifiées {#scheduled-queries}

>[!IMPORTANT]
>
>Vous trouverez ci-dessous une liste des limitations des requêtes planifiées lorsque vous utilisez l’éditeur de requêtes. Elles ne s’appliquent pas à l’API [!DNL Query Service] :<br/>Vous pouvez uniquement ajouter un planning à une requête qui a déjà été créée, enregistrée et exécutée.<br/>Vous **ne pouvez pas** ajouter un planning à une requête paramétrée.<br/>Les requêtes planifiées **ne peuvent pas** contenir un bloc anonyme.

Les plannings sont définis à partir du Query Editor. Toutefois, seules les requêtes qui ont déjà été enregistrées en tant que modèle peuvent être planifiées. Pour ajouter un planning à une requête, sélectionnez un modèle de requête dans l’onglet [!UICONTROL Modèles] ou [!UICONTROL Requêtes planifiées] pour accéder au Query Editor.

Pour savoir comment ajouter des plannings à l’aide de l’API, veuillez lire le [guide de point d’entrée des requêtes planifiées](../api/scheduled-queries.md).

Lorsqu’une requête enregistrée est accessible à partir du Query Editor, l’onglet [!UICONTROL Plannings] s’affiche sous le nom de la requête. Sélectionnez **[!UICONTROL Plannings]**.

![Query Editor avec l’onglet Plannings en surbrillance.](../images/ui/query-editor/schedules-tab.png)

L’espace de travail des plannings s’affiche. Sélectionnez **[!UICONTROL Ajouter un planning]** pour créer un planning.

![Espace de travail Planning du Query Editor avec l’option Ajouter un planning mise en surbrillance.](../images/ui/query-editor/add-schedule.png)

La page Détails du planning s’affiche. Sur cette page, vous pouvez choisir la fréquence de la requête planifiée, la date de début et de fin, le jour de la semaine où la requête planifiée sera exécutée, ainsi que le jeu de données vers lequel exporter la requête.

![Le panneau Détails du planning est mis en surbrillance.](../images/ui/query-editor/schedule-details.png)

Vous pouvez choisir les options suivantes pour **[!UICONTROL Fréquence]** :

- **[!UICONTROL Horaire]** : la requête planifiée s’exécute toutes les heures pour la période que vous avez sélectionnée.
- **[!UICONTROL Quotidien]** : la requête planifiée s’exécute tous les X jours à l’heure et à la période que vous avez sélectionnées. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.
- **[!UICONTROL Hebdomadaire]** : la requête sélectionnée sera exécutée aux jours de la semaine, à l’heure et à la période que vous avez sélectionnés. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.
- **[!UICONTROL Mensuel]** : la requête sélectionnée s’exécute tous les mois au jour, à l’heure et à la période que vous avez sélectionnés. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.
- **[!UICONTROL Annuel]** : la requête sélectionnée s’exécute chaque année au jour, au mois, à l’heure et à la période que vous avez sélectionnés. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.

Pour le jeu de données, vous avez la possibilité d’en utiliser un existant ou d’en créer un nouveau.

>[!IMPORTANT]
>
> Puisque vous utilisez un jeu de données existant ou que vous en créez un nouveau, vous n’avez **pas** besoin d’inclure `INSERT INTO` ou `CREATE TABLE AS SELECT` dans le cadre de la requête, puisque les jeux de données sont déjà définis. L’inclusion de `INSERT INTO` ou `CREATE TABLE AS SELECT` dans le cadre de vos requêtes planifiées entraînera une erreur.

Après avoir confirmé tous ces détails, sélectionnez **[!UICONTROL Enregistrer]** pour créer un planning. L’espace de travail des plannings affiche les détails du planning nouvellement créé, y compris l’ID du planning, le planning lui-même et le jeu de données de sortie du planning. Vous pouvez utiliser l’ID de planning pour rechercher plus d’informations sur les exécutions de la requête planifiée elle-même. Pour en savoir plus, veuillez lire le [guide des points d’entrée d’exécution de requête planifiée](../api/runs-scheduled-queries.md).

![Espace de travail des plannings avec le nouveau planning mis en surbrillance.](../images/ui/query-editor/schedules-workspace.png)

#### Supprimer ou désactiver un planning {#delete-schedule}

Vous pouvez supprimer ou désactiver un planning dans l’espace de travail des plannings. Vous devez sélectionner un modèle de requête à partir de l’onglet [!UICONTROL Modèles] ou de l’onglet [!UICONTROL Requêtes planifiées] pour accéder à l’éditeur de requêtes et sélectionner **[!UICONTROL Planning]** pour accéder à l’espace de travail des plannings.

Sélectionnez un planning dans les lignes des plannings disponibles. Vous pouvez activer ou désactiver la requête planifiée à l’aide du bouton d’activation.

>[!IMPORTANT]
>
>Vous devez désactiver le planning avant de pouvoir supprimer un planning pour une requête.

Sélectionnez **[!UICONTROL Supprimer un planning]** pour supprimer le planning désactivé.

![L’espace de travail des plannings avec l’option Désactiver le planning et Supprimer le planning est en surbrillance.](../images/ui/query-editor/delete-schedule.png)

### Enregistrement des requêtes {#saving-queries}

Le [!DNL Query Editor] offre une fonction de sauvegarde qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Pour enregistrer une requête, sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit du [!DNL Query Editor]. Avant de pouvoir enregistrer une requête, vous devez lui donner un nom à l’aide du panneau **[!UICONTROL Détails sur la requête]**.

>[!NOTE]
>
>Les requêtes nommées et enregistrées dans à l’aide du Query Editor sont disponibles sous forme de modèles dans l’onglet [!UICONTROL Modèles] du tableau de bord Requête. Pour plus d’informations, consultez la [documentation sur les modèles](./query-templates.md).

### Accès aux requêtes précédentes {#previous-queries}

Toutes les requêtes exécutées à partir du [!DNL Query Editor] sont capturées dans le tableau Journal. Vous pouvez utiliser la fonctionnalité de recherche dans l’onglet **[!UICONTROL Journal]** pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans l’onglet **[!UICONTROL Modèles]**.

Si une requête a été planifiée, alors l’onglet [!UICONTROL Requêtes planifiées] offre une meilleure visibilité à travers l’interface utilisateur pour ces tâches de requête. Pour plus d’informations, consultez la [documentation sur la surveillance des requêtes](../monitor-queries.md).

>[!NOTE]
>
>Les requêtes non exécutées ne sont pas enregistrées dans le journal. Pour que la requête soit disponible dans [!DNL Query Service], elle doit être exécutée ou enregistrée dans [!DNL Query Editor].

## Exécution de requête à l’aide de Query Editor {#executing-queries}

Pour exécuter une requête dans [!DNL Query Editor], vous pouvez saisir le langage SQL dans l’éditeur ou charger une requête précédente depuis l’onglet **[!UICONTROL Journal]** ou **[!UICONTROL Modèles]**, et sélectionner **Lire**. L’état de l’exécution de la requête s’affiche dans l’onglet **[!UICONTROL Console]** ci-dessous et les données de sortie s’affichent dans l’onglet **[!UICONTROL Résultats]**.

### Console {#console}

La console fournit des informations sur le statut et le fonctionnement de [!DNL Query Service]. La console affiche le statut de la connexion à [!DNL Query Service], les opérations des requêtes en cours d’exécution et tout message d’erreur résultant de ces requêtes.

![L’onglet Console de la console du Query Editor.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l’exécution d’une requête. Elle n’affiche pas les erreurs de validation de requête avant l’exécution de la requête.

### Résultats de requête {#query-results}

Une fois une requête terminée, les résultats sont affichés dans l’onglet **[!UICONTROL Résultats]**, en regard de l’onglet **[!UICONTROL Console]**. Cet affichage indique la sortie tabulaire de votre requête (jusqu’à 100 lignes). Il vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées, puis exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le [tutoriel sur la génération de jeux de données](./create-datasets.md) pour apprendre à générer un jeu de données à partir des résultats de requête dans [!DNL Query Editor].

![L’onglet Résultats de la console du Query Editor affiche les résultats de l’exécution d’une requête.](../images/ui/query-editor/query-results.png)

## Exécuter des requêtes avec le tutoriel vidéo sur [!DNL Query Service] {#query-tutorial-video}

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. En outre, l’utilisation de propriétés individuelles dans un objet XDM, l’utilisation de fonctions définies par Adobe et l’utilisation de CREATE TABLE AS SELECT (CTAS) sont illustrées.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Étapes suivantes

Maintenant que vous connaissez les fonctionnalités disponibles dans le [!DNL Query Editor] et que vous savez naviguer dans l’application, vous pouvez commencer à créer vos requêtes directement sur [!DNL Platform]. Pour plus d’informations sur l’exécution de requêtes SQL par rapport aux jeux de données dans [!DNL Data Lake], consultez le guide sur ’[exécution de requêtes](../best-practices/writing-queries.md).
