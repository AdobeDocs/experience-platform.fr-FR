---
keywords: Experience Platform; accueil;rubriques populaires;query service;Query Service;requête;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes;
solution: Experience Platform
title: Guide de l’IU de Query Service
description: Adobe Experience Platform Query Service fournit une interface utilisateur qui permet d’écrire et d’exécuter des requêtes, d’afficher des requêtes précédemment exécutées et d’accéder aux requêtes enregistrées par les utilisateurs de votre entreprise.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 71%

---

# Guide de l’interface utilisateur de [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs de votre organisation. Pour accéder à l’interface utilisateur d’[Adobe Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche.

## [!DNL Query Editor]

Le [!DNL Query Editor] vous permet d’écrire et d’exécuter des requêtes sans utiliser de client externe. Cliquez sur **[!UICONTROL Créer une requête]** pour ouvrir le [!DNL Query Editor] et créer une requête. Vous pouvez également accéder au [!DNL Query Editor] en sélectionnant une requête dans les onglets **[!UICONTROL Journal]** ou **[!UICONTROL Modèles]**. La sélection d’une requête exécutée ou enregistrée précédemment déclenche l’ouverture du [!DNL Query Editor] et affiche le code SQL de la requête sélectionnée.

![Le tableau de bord Requêtes avec l’option Créer une requête mise en surbrillance.](../images/ui/overview/overview.png)

[!DNL Query Editor] offre un espace d’édition dans lequel vous pouvez commencer à saisir une requête. Au fur et à mesure que vous tapez, l’éditeur complète automatiquement les mots réservés SQL, les tables et les noms des champs dans les tables. Une fois votre requête rédigée, cliquez sur le bouton **Lire** pour exécuter la requête. L’onglet **[!UICONTROL Console]** situé sous l’éditeur indique ce que fait actuellement [!DNL Query Service], indiquant le moment où une requête a été renvoyée. L’onglet **[!UICONTROL Résultat]**, en regard de la Console, affiche les résultats de la requête. Pour plus d’informations sur l’utilisation de [!DNL Query Editor], reportez-vous au [Guide d’utilisation de Query Editor](./user-guide.md).

