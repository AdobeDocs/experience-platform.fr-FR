---
keywords: Experience Platform;accueil;rubriques populaires;tableau;Tableau;service de requête;service de requête;se connecter au service de requête ;
solution: Experience Platform
title: Connexion de Tableau à Query Service
topic-legacy: connect
description: Ce document décrit les étapes à suivre pour connecter Tableau à Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 0c20b19c4c34b29c46964d5d87a8646c61055b06
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---

# Connexion [!DNL Tableau] vers Query Service

Ce document décrit les étapes à suivre pour connecter Tableau à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Tableau] et connaissent comment naviguer dans son interface. Plus d’informations sur [!DNL Tableau] se trouve dans la variable [officiel [!DNL Tableau] documentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Pour se connecter [!DNL Tableau] to [!DNL Query Service], ouvrez [!DNL Tableau], et dans le **[!DNL To a Server]** section select **[!DNL More]** suivie de **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

Vous pouvez désormais saisir des valeurs pour vous connecter à Adobe Experience Platform. Pour plus d’informations sur la recherche du nom de la base de données, de l’hôte, du port et des informations de connexion, consultez la section [guide des informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivie de **[!UICONTROL Informations d’identification]**.

Vérifiez que vous avez coché la variable **[!UICONTROL SSL requis]** avant de tenter de se connecter.

>[!IMPORTANT]
>
>Voir [[!DNL Query Service] Documentation SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service et sur la connexion à l’aide de `verify-full` Mode SSL.

![](../images/clients/tableau/sign-in.png)

>[!IMPORTANT]
>
>Les structures de données imbriquées dans des outils de BI tiers peuvent être aplaties afin d’améliorer leur convivialité et de réduire la charge de travail requise pour récupérer, analyser, transformer et générer des rapports sur les données. Consultez la documentation relative à la[`FLATTEN` fonctionnalité](../best-practices/flatten-nested-data.md) pour savoir comment activer ce paramètre lors de la connexion à une base de données.

Après avoir renseigné toutes vos informations d’identification, sélectionnez **[!DNL Sign In]** pour continuer.

Vous êtes maintenant connecté à Adobe Experience Platform, avec une liste de vos tableaux affichés sur le côté.

![](../images/clients/tableau/connected.png)

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Tableau] pour écrire des requêtes. Pour plus d’informations sur l’écriture et l’exécution de requêtes, veuillez lire le guide sur [exécution de requêtes](../best-practices/writing-queries.md).
