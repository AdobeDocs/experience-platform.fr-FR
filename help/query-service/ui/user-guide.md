---
keywords: Experience Platform;accueil;rubriques populaires;Query editor;query editor;Query service;query service;
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Editor
description: Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service. Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: d83604b2bf6a8e2f2b5802a5e7f26447fbf7eb2e
workflow-type: tm+mt
source-wordcount: '2821'
ht-degree: 23%

---

# Guide de l’interface utilisateur de Query Editor

>[!NOTE]
>
>L’ancien éditeur a été abandonné le 24 mai 2024. Il n’est plus accessible à l’utilisation. Vous pouvez désormais utiliser l’[Éditeur de requêtes amélioré](#enhanced-editor-toggle) pour écrire, valider et exécuter vos requêtes.

Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service qui vous permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur de [!DNL Experience Platform]. Query Editor prend en charge le développement de requêtes pour l’analyse et l’exploration de données, et vous permet d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour remplir des jeux de données dans [!DNL Experience Platform].

Pour plus d’informations sur les concepts et les fonctionnalités de Query Service, consultez la [Présentation de Query Service](../home.md). Pour en savoir plus sur la navigation dans l’interface utilisateur de Query Service sur [!DNL Platform], consultez la [Présentation de l’interface utilisateur de Query Service](./overview.md).

## Prise en main {#getting-started}

Query Editor permet une exécution flexible des requêtes en se connectant à Query Service. Les requêtes ne s’exécutent que lorsque cette connexion est active.

## Accès à Query Editor {#accessing-query-editor}

Dans l’interface utilisateur de [!DNL Experience Platform], sélectionnez **[!UICONTROL Requêtes]** dans le menu de navigation de gauche pour ouvrir l’espace de travail Query Service. Ensuite, pour commencer à écrire des requêtes, sélectionnez **[!UICONTROL Créer une requête]** en haut à droite de l’écran. Ce lien est disponible depuis n’importe quelle page de l’espace de travail Query Service.

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

### Sélecteur de base de données {#database-selector}

Sélectionnez une base de données à interroger dans le menu déroulant en haut à droite de l’éditeur de requêtes. La base de données sélectionnée s’affiche dans la liste déroulante.

![L’éditeur de requêtes avec le menu déroulant de la base de données en surbrillance.](../images/ui/query-editor/database-dropdown.png)

### Paramètres       {#settings}

Une icône de paramètres au-dessus du champ de saisie de l’éditeur de requêtes comprend des options pour activer/désactiver le thème sombre ou désactiver/activer la saisie automatique.

>[!TIP]
>
>Vous pouvez [!UICONTROL désactiver la saisie automatique de la syntaxe] lors de la création d’une requête sans perdre la progression.

Pour activer les thèmes foncés ou clairs, sélectionnez l’icône des paramètres (![Icône Paramètres A.](/help/images/icons/settings.png)) suivi de l’option dans le menu déroulant qui s’affiche.

![L’éditeur de requêtes avec l’icône de paramètres et l’option de menu déroulant Activer le thème sombre sont surlignée.](../images/ui/query-editor/query-editor-settings.png)

#### Saisie automatique {#auto-complete}

L’éditeur de requêtes propose automatiquement des mots-clés SQL potentiels, ainsi que des détails de tableau ou de colonne pour la requête au fur et à mesure que vous l’écrivez. La fonction de saisie automatique est activée par défaut et peut être désactivée ou activée à tout moment dans les paramètres de l’éditeur de requêtes.

Le paramètre de configuration de saisie automatique est défini par utilisateur et mémorisé pour les connexions consécutives de cet utilisateur. La désactivation de cette fonction arrête le traitement de plusieurs commandes de métadonnées et la suggestion de recommandations qui accélère généralement la vitesse de l’auteur lors de la modification des requêtes.


### Exécution de plusieurs requêtes séquentielles {#execute-multiple-sequential-queries}

Utilisez l’éditeur de requêtes amélioré pour écrire plusieurs requêtes et exécuter toutes les requêtes de manière séquentielle. L’exécution de plusieurs requêtes dans une séquence génère chacune une entrée de journal. Toutefois, seuls les résultats de la première requête s’affichent dans la console de l’éditeur de requêtes. Vérifiez le journal des requêtes si vous devez résoudre ou confirmer les requêtes qui ont été exécutées. Pour plus d’informations, consultez la [documentation sur les journaux de requête](./query-logs.md) .

>[!NOTE]
> 
>Si une requête CTAS est exécutée après la première requête dans Query Editor, une table est toujours créée, mais il n’y a aucune sortie dans la console Query Editor.

### Exécuter la requête sélectionnée {#execute-selected-query}

Si vous avez écrit plusieurs requêtes mais que vous ne devez exécuter qu’une seule requête, vous pouvez mettre en surbrillance la requête choisie et sélectionner l’événement
Icône [!UICONTROL Exécuter la requête sélectionnée] . Cette icône est désactivée par défaut jusqu’à ce que vous sélectionniez la syntaxe de la requête dans l’éditeur.

![L’éditeur de requêtes avec l’icône [!UICONTROL Exécuter la requête sélectionnée] mise en surbrillance.](../images/ui/query-editor/run-selected-query.png)

### Annuler la session de l’éditeur de requêtes {#cancel-query}

Contrôlez l’exécution des requêtes et améliorez votre productivité en annulant les requêtes longues. Cette action efface l’éditeur de requêtes lors d’une exécution de requête. Gardez à l’esprit que la requête continue de s’exécuter en arrière-plan. S’il s’agit d’une requête CTAS, elle génère toujours un jeu de données de sortie. Pour annuler l’exécution dans l’éditeur et continuer à composer une instruction SQL, sélectionnez **[!UICONTROL Annuler la requête]** après l’exécution d’une requête.

![L’éditeur de requêtes avec [!UICONTROL Annuler la requête] mise en surbrillance.](../images/ui/query-editor/cancel-query-run.png)

Une boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Confirmer]** pour annuler l’exécution de la requête.

