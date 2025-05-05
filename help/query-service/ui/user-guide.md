---
keywords: Experience Platform;accueil;rubriques populaires;Query editor;query editor;Query service;query service;
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Editor
description: Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service. Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’Experience Platform. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '2683'
ht-degree: 25%

---

# Guide de l’interface utilisateur de Query Editor

Query Editor est un outil interactif fourni par Adobe Experience Platform Query Service. Il permet d’écrire, de valider et d’exécuter des requêtes pour les données d’expérience client dans l’interface utilisateur d’[!DNL Experience Platform]. Query Editor prend en charge le développement de requête pour l’analyse et l’exploration de données. Il vous permet également d’exécuter des requêtes interactives à des fins de développement, ainsi que des requêtes non interactives pour renseigner les jeux de données dans [!DNL Experience Platform].

Pour plus d’informations sur les concepts et les fonctionnalités de Query Service, consultez la [Présentation de Query Service](../home.md). Pour en savoir plus sur la navigation dans l’interface utilisateur de Query Service sur [!DNL Experience Platform], consultez la [Présentation de l’interface utilisateur de Query Service](./overview.md).

## Prise en main {#getting-started}

Query Editor offre une exécution flexible des requêtes en se connectant à Query Service, et les requêtes ne s’exécutent que lorsque cette connexion est active.

## Accès à Query Editor {#accessing-query-editor}

Dans l’interface utilisateur de [!DNL Experience Platform], sélectionnez **[!UICONTROL Requêtes]** dans le menu de navigation de gauche pour ouvrir l’espace de travail de Query Service. Ensuite, pour commencer à écrire des requêtes, sélectionnez **[!UICONTROL Créer une requête]** en haut à droite de l’écran. Ce lien est disponible depuis n’importe quelle page de l’espace de travail Query Service.

![Onglet Présentation de l’espace de travail Requêtes avec l’option Créer une requête mise en surbrillance.](../images/ui/query-editor/create-query.png)

### Connexion à Query Service {#connecting-to-query-service}

Query Editor prend quelques secondes pour s’initialiser et se connecter à Query Service lorsqu’il est ouvert. La console vous indique qu’il est connecté, comme illustré ci-dessous. Si vous tentez d’exécuter une requête avant que l’éditeur ne soit connecté, l’exécution est retardée jusqu’à ce que la connexion soit établie.

![Sortie de console du Query Editor lors de la connexion initiale.](../images/ui/query-editor/connect.png)

### Exécution des requêtes depuis Query Editor {#run-a-query}

Les requêtes exécutées à partir du Query Editor s’exécutent de manière interactive, ce qui signifie que si vous fermez le navigateur ou quittez la page, la requête est annulée. Il en va de même pour les requêtes effectuées pour générer des jeux de données à partir de sorties de requête.

## Création de requêtes à l’aide de l’éditeur de requêtes amélioré {#query-authoring}

Avec Query Editor, vous pouvez écrire, exécuter et enregistrer des requêtes de données d’expérience client. Toutes les requêtes exécutées ou enregistrées dans Query Editor sont disponibles pour tous les utilisateurs de votre organisation qui ont accès à Query Service.

### Sélecteur de base de données {#database-selector}

Sélectionnez une base de données à interroger dans le menu déroulant en haut à droite de Query Editor. La base de données sélectionnée s’affiche dans la liste déroulante.

![Query Editor avec le menu déroulant de la base de données mis en surbrillance.](../images/ui/query-editor/database-dropdown.png)

### Paramètres {#settings}

Une icône de paramètres située au-dessus du champ de saisie du Query Editor inclut des options permettant d’activer/désactiver le thème sombre ou de désactiver/activer la saisie automatique.

>[!TIP]
>
>Vous pouvez [!UICONTROL désactiver la saisie automatique de la syntaxe] lors de la création d’une requête sans perdre votre progression.

Pour activer les thèmes sombres ou clairs, sélectionnez l’icône des paramètres (![A icône des paramètres.](/help/images/icons/settings.png)) suivi de l’option dans le menu déroulant qui s’affiche.

