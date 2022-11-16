---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;requête;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Service
topic-legacy: guide
description: Adobe Experience Platform Query Service fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 3b6862dd3bb770df4a1549275f911dd81a178002
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 21%

---

# Guide de l’interface utilisateur du [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS. Pour accéder à l’interface utilisateur d’[Adobe Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche.

## [!DNL Query Editor]

Le [!DNL Query Editor] permet d’écrire et d’exécuter des requêtes sans utiliser de client externe. Sélectionner **[!UICONTROL Créer une requête]** pour ouvrir le [!DNL Query Editor] et créez une requête. Vous pouvez également accéder au [!DNL Query Editor] en sélectionnant une requête dans le **[!UICONTROL Journal]** ou **[!UICONTROL Modèles]** onglets. La sélection d’une requête exécutée ou enregistrée précédemment ouvre la [!DNL Query Editor] et afficher le SQL de la requête sélectionnée.

![Le tableau de bord Requêtes avec l’option Créer une requête mise en surbrillance.](../images/ui/overview/overview.png)

[!DNL Query Editor] fournit un espace de modification où vous pouvez commencer à saisir une requête. Au fur et à mesure que vous tapez, l’éditeur complète automatiquement les mots réservés SQL, les tables et les noms de champ dans les tables. Lorsque vous avez terminé d’écrire votre requête, sélectionnez l’option **Play** pour exécuter la requête. L’onglet **[!UICONTROL Console]** situé sous l’éditeur indique ce que fait actuellement , indiquant le moment où une requête a été renvoyée. [!DNL Query Service] L’onglet **[!UICONTROL Résultat]**, en regard de la Console, affiche les résultats de la requête. Voir [Guide de Query Editor](./user-guide.md) pour plus d’informations sur l’utilisation de la variable [!DNL Query Editor].

![Zoomé en vue de la variable [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Requêtes planifiées {#scheduled-queries}

Les requêtes qui ont déjà été enregistrées en tant que modèle peuvent être planifiées pour une exécution régulière. Lors de la planification d’une requête, vous pouvez choisir la fréquence des exécutions, la date de début et de fin, le jour de la semaine où la requête planifiée s’exécute, ainsi que le jeu de données vers lequel exporter la requête. Les plannings de requête sont définis à l’aide de Query Editor.

Pour savoir comment planifier une requête via l’interface utilisateur, reportez-vous à la section [guide des requêtes planifiées](./user-guide.md#scheduled-queries). Pour savoir comment ajouter des plannings à l’aide de l’API, veuillez lire le [guide de point de terminaison des requêtes planifiées](../api/scheduled-queries.md).

Une fois qu’une requête a été planifiée, elle apparaît dans la liste des requêtes planifiées de la variable [!UICONTROL Requêtes planifiées] . Vous trouverez des détails complets sur la requête, les exécutions, le créateur et les minutages en sélectionnant une requête planifiée dans la liste.

![L’espace de travail Requêtes avec l’onglet Requêtes planifiées mis en surbrillance et qui affiche des lignes de plannings de requête.](../images/ui/overview/scheduled-queries.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Le champ name correspond au nom du modèle ou aux premiers caractères de votre requête SQL. Toute requête créée à l’aide de l’interface utilisateur avec Query Editor est nommée dès le départ. Si la requête a été créée via l’API, alors le nom de la requête est un extrait de code SQL initial utilisé pour créer la requête. |
| **[!UICONTROL Modèle]** | Nom du modèle de la requête. Sélectionnez un nom de modèle pour accéder à l’éditeur de requêtes. Le modèle de requête est affiché dans Query Editor à des fins pratiques. S’il n’existe aucun nom de modèle, la ligne est marquée d’un trait d’union et il n’est pas possible de rediriger vers l’éditeur de requêtes pour afficher la requête. |
| **[!UICONTROL SQL]** | Fragment de la requête SQL. |
| **[!UICONTROL Fréquence d’exécution]** | Il s’agit de la cadence d’exécution de votre requête. Les valeurs disponibles sont les suivantes : `Run once` et `Scheduled`. Les requêtes peuvent être filtrées en fonction de leur fréquence d’exécution. |
| **[!UICONTROL Créé par]** | Nom de l’utilisateur qui a créé la requête. |
| **[!UICONTROL Créé]** | Horodatage de création de la requête, au format UTC. |
| **[!UICONTROL Horodatage de la dernière exécution]** | Horodatage le plus récent lors de l’exécution de la requête. Cette colonne indique si une requête a été exécutée conformément à son planning actuel. |
| **[!UICONTROL État de la dernière exécution]** | Etat de la dernière exécution de la requête. Les trois valeurs d’état sont les suivantes : `successful` `failed` ou `in progress`. |

Consultez la documentation pour plus d’informations sur la manière de [Surveillance des requêtes via l’interface utilisateur de Query Service](../monitor-queries.md).

## Modèles {#browse}

Le **[!UICONTROL Modèles]** affiche les requêtes enregistrées par les utilisateurs de votre entreprise. Il est utile de les voir comme des projets de requêtes, car les requêtes enregistrées ici peuvent encore être en cours de construction. Requêtes affichées sur la page **[!UICONTROL Modèles]** s’affichent également sous la forme de requêtes exécutées dans **[!UICONTROL Journal]** s’ils ont été exécutés précédemment par [!DNL Query Service].

![Un zoom dans l&#39;onglet Modèles du tableau de bord Requêtes qui affiche plusieurs requêtes enregistrées.](../images/ui/overview/templates.png)

| Colonne | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Le champ name est soit le nom de la requête créé par l&#39;utilisateur, soit les premiers caractères de votre requête SQL. Toute requête créée à l’aide de l’interface utilisateur avec Query Editor est nommée dès le départ. Si la requête a été créée via l’API, alors le nom de la requête est un extrait de code SQL initial utilisé pour créer la requête. Vous pouvez sélectionner le nom de la requête à ouvrir dans le [!DNL Query Editor]. Vous pouvez également utiliser la barre de recherche pour rechercher la variable [!UICONTROL Nom] d’une requête. Les recherches sont sensibles à la casse. |
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