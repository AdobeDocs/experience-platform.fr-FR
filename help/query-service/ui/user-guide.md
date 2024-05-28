---
keywords: Experience Platform;accueil;rubriques populaires;Query editor;query editor;Query service;query service;
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Editor
description: Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service. Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 45eab8f894819eea36465ea0b8f3f3dd8f91fbe0
workflow-type: tm+mt
source-wordcount: '2432'
ht-degree: 31%

---

# Guide de l’interface utilisateur de Query Editor

>[!NOTE]
>
>L’ancien éditeur a été abandonné le 24 mai 2024. Il n’est plus accessible à l’utilisation. Vous pouvez désormais utiliser la variable [Éditeur de requêtes amélioré](#enhanced-editor-toggle) pour écrire, valider et exécuter vos requêtes

Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service qui vous permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans les [!DNL Experience Platform] de l’interface utilisateur. Query Editor prend en charge le développement de requêtes à des fins d’analyse et d’exploration de données, et vous permet d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner des jeux de données dans [!DNL Experience Platform].

Pour plus d’informations sur les concepts et les fonctionnalités de Query Service, consultez la [Présentation de Query Service](../home.md). Pour en savoir plus sur la navigation dans l’interface utilisateur de Query Service sur [!DNL Platform], consultez la [Présentation de l’interface utilisateur de Query Service](./overview.md).

## Prise en main {#getting-started}

Query Editor permet une exécution flexible des requêtes en se connectant à Query Service. Les requêtes ne s’exécutent que lorsque cette connexion est active.

## Accès à Query Editor {#accessing-query-editor}

Dans le [!DNL Experience Platform] Interface utilisateur, sélectionnez **[!UICONTROL Requêtes]** dans le menu de navigation de gauche pour ouvrir l’espace de travail Query Service. Ensuite, pour commencer à écrire des requêtes, sélectionnez **[!UICONTROL Créer une requête]** en haut à droite de l’écran. Ce lien est disponible depuis n’importe quelle page de l’espace de travail Query Service.

![Onglet Présentation de l’espace de travail Requêtes avec l’option Créer une requête mise en surbrillance.](../images/ui/query-editor/create-query.png)

### Connexion à Query Service {#connecting-to-query-service}

L’éditeur de requêtes prend quelques secondes pour s’initialiser et se connecter à Query Service à son ouverture. La console vous indique qu’il est connecté, comme illustré ci-dessous. Si vous tentez d’exécuter une requête avant que l’éditeur ne soit connecté, l’exécution est retardée jusqu’à ce que la connexion soit établie.

![Sortie de console du Query Editor lors de la connexion initiale.](../images/ui/query-editor/connect.png)

### Exécution des requêtes depuis Query Editor {#run-a-query}

Les requêtes exécutées à partir de Query Editor s’exécutent de manière interactive, ce qui signifie que si vous fermez le navigateur ou quittez le navigateur, la requête est annulée. Il en va de même pour les requêtes effectuées pour générer des jeux de données à partir de sorties de requête.

## Création de requêtes à l’aide de l’éditeur de requêtes amélioré {#query-authoring}

>[!NOTE]
>
>L’ancien éditeur a été abandonné le 24 mai 2024. Il n’est plus accessible à l’utilisation. Vous pouvez désormais utiliser l’éditeur de requêtes amélioré pour écrire, valider et exécuter vos requêtes.

Avec Query Editor, vous pouvez écrire, exécuter et enregistrer des requêtes de données d’expérience client. Toutes les requêtes exécutées ou enregistrées dans Query Editor sont disponibles pour tous les utilisateurs de votre entreprise ayant accès à Query Service.

### Paramètres {#settings}

Une icône de paramètres au-dessus du champ de saisie de l’éditeur de requêtes comprend des options pour activer/désactiver le thème sombre ou désactiver/activer la saisie automatique.

>[!TIP]
>
>Vous pouvez [!UICONTROL Désactivation de la saisie automatique de la syntaxe] lors de la création d’une requête sans perdre la progression.

Pour activer les thèmes sombres ou lumineux, sélectionnez l’icône de paramètres (![Icône Paramètres .](../images/ui/query-editor/settings-icon.png)) suivi de l’option du menu déroulant qui s’affiche.

![L’éditeur de requêtes avec l’icône de paramètres et l’option de menu déroulant Activer le thème sombre sont mises en surbrillance.](../images/ui/query-editor/query-editor-settings.png)

#### Saisie automatique {#auto-complete}

L’éditeur de requêtes propose automatiquement des mots-clés SQL potentiels, ainsi que des détails de tableau ou de colonne pour la requête au fur et à mesure que vous l’écrivez. La fonction de saisie automatique est activée par défaut et peut être désactivée ou activée à tout moment dans les paramètres de l’éditeur de requêtes.

Le paramètre de configuration de saisie automatique est défini par utilisateur et mémorisé pour les connexions consécutives de cet utilisateur. La désactivation de cette fonction arrête le traitement de plusieurs commandes de métadonnées et la suggestion de recommandations qui accélère généralement la vitesse de l’auteur lors de la modification des requêtes.

<!-- Currently editing the auto complete setting info. -->



### Exécution de plusieurs requêtes séquentielles {#execute-multiple-sequential-queries}

Utilisez l’éditeur de requêtes amélioré pour écrire plusieurs requêtes et exécuter toutes les requêtes de manière séquentielle. L’exécution de plusieurs requêtes dans une séquence génère chacune une entrée de journal. Toutefois, seuls les résultats de la première requête s’affichent dans la console de l’éditeur de requêtes. Vérifiez le journal des requêtes si vous devez résoudre ou confirmer les requêtes qui ont été exécutées. Voir [documentation sur les journaux de requête](./query-logs.md) pour plus d’informations.

>[!NOTE]
> 
>Si une requête CTAS est exécutée après la première requête dans Query Editor, une table est toujours créée, mais il n’y a aucune sortie dans la console Query Editor.

### Exécuter la requête sélectionnée {#execute-selected-query}

Si vous avez écrit plusieurs requêtes mais que vous ne devez exécuter qu’une seule requête, vous pouvez mettre en surbrillance la requête choisie et sélectionner l’événement
[!UICONTROL Exécuter la requête sélectionnée] Icône Cette icône est désactivée par défaut jusqu’à ce que vous sélectionniez la syntaxe de la requête dans l’éditeur.

![L’éditeur de requêtes avec la variable [!UICONTROL Exécuter la requête sélectionnée] en surbrillance.](../images/ui/query-editor/run-selected-query.png)

### Annuler la session de l’éditeur de requêtes {#cancel-query}

Contrôlez l’exécution des requêtes et améliorez votre productivité en annulant les requêtes longues. Cette action efface l’éditeur de requêtes lors d’une exécution de requête. Gardez à l’esprit que la requête continue de s’exécuter en arrière-plan. S’il s’agit d’une requête CTAS, elle génère toujours un jeu de données de sortie. Pour annuler l’exécution dans l’éditeur et continuer à composer une instruction SQL, sélectionnez **[!UICONTROL Annuler la requête]** après l’exécution d’une requête.

![L’éditeur de requêtes avec [!UICONTROL Annuler la requête] surlignée.](../images/ui/query-editor/cancel-query-run.png)

Une boîte de dialogue de confirmation s’affiche. Sélectionner **[!UICONTROL Confirmer]** pour annuler la requête exécutée.

![La boîte de dialogue de confirmation de requête Annuler avec l’option Confirmer est mise en surbrillance.](../images/ui/query-editor/cancel-query-confirmation-dialog.png)

### Nombre de résultats {#result-count}

L’éditeur de requêtes dispose d’une sortie de ligne maximale de 50 000 lignes. Vous pouvez choisir le nombre de lignes affichées simultanément dans la console de l’éditeur de requêtes. Pour modifier le nombre de lignes affichées dans la console, sélectionnez l’option **[!UICONTROL Résultats count]** et sélectionnez l’une des options 50, 100, 150, 300 et 500.

![La liste déroulante Query Editor avec le nombre de résultats est mise en surbrillance.](../images/ui/query-editor/result-count.png)

## Rédaction de requêtes {#writing-queries}

[!UICONTROL Query Editor est organisé de façon à rendre l’écriture de requête aussi facile que possible. ] La copie d’écran ci-dessous présente l’affichage de l’éditeur dans l’interface utilisateur. Le champ d’entrée SQL et le bouton **Lire** sont mis en surbrillance.

![Query Editor avec le champ d’entrée SQL et le bouton Lire en surbrillance.](../images/ui/query-editor/editor.png)

Pour réduire le temps de développement, il est recommandé de développer vos requêtes avec des limites sur le nombre de lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête produit la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT`, afin de générer un jeu de données avec la sortie.

## Outils d’écriture dans Query Editor {#writing-tools}

- **Mise en surbrillance automatique de la syntaxe :** facilite la lecture et l’organisation SQL.

![Instruction SQL dans le Query Editor présentant une mise en surbrillance des couleurs de syntaxe.](../images/ui/query-editor/syntax-highlight.png)

- **Saisie automatique de mots-clés SQL :** commencez à saisir votre requête, puis utilisez les touches fléchées pour accéder au terme souhaité et appuyez sur **Entrée**.

![Quelques caractères SQL avec le menu déroulant de saisie automatique qui fournit des options du Query Editor.](../images/ui/query-editor/syntax-auto.png)

- **Saisie automatique de tableau et de champ :** commencez à saisir le nom du tableau auquel vous souhaitez appliquer `SELECT`, puis utilisez les touches fléchées pour accéder au tableau recherché et appuyez sur **Entrée**. Une fois qu’un tableau est sélectionné, la saisie automatique reconnaît les champs de ce tableau.

![Entrée du Query Editor affichant les suggestions de noms de tableau déroulant.](../images/ui/query-editor/tables-auto.png)

### Mettre le texte en forme {#format-text}

La variable [!UICONTROL Texte du format] rend votre requête plus lisible en ajoutant un style de syntaxe normalisé. Sélectionner **[!UICONTROL Texte du format]** pour normaliser tout le texte dans l’éditeur de requêtes.

>[!NOTE]
>
>La variable [!UICONTROL Texte du format] ne fonctionne pas avec les blocs anonymes. Pour savoir comment chaîner séquentiellement une ou plusieurs instructions SQL, reportez-vous à la section [documentation bloquée anonyme](../key-concepts/anonymous-block.md).

![L’éditeur de requêtes avec [!UICONTROL Texte du format] et les instructions SQL mises en surbrillance.](../images/ui/query-editor/format-text.png)

<!-- ### Undo text {#undo-text}

If you format your SQL in the Query Editor, you can undo the formatting applied by the [!UICONTROL Format text] feature. To return your SQL back to its original form, select **[!UICONTROL Undo text]**.

![The Query Editor with [!UICONTROL Undo text] and the SQL statements highlighted.](../images/ui/query-editor/undo-text.png) -->

### Copier le SQL {#copy-sql}

Sélectionnez l’icône Copier pour copier SQL à partir de Query Editor dans le presse-papiers. Cette fonctionnalité de copie est disponible à la fois pour les modèles de requête et les requêtes nouvellement créées dans Query Editor.

![L&#39;espace de travail Requêtes avec un exemple de modèle de requête avec l&#39;icône de copie mise en surbrillance.](../images/ui/query-editor/copy-sql.png)

### Détails de la requête {#query-details}

Pour afficher une requête dans l’éditeur de requêtes, sélectionnez un modèle enregistré dans le [!UICONTROL Modèles] . Le panneau Détails de la requête fournit des informations et des outils supplémentaires pour gérer la requête sélectionnée. Il affiche également des métadonnées utiles telles que la dernière fois où la requête a été modifiée et qui l’a modifiée, le cas échéant.

>[!NOTE]
>
>La variable [!UICONTROL Afficher le planning], [!UICONTROL Ajouter un planning] et [!UICONTROL Supprimer la requête] Les options ne sont disponibles qu’après l’enregistrement de la requête en tant que modèle. La variable [!UICONTROL Ajouter un planning] Cette option vous permet d’accéder directement au créateur de planification à partir de l’éditeur de requêtes. La variable [!UICONTROL Afficher le planning] permet d’accéder directement à l’inventaire des planifications pour cette requête. Consultez la documentation sur les plannings de requête pour savoir comment [création de calendriers de requête dans l’interface utilisateur](./query-schedules.md#create-schedule).

![Query Editor avec le panneau des détails de la requête mis en surbrillance.](../images/ui/query-editor/query-details.png)

Dans le panneau Détails, vous pouvez générer un jeu de données de sortie directement à partir de l’interface utilisateur, supprimer ou nommer la requête affichée, afficher le planning d’exécution de la requête et ajouter la requête à un planning.

Pour générer un jeu de données de sortie, sélectionnez **[!UICONTROL Exécuter comme CTAS]**. La variable **[!UICONTROL Entrer les détails du jeu de données de sortie]** s’affiche. Saisissez un nom et une description, puis sélectionnez **[!UICONTROL Exécuter comme CTAS]**. Le nouveau jeu de données s’affiche dans la variable **[!UICONTROL Jeux de données]** Onglet Parcourir . Voir [la documentation d’affichage des jeux de données](../../catalog/datasets/user-guide.md#view-datasets) pour en savoir plus sur les jeux de données disponibles pour votre organisation.

>[!NOTE]
>
>La variable [!UICONTROL Exécuter comme CTAS] n’est disponible que si la requête contient **not** a été planifié.

![La variable [!UICONTROL Entrer les détails du jeu de données de sortie] boîte de dialogue.](../images/ui/query-editor/output-dataset-details.png)

Après avoir exécuté la variable **[!UICONTROL Exécuter comme CTAS]** , un message de confirmation s’affiche pour vous informer de l’action réussie. Ce message contextuel contient un lien qui permet d’accéder facilement à l’espace de travail des logs de requête. Voir [documentation sur les journaux de requête](./query-logs.md) pour plus d’informations sur les logs de requête.

### Enregistrement des requêtes {#saving-queries}

Query Editor fournit une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Pour enregistrer une requête, sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit de Query Editor. Avant de pouvoir enregistrer une requête, vous devez lui donner un nom à l’aide du panneau **[!UICONTROL Détails sur la requête]**.

>[!NOTE]
>
>Les requêtes nommées et enregistrées dans à l’aide du Query Editor sont disponibles sous forme de modèles dans l’onglet [!UICONTROL Modèles] du tableau de bord Requête. Pour plus d’informations, consultez la [documentation sur les modèles](./query-templates.md).

Lorsque vous enregistrez une requête dans l’éditeur de requêtes, un message de confirmation s’affiche pour vous informer de la réussite de l’action. Ce message contextuel contient un lien qui permet d’accéder facilement à l’espace de travail de planification des requêtes. Voir [documentation sur les requêtes de planification](./query-schedules.md) pour savoir comment exécuter des requêtes sur une cadence personnalisée.

### Requêtes planifiées {#scheduled-queries}

Les requêtes qui ont été enregistrées en tant que modèle peuvent être planifiées à partir de l’éditeur de requêtes. La planification des requêtes vous permet d’automatiser les exécutions de requête sur une cadence personnalisée. Vous pouvez planifier des requêtes en fonction de la fréquence, de la date et de l’heure, et choisir également un jeu de données de sortie pour vos résultats, si nécessaire. Les plannings de requête peuvent également être désactivés ou supprimés via l’interface utilisateur.

Les planifications sont définies dans l’éditeur de requêtes. Lorsque vous utilisez l’éditeur de requêtes, vous ne pouvez ajouter qu’un planning à une requête qui a déjà été créée et enregistrée. La même limitation ne s’applique pas à l’API Query Service.

>[!NOTE]
>
>Les requêtes planifiées qui échouent lors de dix exécutions consécutives sont automatiquement placées dans une [!UICONTROL Quarantiné] statut. Une requête avec ce statut nécessite votre intervention avant toute autre exécution. Voir [requêtes mises en quarantaine](./monitor-queries.md#quarantined-queries) pour plus d’informations.

Consultez la documentation sur les plannings de requête pour savoir comment [création de calendriers de requête dans l’interface utilisateur](./query-schedules.md). Pour savoir comment ajouter des plannings à l’aide de l’API, vous pouvez également lire le [guide de point de terminaison des requêtes planifiées](../api/scheduled-queries.md).

Toutes les requêtes planifiées sont ajoutées à la liste dans la variable [!UICONTROL Requêtes planifiées] . Depuis cet espace de travail, vous pouvez surveiller l’état de toutes les tâches de requête planifiées via l’interface utilisateur. Sur le [!UICONTROL Requêtes planifiées] , vous pouvez trouver des informations importantes sur les exécutions de requête et vous abonner aux alertes. Les informations disponibles incluent l’état, les détails de planification et les messages/codes d’erreur en cas d’échec de l’exécution. Voir [Surveiller le document des requêtes planifiées](./monitor-queries.md) pour plus d’informations.


### Accès aux requêtes précédentes {#previous-queries}

Toutes les requêtes exécutées depuis Query Editor sont capturées dans le tableau Journal. Vous pouvez utiliser la fonctionnalité de recherche dans l’onglet **[!UICONTROL Journal]** pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans l’onglet **[!UICONTROL Modèles]**.

Si une requête a été planifiée, alors l’onglet [!UICONTROL Requêtes planifiées] offre une meilleure visibilité à travers l’interface utilisateur pour ces tâches de requête. Pour plus d’informations, consultez la [documentation sur la surveillance des requêtes](./monitor-queries.md).

>[!NOTE]
>
>Les requêtes non exécutées ne sont pas enregistrées dans le journal. Pour que la requête soit disponible dans Query Service, elle doit être exécutée ou enregistrée dans Query Editor.

## Exécution de requête à l’aide de Query Editor {#executing-queries}

Pour exécuter une requête dans Query Editor, vous pouvez saisir du code SQL dans l’éditeur ou charger une requête précédente à partir du **[!UICONTROL Journal]** ou **[!UICONTROL Modèles]** et sélectionnez **Play**. L’état de l’exécution de la requête s’affiche dans l’onglet **[!UICONTROL Console]** ci-dessous et les données de sortie s’affichent dans l’onglet **[!UICONTROL Résultats]**.

### Console {#console}

La console fournit des informations sur l’état et le fonctionnement de Query Service. La console affiche l’état de la connexion à Query Service, les opérations des requêtes en cours d’exécution et tout message d’erreur résultant de ces requêtes.

![L’onglet Console de la console du Query Editor.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l&#39;exécution d&#39;une requête. Elle n’affiche pas les erreurs de validation de requête qui se produisent avant l’exécution d’une requête.

### Résultats de requête {#query-results}

Une fois une requête terminée, les résultats sont affichés dans l’onglet **[!UICONTROL Résultats]**, en regard de l’onglet **[!UICONTROL Console]**. Cette vue affiche la sortie tabulaire de votre requête, qui affiche entre 50 et 500 lignes de résultats selon le choix que vous avez effectué. [comptage des résultats](#result-count). Il vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées, puis exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le [tutoriel sur la génération de jeux de données](./create-datasets.md) pour apprendre à générer un jeu de données à partir des résultats de requête dans Query Editor.

![L’onglet Résultats de la console du Query Editor affiche les résultats de l’exécution d’une requête.](../images/ui/query-editor/query-results.png)

## Cas d’utilisation {#use-cases}

Query Service fournit des solutions à divers cas d’utilisation dans différents secteurs d’activité et scénarios commerciaux. Ces exemples pratiques montrent la flexibilité et l&#39;impact du service pour répondre à divers besoins. À [Découvrez comment Query Service peut répondre à vos besoins spécifiques.](../use-cases/overview.md), explorez la collection complète de documents de cas d’utilisation. Découvrez comment utiliser Query Service pour fournir des insights et des solutions pour une efficacité opérationnelle et une réussite commerciale améliorées.

<!-- This video is from 2019. The logic is sounds but the workflow is too outdated. -->

## Tutoriel vidéo sur l’exécution de requêtes avec Query Service {#query-tutorial-video}

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. La vidéo présente également l’utilisation de propriétés individuelles dans un objet XDM, des fonctions définies par l’Adobe et comment utiliser des requêtes CREATE TABLE AS SELECT (CTAS).

>[!NOTE]
>
>L’interface utilisateur décrite dans la vidéo est obsolète, mais la logique utilisée dans le workflow reste la même.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Étapes suivantes

Maintenant que vous savez quelles fonctionnalités sont disponibles dans Query Editor et comment parcourir l’application, vous pouvez commencer à créer vos propres requêtes directement dans [!DNL Platform]. Pour plus d’informations sur l’exécution de requêtes SQL par rapport aux jeux de données dans [!DNL Data Lake], consultez le guide sur ’[exécution de requêtes](../best-practices/writing-queries.md).
