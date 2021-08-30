---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;requête;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Service
topic-legacy: guide
description: Adobe Experience Platform Query Service fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 30c3ca4aa3e8f42140566c8fdf9fbc855ec72e1b
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 47%

---

# [!DNL Query Service] guide

Adobe Experience Platform [!DNL Query Service] fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS. Pour accéder à l’interface utilisateur d’[Adobe Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche.

## [!DNL Query Editor]

La fonction [!DNL Query Editor] permet d&#39;écrire et d&#39;exécuter des requêtes sans utiliser de client externe. Sélectionnez **[!UICONTROL Créer une requête]** pour ouvrir la [!DNL Query Editor] et créer une requête. Vous pouvez également accéder à [!DNL Query Editor] en sélectionnant une requête dans les onglets **[!UICONTROL Journal]** ou **[!UICONTROL Parcourir]**. La sélection d’une requête exécutée ou enregistrée précédemment ouvre la [!DNL Query Editor] et affiche le code SQL de la requête sélectionnée.

![Image](../images/ui/overview/overview.png)

[!DNL Query Editor] fournit un espace de modification où vous pouvez commencer à saisir une requête. Au fur et à mesure que vous tapez, l’éditeur complète automatiquement les mots réservés SQL, les tables et les noms de champ dans les tables. Lorsque vous avez terminé d’écrire votre requête, cliquez sur le bouton **Lire** pour exécuter la requête. L’onglet **[!UICONTROL Console]** situé sous l’éditeur indique ce que fait actuellement , indiquant le moment où une requête a été renvoyée. [!DNL Query Service] L’onglet **[!UICONTROL Résultat]**, en regard de la Console, affiche les résultats de la requête. Pour plus d’informations sur l’utilisation de [!DNL Query Editor], consultez le [guide de Query Editor](./user-guide.md) .

![Image](../images/ui/overview/query-editor.png)

## Parcourir

L’onglet **[!UICONTROL Parcourir]** affiche les requêtes enregistrées par les utilisateurs de votre organisation. Il est utile de les voir comme des projets de requêtes, car les requêtes enregistrées ici peuvent encore être en cours de construction. Les requêtes affichées dans l’onglet **[!UICONTROL Parcourir]** s’affichent également sous la forme de requêtes exécutées dans l’onglet **[!UICONTROL Journal]** si elles ont été exécutées par [!DNL Query Service].

![Image](../images/ui/overview/browse.png)

| Colonne | Description |
| --- | --- |
| Nom | Nom de la requête créée par l’utilisateur. Vous pouvez sélectionner le nom pour ouvrir la requête dans la balise [!DNL Query Editor]. Vous pouvez également utiliser la barre de recherche pour effectuer une recherche sur le nom d’une requête. Les recherches sont sensibles à la casse. |
| SQL | Premiers caractères de la requête SQL. Placez le pointeur de la souris sur le code pour afficher la requête entière. |
| Modifié par | Dernier utilisateur à avoir modifié la requête. Tout utilisateur de votre entreprise ayant accès à [!DNL Query Service] peut modifier des requêtes. |
| Dernière modification | Date et heure de la dernière modification apportée à la requête, dans le fuseau horaire du navigateur. |

## Journal

L’onglet **[!UICONTROL Journal]** fournit une liste de requêtes qui ont été exécutées précédemment. Par défaut, le journal répertorie les requêtes dans l’ordre chronologique décroissant.

![Image](../images/ui/overview/log.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Nom de la requête, composé des premiers caractères de la requête SQL. Le fait de sélectionner le nom ouvre la balise [!DNL Query Editor], ce qui vous permet de modifier la requête. Vous pouvez utiliser la barre de recherche pour effectuer une recherche sur le nom d’une requête. Les recherches sont sensibles à la casse. |
| **[!UICONTROL Créée par]** | Nom de la personne qui a créé la requête. |
| **[!UICONTROL client]** | Client utilisé pour la requête. |
| **[!UICONTROL Jeu de données]** | Jeu de données d’entrée utilisé par la requête. Sélectionnez le jeu de données pour accéder à l’écran des détails du jeu de données d’entrée. |
| **[!UICONTROL État]** | État actuel de la requête. |
| **[!UICONTROL Dernière exécution]** | Moment de la dernière exécution de la requête. Vous pouvez trier la liste par ordre croissant ou décroissant en sélectionnant la flèche au-dessus de cette colonne. |
| **[!UICONTROL Temps d’exécution]** | Temps nécessaire pour l’exécution de la requête. |

## Informations d’identification

L’onglet **[!UICONTROL Informations d’identification]** affiche à la fois les informations d’identification arrivant à expiration et non arrivant à expiration. Pour plus d’informations sur l’utilisation de ces informations d’identification pour se connecter à des clients externes, consultez le [guide des informations d’identification](../clients/overview.md).

![Image](../images/ui/overview/credentials.png)

## Étapes suivantes

Maintenant que vous connaissez l’interface utilisateur [!DNL Query Service] sur [!DNL Platform], vous pouvez accéder à [!DNL Query Editor] pour commencer à créer vos propres projets de requête à partager avec d’autres utilisateurs de votre entreprise. Pour plus d’informations sur la création et l’exécution de requêtes dans [!DNL Query Editor], consultez le [guide d’utilisation de Query Editor](./user-guide.md).