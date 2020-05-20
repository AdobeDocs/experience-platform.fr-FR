---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’interface utilisateur d’Adobe Experience Platform Requête Service
topic: guide
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---


# Guide Requête Service

Adobe Experience Platform Requête Service fournit une interface utilisateur qui permet d’écrire et d’exécuter des requêtes, des vues de requêtes précédemment exécutées et d’accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS. Pour accéder à l’interface utilisateur d’ [Adobe Experience Platform][platform-ui], sélectionnez **Requêtes** dans le volet de navigation de gauche.

## Éditeur de Requête

L’éditeur de Requêtes vous permet d’écrire et d’exécuter des requêtes sans utiliser de client externe. Cliquez sur **Créer une Requête** pour ouvrir l’éditeur de Requête et créer une nouvelle requête. Vous pouvez également accéder à l’éditeur de Requêtes en sélectionnant une requête dans les onglets *Journal* ou *Parcourir* . La sélection d&#39;une requête précédemment exécutée ou enregistrée ouvre l&#39;éditeur de Requête et affiche le code SQL pour la requête sélectionnée.

![Image](../images/queries/ui-overview/overview.png)

L’éditeur de Requêtes offre un espace de modification dans lequel vous pouvez commencer à saisir une requête. Au fur et à mesure que vous tapez, l&#39;éditeur complète automatiquement les mots réservés SQL, les tables et les noms de champ dans les tables. Lorsque vous avez terminé d’écrire votre requête, cliquez sur **Lecture** pour exécuter la requête. L&#39;onglet *Console* situé sous l&#39;éditeur affiche ce que Requête Service est en train de faire, indiquant à quel moment une requête a été renvoyée. L&#39;onglet *Résultat* , en regard de la Console, affiche les résultats de la requête. Pour plus d’informations sur l’utilisation de l’éditeur de requêtes, consultez le guide [de l’éditeur de][query-editor] Requêtes.

![Image](../images/queries/ui-overview/query-editor.png)

## Parcourir

L’onglet *Parcourir* affiche les requêtes enregistrées par les utilisateurs de votre entreprise. Il est utile de les considérer comme des projets de requête, car les requêtes sauvées ici peuvent encore être en construction. Les Requêtes affichées dans l’onglet *Parcourir* s’affichent également sous forme de requêtes d’exécution dans l’onglet *Journal* si elles ont été exécutées précédemment par Requête Service.

![Image](../images/queries/ui-overview/browse.png)

| Colonne | Description |
| --- | --- |
| Nom | Nom de la requête créée par l’utilisateur. Vous pouvez cliquer sur le nom pour ouvrir la requête dans l’éditeur de Requêtes. Vous pouvez également utiliser la barre de recherche pour rechercher le nom d’une requête. Les recherches sont sensibles à la casse. |
| SQL | Les premiers caractères de la requête SQL. Placer le pointeur de la souris sur le code affiche la requête complète. |
| Modifié par | Dernier utilisateur qui a modifié la requête. Tout utilisateur de votre organisation ayant accès à Requête Service peut modifier des requêtes. |
| Dernière modification | Date et heure de la dernière modification apportée à la requête, dans le fuseau horaire du navigateur. |

## Journal

L&#39;onglet *Journal* fournit une liste de requêtes qui ont été exécutées précédemment. Par défaut, le journal liste les requêtes dans la chronologie inverse.

![Image](../images/queries/ui-overview/log.png)

| Colonne | Description |
| --- | --- |
| Nom | Nom de la requête, composé des premiers caractères de la requête SQL. Cliquez sur le nom pour ouvrir l’éditeur de Requêtes, ce qui vous permet de modifier la requête. Vous pouvez utiliser la barre de recherche pour rechercher le nom d’une requête. Les recherches sont sensibles à la casse. |
| Créé par | Nom de la personne qui a créé la requête. |
| Client | Client utilisé pour la requête. |
| Jeu de données | Jeu de données d’entrée utilisé par la requête. Cliquez sur le jeu de données pour accéder à l&#39;écran des détails du jeu de données d&#39;entrée. |
| État | Statut actuel de la requête. |
| Dernière exécution | Quand la requête a été exécutée en dernier. Vous pouvez trier la liste par ordre croissant ou décroissant en cliquant sur la flèche située au-dessus de cette colonne. |
| Durée d’exécution | Durée d’exécution de la requête. |

## Informations d&#39;identification

L’onglet *Informations d’identification* affiche vos informations d’identification Postgres. Cliquez sur l’icône **Copier** en regard d’un champ pour stocker son contenu dans la mémoire tampon du clavier. Pour plus d&#39;informations sur l&#39;utilisation de ces informations d&#39;identification pour établir une connexion avec des clients externes, consultez le guide [][connect-clients]Connexion avec les clients.

![Image](../images/queries/ui-overview/credentials.png)

## Étapes suivantes

Maintenant que vous connaissez l’interface utilisateur de Requête Service sur la plate-forme, vous pouvez accéder à l’éditeur de Requêtes pour début de création de vos propres projets de requête à partager avec d’autres utilisateurs de votre entreprise. Pour plus d&#39;informations sur la création et l&#39;exécution de requêtes dans l&#39;éditeur de Requêtes, consultez le guide [d&#39;utilisation de l&#39;éditeur de][query-editor]Requêtes.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
