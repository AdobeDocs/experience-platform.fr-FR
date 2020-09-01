---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Guide de l’interface utilisateur d’Adobe Experience Platform Query Service
topic: guide
description: Adobe Experience Platform Query Service présente une interface utilisateur qui permet d’écrire et d’exécuter des requêtes, de voir les requêtes précédemment exécutées et d’accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 67%

---


# [!DNL Query Service] guide

The Adobe Experience Platform [!DNL Query Service] provides a user interface that can be used to write and execute queries, view previously executed queries, and access queries saved by users within your IMS Organization. Pour accéder à l’interface utilisateur d’[Adobe Experience Platform][platform-ui], sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche.

## [!DNL Query Editor]

The [!DNL Query Editor] enables you to write and execute queries without using an external client. Click **[!UICONTROL Create Query]** to open the [!DNL Query Editor] and create a new query. You can also access the [!DNL Query Editor] by selecting a query from the **[!UICONTROL Log]** or **[!UICONTROL Browse]** tabs. Selecting a previously executed or saved query will open the [!DNL Query Editor] and display the SQL for the selected query.

![Image](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] fournit un espace de modification dans lequel vous pouvez commencer à saisir une requête. Au fur et à mesure que vous tapez, l’éditeur complète automatiquement les mots réservés SQL, les tables et les noms des champs dans les tables. When finished writing your query, click the **Play** button to run the query. L’onglet **[!UICONTROL Console]** situé sous l’éditeur indique ce que fait actuellement , indiquant le moment où une requête a été renvoyée. [!DNL Query Service] L’onglet **[!UICONTROL Résultat]**, en regard de la Console, affiche les résultats de la requête. See the [Query Editor guide][query-editor] for more information on using the [!DNL Query Editor].

![Image](../images/queries/ui-overview/query-editor.png)

## Parcourir

L’onglet **[!UICONTROL Parcourir]** affiche les requêtes enregistrées par les utilisateurs de votre organisation. Il est utile de les voir comme des projets de requêtes, car les requêtes enregistrées ici peuvent encore être en cours de construction. Les requêtes affichées dans l’onglet **[!UICONTROL Parcourir]** s’affichent également sous la forme de requêtes exécutées dans l’onglet **[!UICONTROL Journal]** si elles ont été exécutées par [!DNL Query Service].

![Image](../images/queries/ui-overview/browse.png)

| Colonne | Description |
| --- | --- |
| Nom | Nom de la requête créée par l’utilisateur. You can click on the name to open the query in the [!DNL Query Editor]. Vous pouvez également utiliser la barre de recherche pour effectuer une recherche sur le nom d’une requête. Les recherches sont sensibles à la casse. |
| SQL | Premiers caractères de la requête SQL. Placez le pointeur de la souris sur le code pour afficher la requête entière. |
| Modifié par | Dernier utilisateur à avoir modifié la requête. Any user in your organization with access to [!DNL Query Service] can modify queries. |
| Dernière modification | Date et heure de la dernière modification apportée à la requête, dans le fuseau horaire du navigateur. |

## Journal

L’onglet **[!UICONTROL Journal]** fournit une liste de requêtes qui ont été exécutées précédemment. Par défaut, le journal répertorie les requêtes dans l’ordre chronologique décroissant.

![Image](../images/queries/ui-overview/log.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Nom de la requête, composé des premiers caractères de la requête SQL. Clicking on the name opens the [!DNL Query Editor], allowing you to edit the query. Vous pouvez utiliser la barre de recherche pour effectuer une recherche sur le nom d’une requête. Les recherches sont sensibles à la casse. |
| **[!UICONTROL Créée par]** | Nom de la personne qui a créé la requête. |
| **[!UICONTROL client]** | Client utilisé pour la requête. |
| **[!UICONTROL Jeu de données]** | Jeu de données d’entrée utilisé par la requête. Cliquez sur le jeu de données pour accéder à l’écran des détails du jeu de données d’entrée. |
| **[!UICONTROL État]** | État actuel de la requête. |
| **[!UICONTROL Dernière exécution]** | Moment de la dernière exécution de la requête. Vous pouvez trier la liste par ordre croissant ou décroissant en cliquant sur la flèche au-dessus de cette colonne. |
| **[!UICONTROL Temps d’exécution]** | Temps nécessaire pour l’exécution de la requête. |

## Informations d’identification

L’onglet **[!UICONTROL Informations d’identification]** affiche vos informations d’identification [!DNL Postgres] Cliquez sur l’icône **[!UICONTROL Copier]** en regard d’un champ pour stocker son contenu dans la mémoire tampon du clavier. Pour plus d’informations sur l’utilisation de ces informations d’identification pour établir une connexion avec des clients externes, consultez le [guide de connexion aux clients][connect-clients].

![Image](../images/queries/ui-overview/credentials.png)

## Étapes suivantes

Now that you are familiar with [!DNL Query Service] user interface on [!DNL Platform], you can access [!DNL Query Editor] to start creating your own query projects to share with other users in your organization. For more information on authoring and running queries in [!DNL Query Editor], see the [Query Editor user guide][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