![Query Editor avec l’icône des paramètres et l’option de menu déroulant Activer le thème sombre mise en surbrillance.](../images/ui/query-editor/query-editor-settings.png)

#### Saisie automatique {#auto-complete}

Le Query Editor suggère automatiquement des mots-clés SQL potentiels ainsi que des détails de tableau ou de colonne pour la requête au fur et à mesure que vous l’écrivez. La fonction de saisie automatique est activée par défaut et peut être désactivée ou activée à tout moment à partir des paramètres du Query Editor.

Le paramètre de configuration de saisie automatique est défini par utilisateur et mémorisé pour les connexions consécutives de cet utilisateur. La désactivation de cette fonction arrête le traitement de plusieurs commandes de métadonnées et la suggestion de recommandations qui accélère généralement la vitesse de l’auteur lors de la modification des requêtes.


### Exécution de plusieurs requêtes séquentielles {#execute-multiple-sequential-queries}

Utilisez l’éditeur de requêtes amélioré pour écrire plusieurs requêtes et exécuter toutes les requêtes de manière séquentielle. L’exécution de plusieurs requêtes dans une séquence génère chacune une entrée de journal. Cependant, seuls les résultats de la première requête s’affichent dans la console du Query Editor. Vérifiez le journal des requêtes si vous devez dépanner ou confirmer les requêtes qui ont été exécutées. Pour plus d’informations, consultez la [documentation sur les journaux de requêtes](./query-logs.md).

>[!NOTE]
> 
>Si une requête CTAS est exécutée après la première requête dans le Query Editor, une table est toujours créée, mais aucune sortie n’est générée sur la console Query Editor.

### Exécuter la requête sélectionnée {#execute-selected-query}

Si vous avez écrit plusieurs requêtes, mais ne devez exécuter qu’une seule, vous pouvez mettre en surbrillance la requête choisie et sélectionner la requête
Icône [!UICONTROL &#x200B; Exécuter la requête sélectionnée &#x200B;]. Cette icône est désactivée par défaut jusqu’à ce que vous sélectionniez la syntaxe de la requête dans l’éditeur.

![Query Editor avec l’icône [!UICONTROL Exécuter la requête sélectionnée] mise en surbrillance.](../images/ui/query-editor/run-selected-query.png)

### Annuler la session du Query Editor {#cancel-query}

Prenez le contrôle de l’exécution des requêtes et améliorez votre productivité en annulant les requêtes de longue durée. Cette action efface le Query Editor lors de l’exécution d’une requête. N’oubliez pas que la requête continue de s’exécuter en arrière-plan. S’il s’agit d’une requête CTAS, elle génère toujours un jeu de données de sortie. Pour annuler l’exécution dans l’éditeur et continuer à composer une instruction SQL, sélectionnez **[!UICONTROL Annuler la requête]** après l’exécution d’une requête.

![Query Editor avec l’option [!UICONTROL Annuler la requête] mise en surbrillance.](../images/ui/query-editor/cancel-query-run.png)

Une boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Confirmer]** pour annuler l’exécution de la requête.

![Boîte de dialogue de confirmation d’annulation de la requête avec l’option Confirmer mise en surbrillance.](../images/ui/query-editor/cancel-query-confirmation-dialog.png)

### Nombre de résultats {#result-count}

Le Query Editor a une sortie de ligne maximale de 50 000. Vous pouvez choisir le nombre de lignes à afficher en même temps dans la console du Query Editor. Pour modifier le nombre de lignes affichées dans la console, sélectionnez la liste déroulante **[!UICONTROL Nombre de résultats]** et sélectionnez l’une des options suivantes : 50, 100, 150, 300, 500 et 1 000.

>[!NOTE]
>
>Comme l’interface utilisateur d’Experience Platform peut prendre en charge jusqu’à 1 000 lignes, la transmission d’une valeur LIMIT supérieure à 1 000 est ignorée.

![Query Editor avec le menu déroulant Nombre de résultats mis en surbrillance.](../images/ui/query-editor/result-count.png)

