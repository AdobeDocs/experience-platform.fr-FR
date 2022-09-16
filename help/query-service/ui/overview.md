---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;requête;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Service
topic-legacy: guide
description: Adobe Experience Platform Query Service fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: a887c502213e96d6af90af0859da78c2984f89a7
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 42%

---

# Guide de l’interface utilisateur du [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS. Pour accéder à l’interface utilisateur d’[Adobe Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche.

## [!DNL Query Editor]

Le [!DNL Query Editor] permet d’écrire et d’exécuter des requêtes sans utiliser de client externe. Sélectionner **[!UICONTROL Créer une requête]** pour ouvrir le [!DNL Query Editor] et créez une requête. Vous pouvez également accéder au [!DNL Query Editor] en sélectionnant une requête dans le **[!UICONTROL Journal]** ou **[!UICONTROL Parcourir]** onglets. La sélection d’une requête exécutée ou enregistrée précédemment ouvre la [!DNL Query Editor] et afficher le SQL de la requête sélectionnée.

![Le tableau de bord Requêtes avec l’option Créer une requête mise en surbrillance.](../images/ui/overview/overview.png)

[!DNL Query Editor] fournit un espace de modification où vous pouvez commencer à saisir une requête. Au fur et à mesure que vous tapez, l’éditeur complète automatiquement les mots réservés SQL, les tables et les noms de champ dans les tables. Lorsque vous avez terminé d’écrire votre requête, sélectionnez l’option **Play** pour exécuter la requête. L’onglet **[!UICONTROL Console]** situé sous l’éditeur indique ce que fait actuellement , indiquant le moment où une requête a été renvoyée. [!DNL Query Service] L’onglet **[!UICONTROL Résultat]**, en regard de la Console, affiche les résultats de la requête. Voir [Guide de Query Editor](./user-guide.md) pour plus d’informations sur l’utilisation de la variable [!DNL Query Editor].

![Zoomé en vue de la variable [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Parcourir {#browse}

L’onglet **[!UICONTROL Parcourir]** affiche les requêtes enregistrées par les utilisateurs de votre organisation. Il est utile de les voir comme des projets de requêtes, car les requêtes enregistrées ici peuvent encore être en cours de construction. Les requêtes affichées dans l’onglet **[!UICONTROL Parcourir]** s’affichent également sous la forme de requêtes exécutées dans l’onglet **[!UICONTROL Journal]** si elles ont été exécutées par [!DNL Query Service].

![Un zoom dans l&#39;onglet Parcourir du tableau de bord Requêtes qui affiche plusieurs requêtes enregistrées.](../images/ui/overview/browse.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Nom de la requête créée par l’utilisateur. Vous pouvez sélectionner le nom d’ouverture de la requête dans le [!DNL Query Editor]. Vous pouvez également utiliser la barre de recherche pour effectuer une recherche sur le nom d’une requête. Les recherches sont sensibles à la casse. |
| **[!UICONTROL SQL]** | Premiers caractères de la requête SQL. Placez le pointeur de la souris sur le code pour afficher la requête entière. |
| **[!UICONTROL Modified by]** | Dernier utilisateur à avoir modifié la requête. Tout utilisateur de votre entreprise ayant accès à [!DNL Query Service] peut modifier des requêtes. |
| **[!UICONTROL Dernière modification]** | Date et heure de la dernière modification apportée à la requête, dans le fuseau horaire du navigateur. |

## Journal

L’onglet **[!UICONTROL Journal]** fournit une liste de requêtes qui ont été exécutées précédemment. Par défaut, le journal répertorie les requêtes dans l’ordre chronologique décroissant.

![Un zoom en vue de l&#39;onglet Journal du tableau de bord Requêtes qui affiche une liste des requêtes dans l&#39;ordre chronologique inverse.](../images/ui/overview/log.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Nom de la requête, composé des premiers caractères de la requête SQL. La sélection du nom ouvre la [!DNL Query Editor], ce qui vous permet de modifier la requête. Vous pouvez utiliser la barre de recherche pour effectuer une recherche sur le nom d’une requête. Les recherches sont sensibles à la casse. |
| **[!UICONTROL Créé par]** | Nom de la personne qui a créé la requête. |
| **[!UICONTROL client]** | Client utilisé pour la requête. |
| **[!UICONTROL Jeu de données]** | Jeu de données d’entrée utilisé par la requête. Sélectionnez le jeu de données pour accéder à l’écran des détails du jeu de données d’entrée. |
| **[!UICONTROL Statut]** | État actuel de la requête. |
| **[!UICONTROL Dernière exécution]** | Moment de la dernière exécution de la requête. Vous pouvez trier la liste par ordre croissant ou décroissant en sélectionnant la flèche au-dessus de cette colonne. |
| **[!UICONTROL Exécution]** | Temps nécessaire pour l’exécution de la requête. |

## Informations d’identification

Le **[!UICONTROL Informations d’identification]** affiche vos informations d’identification arrivant à expiration et non arrivant à expiration. Pour plus d’informations sur l’utilisation de ces informations d’identification pour se connecter à des clients externes, veuillez lire la section [guide des informations d’identification](../clients/overview.md).

![Le tableau de bord Requêtes avec l’onglet Informations d’identification surligné.](../images/ui/overview/credentials.png)

## Étapes suivantes

Maintenant que vous connaissez [!DNL Query Service] interface utilisateur de [!DNL Platform], vous pouvez accéder à [!DNL Query Editor] pour commencer à créer vos propres projets de requête à partager avec d’autres utilisateurs de votre entreprise. Pour plus d’informations sur la création et l’exécution de requêtes dans [!DNL Query Editor], reportez-vous à la section [[!DNL Query Editor] guide de l’utilisateur](./user-guide.md).