![ La boîte de dialogue de confirmation de requête Annuler avec l’option Confirmer mise en surbrillance.](../images/ui/query-editor/cancel-query-confirmation-dialog.png)

### Nombre de résultats {#result-count}

L’éditeur de requêtes dispose d’une sortie de ligne maximale de 50 000 lignes. Vous pouvez choisir le nombre de lignes affichées simultanément dans la console de l’éditeur de requêtes. Pour modifier le nombre de lignes affichées dans la console, sélectionnez la liste déroulante **[!UICONTROL Result count]** et sélectionnez les options 50, 100, 150, 300 et 500.

>[!NOTE]
>
>Comme l’interface utilisateur de Platform ne peut prendre en charge que 500 lignes au maximum, la transmission d’une valeur LIMIT supérieure à 500 est ignorée.

![Éditeur de requête avec la liste déroulante Nombre de résultats mise en surbrillance.](../images/ui/query-editor/result-count.png)

## Rédaction de requêtes {#writing-queries}

[!UICONTROL Query Editor est organisé de façon à rendre l’écriture de requête aussi facile que possible. ] La copie d’écran ci-dessous présente l’affichage de l’éditeur dans l’interface utilisateur. Le champ d’entrée SQL et le bouton **Lire** sont mis en surbrillance.

![Query Editor avec le champ d’entrée SQL et le bouton Lire en surbrillance.](../images/ui/query-editor/editor.png)