## Rédaction de requêtes {#writing-queries}

[!UICONTROL Query Editor est organisé de façon à rendre l’écriture de requête aussi facile que possible. &#x200B;] La copie d’écran ci-dessous présente l’affichage de l’éditeur dans l’interface utilisateur. Le champ d’entrée SQL et le bouton **Lire** sont mis en surbrillance.

![Query Editor avec le champ d’entrée SQL et le bouton Lire en surbrillance.](../images/ui/query-editor/editor.png)

Pour réduire au minimum le temps de développement, il est recommandé de développer vos requêtes avec des limites sur le nombre de lignes renvoyées. Par exemple : `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Une fois que vous avez vérifié que votre requête produit la sortie attendue, supprimez les limites et exécutez la requête avec `CREATE TABLE tablename AS SELECT`, afin de générer un jeu de données avec la sortie.

## Outils d’écriture dans Query Editor {#writing-tools}

Utilisez les outils d’écriture de Query Editor pour améliorer votre processus de création de requêtes. Les fonctionnalités incluent des options pour formater le texte, copier le code SQL, gérer les détails de la requête et enregistrer ou planifier votre travail au fur et à mesure de votre progression.

### Mettre le texte en forme {#format-text}

La fonction [!UICONTROL Format de texte] rend votre requête plus lisible en ajoutant un style de syntaxe normalisé. Sélectionnez **[!UICONTROL Formater le texte]** pour normaliser tout le texte dans le Query Editor.

>[!NOTE]
>
>La fonction [!UICONTROL Format du texte] ne fonctionne pas avec les blocs anonymes. Pour savoir comment enchaîner séquentiellement une ou plusieurs instructions SQL, consultez la documentation sur les blocs anonymes [anonyme](../key-concepts/anonymous-block.md).

![Query Editor avec [!UICONTROL Format du texte] et les instructions SQL mises en surbrillance.](../images/ui/query-editor/format-text.png)

<!-- ### Undo text {#undo-text}

If you format your SQL in the Query Editor, you can undo the formatting applied by the [!UICONTROL Format text] feature. To return your SQL back to its original form, select **[!UICONTROL Undo text]**.

![The Query Editor with [!UICONTROL Undo text] and the SQL statements highlighted.](../images/ui/query-editor/undo-text.png) -->

### Copier le SQL {#copy-sql}

Sélectionnez l’icône Copier pour copier le code SQL de Query Editor dans le presse-papiers. Cette fonctionnalité de copie est disponible pour les modèles de requête et les requêtes nouvellement créées dans Query Editor.

![Espace de travail Requêtes avec un exemple de modèle de requête avec l’icône de copie mise en surbrillance.](../images/ui/query-editor/copy-sql.png)

### Détails de la requête {#query-details}

Pour afficher une requête dans le Query Editor, sélectionnez n’importe quel modèle enregistré dans l’onglet [!UICONTROL Modèles]. Le panneau des détails de la requête fournit plus d’informations et d’outils pour gérer la requête sélectionnée. Elle affiche également des métadonnées utiles, telles que la dernière fois où la requête a été modifiée et qui l’a modifiée, le cas échéant.

>[!NOTE]
>
>Les options [!UICONTROL Afficher le planning], [!UICONTROL Ajouter un planning] et [!UICONTROL Supprimer la requête] ne sont disponibles qu’une fois la requête enregistrée en tant que modèle. L’option [!UICONTROL Ajouter un planning] vous permet d’accéder directement au créateur de plannings à partir du Query Editor. L&#39;option [!UICONTROL Afficher le planning] vous permet d&#39;accéder directement à l&#39;inventaire planifié pour cette requête. Consultez la documentation sur les plannings de requête pour savoir comment [ créer des plannings de requête dans l’interface utilisateur ](./query-schedules.md#create-schedule).

![Query Editor avec le panneau des détails de la requête mis en surbrillance.](../images/ui/query-editor/query-details.png)

Dans le panneau des détails, vous pouvez générer un jeu de données de sortie directement à partir de l’interface utilisateur, supprimer ou nommer la requête affichée, afficher le planning d’exécution de la requête et ajouter la requête à un planning.

Pour générer un jeu de données de sortie, sélectionnez **[!UICONTROL Exécuter en tant que CTAS]**. La boîte de dialogue **[!UICONTROL Saisir les détails du jeu de données de sortie]** s’affiche. Saisissez un nom et une description, puis sélectionnez **[!UICONTROL Exécuter en tant que CTAS]**. Le nouveau jeu de données s’affiche dans l’onglet Parcourir **[!UICONTROL Jeux de données]**. Voir [documentation sur l’affichage des jeux de données](../../catalog/datasets/user-guide.md#view-datasets) pour en savoir plus sur les jeux de données disponibles pour votre organisation.

>[!NOTE]
>
>L’option [!UICONTROL Exécuter en tant que CTAS] n’est disponible que si la requête n’a **pas** été planifiée.

![Boîte de dialogue [!UICONTROL Saisir les détails du jeu de données de sortie].](../images/ui/query-editor/output-dataset-details.png)

Une fois que vous avez exécuté l’action **[!UICONTROL Exécuter en tant que CTAS]**, un message de confirmation s’affiche pour vous informer de la réussite de l’action. Ce message contextuel contient un lien qui permet d’accéder facilement à l’espace de travail des journaux de requête. Pour plus d’informations sur les journaux de requêtes[&#128279;](./query-logs.md) consultez la  documentation sur les journaux de requêtes .

### Enregistrement des requêtes {#saving-queries}

Le Query Editor fournit une fonction de sauvegarde qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Pour enregistrer une requête, sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit de Query Editor. Avant de pouvoir enregistrer une requête, vous devez lui donner un nom à l’aide du panneau **[!UICONTROL Détails sur la requête]**.

>[!NOTE]
>
>Les requêtes nommées et enregistrées dans à l’aide du Query Editor sont disponibles sous forme de modèles dans l’onglet [!UICONTROL Modèles] du tableau de bord Requête. Pour plus d’informations, consultez la [documentation sur les modèles](./query-templates.md).

Lorsque vous enregistrez une requête dans le Query Editor, un message de confirmation s’affiche pour vous informer de la réussite de l’action. Ce message contextuel contient un lien qui permet d&#39;accéder facilement à l&#39;espace de travail de planification des requêtes. Consultez la [documentation sur la planification des requêtes](./query-schedules.md) pour savoir comment exécuter des requêtes à une cadence personnalisée.

### Requêtes planifiées {#scheduled-queries}

Les requêtes qui ont été enregistrées en tant que modèle peuvent être planifiées à partir de Query Editor. La planification des requêtes vous permet d’automatiser l’exécution des requêtes selon une cadence personnalisée. Vous pouvez planifier des requêtes en fonction de la fréquence, de la date et de l’heure, mais aussi choisir un jeu de données de sortie pour vos résultats, si nécessaire. Les plannings de requête peuvent également être désactivés ou supprimés via l’interface utilisateur.

Les plannings sont définis dans le Query Editor. Lors de l’utilisation de Query Editor, vous pouvez uniquement ajouter un planning à une requête qui a déjà été créée et enregistrée. La même limitation ne s’applique pas à l’API Query Service.

>[!NOTE]
>
>Les requêtes planifiées qui échouent dix exécutions consécutives sont automatiquement placées dans un statut [!UICONTROL &#x200B; Quarantaine &#x200B;]. Une requête avec ce statut nécessite votre intervention avant que d’autres exécutions puissent avoir lieu. Consultez la documentation [requêtes en quarantaine](./monitor-queries.md#quarantined-queries) pour plus d’informations.

Consultez la documentation sur les plannings de requête pour savoir comment [ créer des plannings de requête dans l’interface utilisateur ](./query-schedules.md). Vous pouvez également découvrir comment ajouter des plannings à l’aide de l’API dans le guide de point d’entrée [des requêtes planifiées](../api/scheduled-queries.md).

Toutes les requêtes planifiées sont ajoutées à la liste dans l’onglet [!UICONTROL Requêtes planifiées]. Depuis cet espace de travail, vous pouvez surveiller le statut de toutes les tâches de requête planifiées via l’interface utilisateur. Sur l’onglet [!UICONTROL Requêtes planifiées], vous pouvez trouver des informations importantes sur les exécutions de vos requêtes et vous abonner aux alertes. Les informations disponibles incluent le statut, les détails du planning et les messages/codes d’erreur en cas d’échec de l’exécution. Pour plus d’informations, consultez le document [Surveiller les requêtes planifiées](./monitor-queries.md) .


### Accès aux requêtes précédentes {#previous-queries}

Toutes les requêtes exécutées depuis Query Editor sont capturées dans le tableau Journal. Vous pouvez utiliser la fonctionnalité de recherche dans l’onglet **[!UICONTROL Journal]** pour rechercher des exécutions de requête. Les requêtes enregistrées sont répertoriées dans l’onglet **[!UICONTROL Modèles]**.

Si une requête a été planifiée, alors l’onglet [!UICONTROL Requêtes planifiées] offre une meilleure visibilité à travers l’interface utilisateur pour ces tâches de requête. Pour plus d’informations, consultez la [documentation sur la surveillance des requêtes](./monitor-queries.md).

>[!NOTE]
>
>Les requêtes non exécutées ne sont pas enregistrées dans le journal. Pour que la requête soit disponible dans Query Service, elle doit être exécutée ou enregistrée dans Query Editor.

### Explorateur d’objets {#object-browser}

Utilisez l’explorateur d’objets pour rechercher et filtrer facilement des jeux de données. L’explorateur d’objets réduit le temps passé à rechercher des tables et des jeux de données dans des environnements volumineux avec de nombreux jeux de données. Grâce à un accès simplifié aux données et métadonnées pertinentes, vous pouvez vous concentrer davantage sur la création de requêtes et moins sur la navigation.

Pour naviguer dans la base de données avec l’explorateur d’objets, saisissez un nom de tableau dans le champ de recherche ou sélectionnez **[!UICONTROL Tableaux]** pour développer la liste des jeux de données et des tableaux disponibles. Lors de l’utilisation du champ de recherche, la liste des tableaux disponibles est filtrée de manière dynamique en fonction de vos entrées.

Chaque jeu de données contenu dans [la base de données sélectionnée](#database-dropdown) est répertorié dans un rail de navigation à gauche du Query Editor.

![Rail de navigation du jeu de données de Query Editor avec l’entrée de recherche mise en surbrillance.](../images/ui/query-editor/search-tables.png)

Le schéma affiché dans l’explorateur d’objets est un schéma observable. Cela signifie que vous pouvez l’utiliser pour surveiller les modifications et les mises à jour en temps réel, car les modifications sont immédiatement visibles. Les schémas observables permettent d’assurer la synchronisation des données et facilitent les tâches de débogage ou d’analyse.

#### Limitation actuelle {#current-limitation}

Le système traite les requêtes de manière séquentielle, ce qui signifie qu’une seule requête peut être exécutée à la fois. Lorsqu’une requête est en cours, les tables supplémentaires ne sont pas accessibles dans le volet de navigation de gauche.

#### Accès aux métadonnées de la table {#table-metadata}

Outre les recherches rapides, vous pouvez désormais accéder facilement aux métadonnées de n’importe quel tableau en sélectionnant l’icône « i » en regard du nom du tableau. Vous obtenez ainsi des informations détaillées sur la table sélectionnée, ce qui vous aide à prendre des décisions éclairées lors de la rédaction de requêtes.

![Rail de navigation du jeu de données de Query Editor avec l’entrée de recherche mise en surbrillance.](../images/ui/query-editor/table-metadata.png)

#### Explorer les tables enfants

Pour explorer les tableaux enfants ou liés, sélectionnez la flèche déroulante en regard d’un nom de tableau dans la liste. Cela développe la table pour afficher toutes les tables enfants associées, et donne une vue claire de la structure des données et permet des constructions de requête plus complexes. L’icône en regard du nom du champ indique le type de données de la colonne, afin de vous aider à l’identifier lors de requêtes complexes.

![Query Editor avec la liste de tableau filtrée affichée.](../images/ui/query-editor/child-table-list.png)

## Exécution de requête à l’aide de Query Editor {#executing-queries}

Pour exécuter une requête dans Query Editor, vous pouvez saisir le langage SQL dans l&#39;éditeur ou charger une requête précédente depuis l&#39;onglet **[!UICONTROL Log]** ou **[!UICONTROL Modèles]** et sélectionner **Lire**. L’état de l’exécution de la requête s’affiche dans l’onglet **[!UICONTROL Console]** ci-dessous et les données de sortie s’affichent dans l’onglet **[!UICONTROL Résultats]**.

### Console {#console}

La console fournit des informations sur l’état et le fonctionnement de Query Service. La console affiche l’état de la connexion à Query Service, les opérations des requêtes en cours d’exécution et tout message d’erreur résultant de ces requêtes.

![L’onglet Console de la console du Query Editor.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La console affiche uniquement les erreurs résultant de l’exécution d’une requête. Elle n’affiche pas les erreurs de validation de requête qui se produisent avant l’exécution d’une requête.

### Résultats de requête {#query-results}

Une fois une requête terminée, les résultats sont affichés dans l’onglet **[!UICONTROL Résultats]**, en regard de l’onglet **[!UICONTROL Console]**. Cette vue affiche la sortie tabulaire de votre requête, affichant entre 50 et 1 000 lignes de résultats en fonction du nombre de [résultats](#result-count) choisi. Il vous permet de vérifier que votre requête produit la sortie attendue. Pour générer un jeu de données avec votre requête, supprimez les limites sur les lignes renvoyées, puis exécutez la requête avec `CREATE TABLE tablename AS SELECT` pour générer un jeu de données avec la sortie. Consultez le [tutoriel sur la génération de jeux de données](./create-datasets.md) pour apprendre à générer un jeu de données à partir des résultats de requête dans Query Editor.

![L’onglet Résultats de la console du Query Editor affiche les résultats de l’exécution d’une requête.](../images/ui/query-editor/query-results.png)

## Exemples {#examples}

Query Service fournit des solutions à divers cas d’utilisation dans des scénarios d’industries et d’entreprises. Ces exemples démontrent la souplesse et l&#39;incidence du service pour répondre à divers besoins. Pour [découvrir comment Query Service peut apporter de la valeur à vos besoins professionnels spécifiques](../use-cases/overview.md), explorez la collection complète de documents de cas d’utilisation. Découvrez comment utiliser Query Service pour fournir des informations et des solutions afin d’améliorer l’efficacité opérationnelle et la réussite commerciale.

<!-- This video is from 2019. The logic is sounds but the workflow is too outdated. -->

## Tutoriel vidéo sur l’exécution de requêtes avec Query Service {#query-tutorial-video}

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. La vidéo explique également l’utilisation de propriétés individuelles dans un objet XDM, les fonctions définies par Adobe et l’utilisation des requêtes CREATE TABLE AS SELECT (CTAS).

>[!NOTE]
>
>L’interface utilisateur illustrée dans la vidéo est obsolète, mais la logique utilisée dans le workflow reste la même.

>[!VIDEO](https://video.tv.adobe.com/v/32943?quality=12&learn=on&captions=fre_fr)

## Étapes suivantes

Maintenant que vous connaissez les fonctionnalités disponibles dans Query Editor et que vous savez naviguer dans l’application, vous pouvez commencer à créer vos propres requêtes directement dans [!DNL Experience Platform]. Pour plus d’informations sur l’exécution de requêtes SQL par rapport aux jeux de données dans [!DNL Data Lake], consultez le guide sur ’[exécution de requêtes](../best-practices/writing-queries.md).