![Un zoom sur le [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Requêtes planifiées {#scheduled-queries}

Les requêtes qui ont déjà été enregistrées en tant que modèle peuvent être planifiées pour une exécution régulière. Lors de la planification d’une requête, vous pouvez choisir la fréquence des exécutions, la date de début et de fin, le jour de la semaine où la requête planifiée s’exécute, ainsi que le jeu de données vers lequel exporter la requête. Les plannings de requête sont définis à l’aide de Query Editor.

Pour savoir comment planifier une requête via l’interface utilisateur, consultez le [guide des requêtes planifiées](./user-guide.md#scheduled-queries). Pour savoir comment ajouter des plannings à l’aide de l’API, veuillez lire le [guide de point d’entrée des requêtes planifiées](../api/scheduled-queries.md).

Une fois qu’une requête a été planifiée, elle apparaît dans la liste des requêtes planifiées de l’onglet [!UICONTROL Requêtes planifiées] . Vous trouverez des détails complets sur la requête, les exécutions, le créateur et les minutages en sélectionnant une requête planifiée dans la liste.

![ L’espace de travail Requêtes avec l’onglet Requêtes planifiées mis en surbrillance et affichant des lignes de plannings de requête.](../images/ui/overview/scheduled-queries.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Le champ nom correspond soit au nom du modèle, soit aux premiers caractères de votre requête SQL. Toute requête créée à l’aide de l’interface utilisateur avec le Query Editor est nommée dès le départ. Si la requête a été créée via l’API, le nom de la requête est un extrait du SQL initial utilisé pour créer la requête. |
| **[!UICONTROL Modèle]** | Nom du modèle de la requête. Sélectionnez un nom de modèle pour accéder à l’éditeur de requêtes. Le modèle de requête est affiché dans l’éditeur de requêtes pour plus de commodité. S’il n’existe aucun nom de modèle, la ligne est marquée d’un trait d’union et il n’est pas possible d’effectuer une redirection vers l’éditeur de requêtes pour afficher la requête. |
| **[!UICONTROL SQL]** | Fragment de la requête SQL. |
| **[!UICONTROL Fréquence d’exécution]** | Il s’agit de la cadence d’exécution de votre requête. Les valeurs disponibles sont `Run once` et `Scheduled`. Les requêtes peuvent être filtrées en fonction de leur fréquence d’exécution. |
| **[!UICONTROL Créé par]** | Nom de la personne qui a créé la requête. |
| **[!UICONTROL Créé]** | La date et l’heure de création de la requête, au format UTC. |
| **[!UICONTROL Horodatage de la dernière exécution]** | La date et l’heure les plus récentes auxquelles la requête a été exécutée. Cette colonne met en évidence si une requête a été exécutée conformément à son planning actuel. |
| **[!UICONTROL État de la dernière exécution]** | Statut de la dernière exécution de la requête. Les trois valeurs de statut sont les suivantes : `successful` `failed` ou `in progress`. |

Consultez la documentation pour plus d’informations sur la façon de [surveiller les requêtes via l’interface utilisateur de Query Service](./monitor-queries.md).

## Modèles {#browse}

L’onglet **[!UICONTROL Modèles]** affiche les requêtes enregistrées par les utilisateurs de votre organisation. Il est utile de les voir comme des projets de requêtes, car les requêtes enregistrées ici peuvent encore être en cours de construction. Les requêtes affichées dans l’onglet **[!UICONTROL Modèles]** s’affichent également sous la forme de requêtes exécutées dans l’onglet **[!UICONTROL Journal]** si elles ont été exécutées par [!DNL Query Service].

![Un zoom dans l’onglet Modèles du tableau de bord Requêtes qui affiche plusieurs requêtes enregistrées.](../images/ui/overview/templates.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Le nom du champ est soit le nom de la requête donné par l’utilisateur, soit les premiers caractères de votre requête SQL. Toute requête créée à l’aide de l’interface utilisateur avec le Query Editor est nommée dès le départ. Si la requête a été créée via l’API, le nom de la requête est un extrait du SQL initial utilisé pour créer la requête. Vous pouvez sélectionner le nom de la requête à ouvrir dans le [!DNL Query Editor]. Vous pouvez également utiliser la barre de recherche pour rechercher le [!UICONTROL nom] d’une requête. Les recherches sont sensibles à la casse. |
| **[!UICONTROL SQL]** | Premiers caractères de la requête SQL. Placez le pointeur de la souris sur le code pour afficher la requête entière. |
| **[!UICONTROL Modifié par]** | Dernier utilisateur à avoir modifié la requête. Tout utilisateur de votre organisation ayant accès à [!DNL Query Service] peut modifier les requêtes. |
| **[!UICONTROL Dernière modification]** | Date et heure de la dernière modification apportée à la requête, dans le fuseau horaire du navigateur. |

Pour plus d’informations sur les modèles dans l’interface utilisateur de Platform, consultez la documentation [Modèles de requête](./query-templates.md) .

## Journal {#log}

L’onglet **[!UICONTROL Journal]** fournit une liste de requêtes qui ont été exécutées précédemment. Par défaut, le journal répertorie les requêtes dans l’ordre chronologique décroissant.

![Un zoom de l’onglet Journal du tableau de bord Requêtes qui affiche une liste des requêtes dans l’ordre chronologique inverse.](../images/ui/overview/log.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Nom de la requête, composé des premiers caractères de la requête SQL. Sélectionnez le nom du modèle pour ouvrir la vue [!UICONTROL Détails du journal de requête] pour cette exécution. Vous pouvez utiliser la barre de recherche pour effectuer une recherche sur le nom d’une requête. Les recherches sont sensibles à la casse. |
| **[!UICONTROL Heure de début]** | Heure à laquelle la requête a été exécutée. |
| **[!UICONTROL Durée complète]** | Heure à laquelle la requête s’est exécutée. |
| **[!UICONTROL Statut]** | Statut actuel de la requête. |
| **[!UICONTROL Jeu de données]** | Jeu de données d’entrée utilisé par la requête. Cliquez sur le jeu de données pour accéder à l’écran des détails du jeu de données d’entrée. |
| **[!UICONTROL Client]** | Client utilisé pour la requête. |
| **[!UICONTROL Créé par]** | Nom de la personne qui a créé la requête. |

>
>
>Sélectionnez l’icône en forme de crayon (![Une icône en forme de crayon.](../images/ui/overview/edit-icon.png)) de n’importe quelle ligne du journal de requête pour accéder à [!DNL Query Editor]. La requête est prérenseignée pour faciliter la modification.

Pour plus d’informations sur les fichiers journaux générés automatiquement par un événement de requête, reportez-vous à la [documentation sur les journaux de requête](./query-logs.md) .

## Informations d’identification

L’onglet **[!UICONTROL Informations d’identification]** affiche vos informations d’identification arrivant à expiration et les autres. Pour plus d’informations sur l’utilisation de ces informations d’identification pour établir une connexion avec des clients externes, consultez le [guide des informations d’identification](../clients/overview.md).

![Le tableau de bord Requêtes avec l’onglet Informations d’identification mis en surbrillance.](../images/ui/overview/credentials.png)

## Étapes suivantes

Maintenant que vous connaissez l’interface utilisateur de [!DNL Query Service] sur [!DNL Platform], vous pouvez accéder à [!DNL Query Editor] pour créer vos propres projets de requêtes à partager avec d’autres utilisateurs de votre organisation. Pour plus d’informations sur la création et l’exécution de requêtes dans [!DNL Query Editor], consultez le guide d’utilisation de [[!DNL Query Editor] ](./user-guide.md).