Pour réduire le temps de développement, il est recommandé de développer vos requêtes avec des limites sur le nombre de lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête produit la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT`, afin de générer un jeu de données avec la sortie.

## Outils d’écriture dans Query Editor {#writing-tools}

Utilisez les outils d’écriture de Query Editor pour améliorer votre processus de création de requêtes. Les fonctionnalités incluent des options permettant de mettre en forme le texte, de copier SQL, de gérer les détails des requêtes, ainsi que d’enregistrer ou de planifier votre travail au fur et à mesure que vous progressez.

### Mettre le texte en forme {#format-text}

La fonction [!UICONTROL Format de texte] rend votre requête plus lisible en ajoutant un style de syntaxe normalisé. Sélectionnez **[!UICONTROL Format de texte]** pour normaliser tout le texte dans l’éditeur de requêtes.

>[!NOTE]
>
>La fonction [!UICONTROL Format de texte] ne fonctionne pas avec les blocs anonymes. Pour savoir comment chaîner une ou plusieurs instructions SQL de manière séquentielle, consultez la [documentation du bloc anonyme](../key-concepts/anonymous-block.md).

![L’éditeur de requêtes avec [!UICONTROL texte de format] et les instructions SQL mises en surbrillance.](../images/ui/query-editor/format-text.png)

<!-- ### Undo text {#undo-text}

If you format your SQL in the Query Editor, you can undo the formatting applied by the [!UICONTROL Format text] feature. To return your SQL back to its original form, select **[!UICONTROL Undo text]**.

![The Query Editor with [!UICONTROL Undo text] and the SQL statements highlighted.](../images/ui/query-editor/undo-text.png) -->

### Copier le SQL {#copy-sql}

Sélectionnez l’icône Copier pour copier SQL à partir de Query Editor dans le presse-papiers. Cette fonctionnalité de copie est disponible à la fois pour les modèles de requête et les requêtes nouvellement créées dans Query Editor.

![ L&#39;espace de travail Requêtes avec un exemple de modèle de requête avec l&#39;icône de copie mise en surbrillance.](../images/ui/query-editor/copy-sql.png)

### Détails de la requête {#query-details}

Pour afficher une requête dans Query Editor, sélectionnez un modèle enregistré dans l’onglet [!UICONTROL Modèles]. Le panneau Détails de la requête fournit des informations et des outils supplémentaires pour gérer la requête sélectionnée. Il affiche également des métadonnées utiles telles que la dernière fois où la requête a été modifiée et qui l’a modifiée, le cas échéant.

>[!NOTE]
>
>Les options [!UICONTROL Afficher la planification], [!UICONTROL Ajouter la planification] et [!UICONTROL Supprimer la requête] ne sont disponibles qu’après l’enregistrement de la requête en tant que modèle. L’option [!UICONTROL Ajouter un planning] permet d’accéder directement au créateur de planning à partir de l’éditeur de requêtes. L’option [!UICONTROL Afficher le planning] permet d’accéder directement à l’inventaire des planifications pour cette requête. Consultez la documentation sur les plannings de requête pour savoir comment [créer des plannings de requête dans l’interface utilisateur](./query-schedules.md#create-schedule).

![Query Editor avec le panneau des détails de la requête mis en surbrillance.](../images/ui/query-editor/query-details.png)

Dans le panneau Détails, vous pouvez générer un jeu de données de sortie directement à partir de l’interface utilisateur, supprimer ou nommer la requête affichée, afficher le planning d’exécution de la requête et ajouter la requête à un planning.

Pour générer un jeu de données de sortie, sélectionnez **[!UICONTROL Exécuter en tant que CTAS]**. La boîte de dialogue **[!UICONTROL Enter output dataset details]** s’affiche. Saisissez un nom et une description, puis sélectionnez **[!UICONTROL Exécuter en tant que CTAS]**. Le nouveau jeu de données s’affiche dans l’onglet de navigation **[!UICONTROL Jeux de données]**. Pour en savoir plus sur les jeux de données disponibles pour votre organisation, consultez la [documentation sur l’affichage des jeux de données](../../catalog/datasets/user-guide.md#view-datasets) .

>[!NOTE]
>
>L&#39;option [!UICONTROL Exécuter en tant que CTAS] n&#39;est disponible que si la requête **et non** a été planifiée.

![Boîte de dialogue [!UICONTROL Entrez les détails du jeu de données de sortie].](../images/ui/query-editor/output-dataset-details.png)

Après avoir exécuté l’action **[!UICONTROL Exécuter en tant que CTAS]**, un message de confirmation s’affiche pour vous informer de la réussite de l’action. Ce message contextuel contient un lien qui permet d’accéder facilement à l’espace de travail des logs de requête. Pour plus d’informations sur les logs de requête, consultez la [documentation sur les logs de requête](./query-logs.md) .

### Enregistrement des requêtes {#saving-queries}

Query Editor fournit une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Pour enregistrer une requête, sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit de Query Editor. Avant de pouvoir enregistrer une requête, vous devez lui donner un nom à l’aide du panneau **[!UICONTROL Détails sur la requête]**.

>[!NOTE]
>
>Les requêtes nommées et enregistrées dans à l’aide du Query Editor sont disponibles sous forme de modèles dans l’onglet [!UICONTROL Modèles] du tableau de bord Requête. Pour plus d’informations, consultez la [documentation sur les modèles](./query-templates.md).

Lorsque vous enregistrez une requête dans l’éditeur de requêtes, un message de confirmation s’affiche pour vous informer de la réussite de l’action. Ce message contextuel contient un lien qui permet d’accéder facilement à l’espace de travail de planification des requêtes. Consultez la [documentation sur les requêtes de planification](./query-schedules.md) pour savoir comment exécuter des requêtes sur une cadence personnalisée.

### Requêtes planifiées {#scheduled-queries}

Les requêtes qui ont été enregistrées en tant que modèle peuvent être planifiées à partir de l’éditeur de requêtes. La planification des requêtes vous permet d’automatiser les exécutions de requête sur une cadence personnalisée. Vous pouvez planifier des requêtes en fonction de la fréquence, de la date et de l’heure, et choisir également un jeu de données de sortie pour vos résultats, si nécessaire. Les plannings de requête peuvent également être désactivés ou supprimés via l’interface utilisateur.

Les planifications sont définies dans l’éditeur de requêtes. Lorsque vous utilisez l’éditeur de requêtes, vous ne pouvez ajouter qu’un planning à une requête qui a déjà été créée et enregistrée. La même limitation ne s’applique pas à l’API Query Service.

>[!NOTE]
>
>Les requêtes planifiées qui échouent dix exécutions consécutives sont automatiquement placées dans un état [!UICONTROL Quarantined]. Une requête avec ce statut nécessite votre intervention avant toute autre exécution. Pour plus d’informations, consultez la documentation [ sur les requêtes mises en quarantaine](./monitor-queries.md#quarantined-queries) .

Consultez la documentation sur les plannings de requête pour savoir comment [créer des plannings de requête dans l’interface utilisateur](./query-schedules.md). Vous pouvez également découvrir comment ajouter des plannings à l’aide de l’API en lisant le [guide de point de terminaison de requêtes planifiées](../api/scheduled-queries.md).

Toutes les requêtes planifiées sont ajoutées à la liste dans l’onglet [!UICONTROL Requêtes planifiées] . Depuis cet espace de travail, vous pouvez surveiller l’état de toutes les tâches de requête planifiées via l’interface utilisateur. Dans l’onglet [!UICONTROL  Requêtes planifiées ], vous pouvez trouver des informations importantes sur les exécutions de vos requêtes et vous abonner à des alertes. Les informations disponibles incluent l’état, les détails de planification et les messages/codes d’erreur en cas d’échec de l’exécution. Pour plus d’informations, consultez le document [Surveiller les requêtes planifiées](./monitor-queries.md) .


### Accès aux requêtes précédentes {#previous-queries}

Toutes les requêtes exécutées depuis Query Editor sont capturées dans le tableau Journal. Vous pouvez utiliser la fonctionnalité de recherche dans l’onglet **[!UICONTROL Journal]** pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans l’onglet **[!UICONTROL Modèles]**.

Si une requête a été planifiée, alors l’onglet [!UICONTROL Requêtes planifiées] offre une meilleure visibilité à travers l’interface utilisateur pour ces tâches de requête. Pour plus d’informations, consultez la [documentation sur la surveillance des requêtes](./monitor-queries.md).

>[!NOTE]
>
>Les requêtes non exécutées ne sont pas enregistrées dans le journal. Pour que la requête soit disponible dans Query Service, elle doit être exécutée ou enregistrée dans Query Editor.

### Explorateur d’objets {#object-browser}

>[!AVAILABILITY]
>
>Le rail de navigation du jeu de données n’est disponible que pour les clients Data Distiller. Votre interface utilisateur Platform peut ne pas contenir le rail de navigation du jeu de données de gauche.  D’autres images de ce document peuvent ne pas refléter le rail de navigation du jeu de données. Pour plus d’informations, contactez votre représentant d’Adobe.

Utilisez l’explorateur d’objets pour rechercher et filtrer facilement des jeux de données. L’explorateur d’objets réduit le temps passé à rechercher des tableaux et des jeux de données dans des environnements volumineux avec de nombreux jeux de données. Grâce à un accès simplifié aux données et métadonnées pertinentes, vous pouvez vous concentrer davantage sur la création de requêtes et moins sur la navigation.

Pour naviguer dans votre base de données à l’aide du navigateur d’objets, saisissez un nom de tableau dans le champ de recherche ou sélectionnez **[!UICONTROL Tableaux]** pour développer la liste des jeux de données et des tableaux disponibles. Lors de l’utilisation du champ de recherche, la liste des tables disponibles est filtrée dynamiquement en fonction de votre saisie.

>[!NOTE]
>
>Chaque jeu de données contenu dans [votre base de données sélectionnée](#database-dropdown) est répertorié dans un rail de navigation à gauche de Query Editor.

![ Rail de navigation du jeu de données Query Editor avec l’entrée de recherche mise en surbrillance.](../images/ui/query-editor/search-tables.png)

Le schéma affiché dans l’explorateur d’objets est un schéma observable. Cela signifie que vous pouvez l’utiliser pour surveiller les modifications et les mises à jour en temps réel lorsque les modifications sont immédiatement visibles. Les schémas observables permettent d’assurer la synchronisation des données et aident à effectuer des tâches de débogage ou d’analyse.

#### Limites actuelles {#current-limitations}

Voici une liste des limites actuelles :

- Exécution de requête séquentielle : une seule requête peut être exécutée à la fois. Lorsqu’une requête est en cours, aucune table supplémentaire ne peut être ouverte dans le volet de navigation de gauche, car les requêtes sont traitées de manière séquentielle.
- Lignes supplémentaires dans les logs de requête : vous pouvez rencontrer des requêtes superflues étiquetées &quot;AFFICHER LES TABLES&quot; dans les logs. Elles seront supprimées dans les prochaines versions.

#### Accès aux métadonnées de tableau {#table-metadata}

Outre les recherches rapides, vous pouvez désormais accéder facilement aux métadonnées d’un tableau en cliquant sur l’icône &quot;i&quot; en regard du nom de ce dernier. Vous disposez ainsi d’informations détaillées sur le tableau sélectionné, qui vous permettent de prendre des décisions éclairées lors de l’écriture de requêtes.

![ Rail de navigation du jeu de données Query Editor avec l’entrée de recherche mise en surbrillance.](../images/ui/query-editor/table-metadata.png)

#### Exploration des tables enfants

Pour explorer des tables enfants ou liées, sélectionnez la flèche de liste déroulante en regard d’un nom de table dans la liste. Le tableau est ainsi développé afin d’afficher les tables enfants associées. Il donne une vue précise de la structure des données et permet des constructions de requêtes plus complexes. L’icône en regard du nom du champ indique le type de données de la colonne, afin de vous aider à l’identifier lors de requêtes complexes.

![L’éditeur de requêtes avec la liste des tableaux filtrés affichée.](../images/ui/query-editor/child-table-list.png)

## Exécution de requête à l’aide de Query Editor {#executing-queries}

Pour exécuter une requête dans Query Editor, vous pouvez saisir du code SQL dans l’éditeur ou charger une requête précédente à partir de l’onglet **[!UICONTROL Journal]** ou **[!UICONTROL Modèles]** et sélectionner **Lire**. L’état de l’exécution de la requête s’affiche dans l’onglet **[!UICONTROL Console]** ci-dessous et les données de sortie s’affichent dans l’onglet **[!UICONTROL Résultats]**.

### Console {#console}

La console fournit des informations sur l’état et le fonctionnement de Query Service. La console affiche l’état de la connexion à Query Service, les opérations des requêtes en cours d’exécution et tout message d’erreur résultant de ces requêtes.

![L’onglet Console de la console du Query Editor.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l&#39;exécution d&#39;une requête. Elle n’affiche pas les erreurs de validation de requête qui se produisent avant l’exécution d’une requête.

### Résultats de requête {#query-results}

Une fois une requête terminée, les résultats sont affichés dans l’onglet **[!UICONTROL Résultats]**, en regard de l’onglet **[!UICONTROL Console]**. Cette vue affiche la sortie tabulaire de votre requête, affichant entre 50 et 500 lignes de résultats selon le [nombre de résultats](#result-count) que vous avez choisi. Il vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées, puis exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le [tutoriel sur la génération de jeux de données](./create-datasets.md) pour apprendre à générer un jeu de données à partir des résultats de requête dans Query Editor.

![L’onglet Résultats de la console du Query Editor affiche les résultats de l’exécution d’une requête.](../images/ui/query-editor/query-results.png)

## Exemples {#examples}

Query Service fournit des solutions à divers cas d’utilisation dans différents secteurs d’activité et scénarios commerciaux. Ces exemples démontrent la flexibilité et l&#39;impact du service pour répondre à divers besoins. Pour [découvrir comment Query Service peut apporter de la valeur à vos besoins spécifiques](../use-cases/overview.md), explorez la collection complète de documents de cas d’utilisation. Découvrez comment utiliser Query Service pour fournir des insights et des solutions pour une efficacité opérationnelle et une réussite commerciale améliorées.

<!-- This video is from 2019. The logic is sounds but the workflow is too outdated. -->

## Tutoriel vidéo sur l’exécution de requêtes avec Query Service {#query-tutorial-video}

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. La vidéo présente également l’utilisation de propriétés individuelles dans un objet XDM, des fonctions définies par l’Adobe et comment utiliser des requêtes CREATE TABLE AS SELECT (CTAS).

>[!NOTE]
>
>L’interface utilisateur décrite dans la vidéo est obsolète, mais la logique utilisée dans le workflow reste la même.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Étapes suivantes

Maintenant que vous savez quelles fonctionnalités sont disponibles dans Query Editor et comment naviguer dans l’application, vous pouvez commencer à créer vos propres requêtes directement dans [!DNL Platform]. Pour plus d’informations sur l’exécution de requêtes SQL par rapport aux jeux de données dans [!DNL Data Lake], consultez le guide sur ’[exécution de requêtes](../best-practices/writing-queries.md).
