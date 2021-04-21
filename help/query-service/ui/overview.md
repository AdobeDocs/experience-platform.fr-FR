---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de requête ; service de Requête ; requête ; éditeur de requêtes ; éditeur de Requêtes ; éditeur de Requêtes ;
solution: Experience Platform
title: Guide de l’interface utilisateur de requête Service
topic-legacy: guide
description: Adobe Experience Platform Requête Service fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, des vues précédemment exécutées et accéder à des requêtes enregistrées par des utilisateurs au sein de votre organisation IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 59%

---

# [!DNL Query Service] guide

Le Adobe Experience Platform [!DNL Query Service] fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, des vues de requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS. Pour accéder à l’interface utilisateur d’[Adobe Experience Platform][platform-ui], sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche.

## [!DNL Query Editor]

[!DNL Query Editor] vous permet d&#39;écrire et d&#39;exécuter des requêtes sans utiliser de client externe. Cliquez sur **[!UICONTROL Créer une Requête]** pour ouvrir [!DNL Query Editor] et créer une nouvelle requête. Vous pouvez également accéder à [!DNL Query Editor] en sélectionnant une requête dans les onglets **[!UICONTROL Log]** ou **[!UICONTROL Parcourir]**. La sélection d&#39;une requête précédemment exécutée ou enregistrée ouvre [!DNL Query Editor] et affiche le code SQL pour la requête sélectionnée.

![Image](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] fournit un espace de modification dans lequel vous pouvez commencer à saisir une requête. Au fur et à mesure que vous tapez, l’éditeur complète automatiquement les mots réservés SQL, les tables et les noms des champs dans les tables. Lorsque vous avez terminé d’écrire votre requête, cliquez sur le bouton **Lecture** pour exécuter la requête. L’onglet **[!UICONTROL Console]** situé sous l’éditeur indique ce que fait actuellement , indiquant le moment où une requête a été renvoyée. [!DNL Query Service] L’onglet **[!UICONTROL Résultat]**, en regard de la Console, affiche les résultats de la requête. Consultez le [guide de l’éditeur de Requêtes][query-editor] pour plus d’informations sur l’utilisation de [!DNL Query Editor].

![Image](../images/queries/ui-overview/query-editor.png)

## Parcourir

L’onglet **[!UICONTROL Parcourir]** affiche les requêtes enregistrées par les utilisateurs de votre organisation. Il est utile de les voir comme des projets de requêtes, car les requêtes enregistrées ici peuvent encore être en cours de construction. Les requêtes affichées dans l’onglet **[!UICONTROL Parcourir]** s’affichent également sous la forme de requêtes exécutées dans l’onglet **[!UICONTROL Journal]** si elles ont été exécutées par [!DNL Query Service].

![Image](../images/queries/ui-overview/browse.png)

| Colonne | Description |
| --- | --- |
| Nom | Nom de la requête créée par l’utilisateur. Vous pouvez cliquer sur le nom pour ouvrir la requête dans [!DNL Query Editor]. Vous pouvez également utiliser la barre de recherche pour effectuer une recherche sur le nom d’une requête. Les recherches sont sensibles à la casse. |
| SQL | Premiers caractères de la requête SQL. Placez le pointeur de la souris sur le code pour afficher la requête entière. |
| Modifié par | Dernier utilisateur à avoir modifié la requête. Tout utilisateur de votre organisation ayant accès à [!DNL Query Service] peut modifier des requêtes. |
| Dernière modification | Date et heure de la dernière modification apportée à la requête, dans le fuseau horaire du navigateur. |

## Journal

L’onglet **[!UICONTROL Journal]** fournit une liste de requêtes qui ont été exécutées précédemment. Par défaut, le journal répertorie les requêtes dans l’ordre chronologique décroissant.

![Image](../images/queries/ui-overview/log.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Nom de la requête, composé des premiers caractères de la requête SQL. Cliquez sur le nom pour ouvrir la [!DNL Query Editor], ce qui vous permet de modifier la requête. Vous pouvez utiliser la barre de recherche pour effectuer une recherche sur le nom d’une requête. Les recherches sont sensibles à la casse. |
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

Maintenant que vous connaissez [!DNL Query Service] l&#39;interface utilisateur de [!DNL Platform], vous pouvez accéder à [!DNL Query Editor] au début de création de vos propres projets de requête à partager avec d&#39;autres utilisateurs de votre organisation. Pour plus d&#39;informations sur la création et l&#39;exécution de requêtes dans [!DNL Query Editor], consultez le [Guide de l&#39;utilisateur de l&#39;éditeur de Requêtes][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
