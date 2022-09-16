---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;postico;Postico;se connecter au service de requête;
solution: Experience Platform
title: Connexion de Postico à Query Service
topic-legacy: connect
description: Ce document contient le lien d’installation du client de sauvegarde Postico pour Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 7%

---

# Connexion [!DNL Postico] vers Query Service (Mac)

Ce document décrit les étapes de connexion. [!DNL Postico] avec Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Postico] et connaissent comment naviguer dans son interface. Plus d’informations sur [!DNL Postico] se trouve dans la variable [officiel [!DNL Postico] documentation](https://eggerapps.at/postico/docs).
> 
> En outre, [!DNL Postico] is **only** disponibles sur les appareils macOS.

Pour se connecter [!DNL Postico] à Query Service, ouvrez [!DNL Postico] et sélectionnez **[!DNL New Favorite]**.

![](../images/clients/postico/open-postico.png)

Vous pouvez désormais saisir des valeurs pour vous connecter à Adobe Experience Platform.

Pour plus d’informations sur la recherche du nom de la base de données, de l’hôte, du port et des informations de connexion, consultez la section [guide des informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivie de **[!UICONTROL Informations d’identification]**.

Après avoir inséré vos informations d’identification, sélectionnez **[!DNL Connect]** pour vous connecter à Query Service.

![](../images/clients/postico/authentication-details.png)

Après la connexion à Platform, vous pourrez voir la liste de toutes les relations précédemment établies avec Query Service.

![](../images/clients/postico/show-queries.png)

## Création d’instructions SQL

Pour créer une requête SQL, sélectionnez et ouvrez &quot;Requête SQL&quot;.

![](../images/clients/postico/create-query.png)

Une zone s’affiche et vous pouvez saisir la requête à exécuter à partir de celle-ci. Lorsque vous avez terminé, sélectionnez **[!DNL Execute Statement]** pour exécuter la requête.

![](../images/clients/postico/run-statement.png)

Un tableau s’affiche, indiquant les résultats de l’exécution de la requête terminée.

![](../images/clients/postico/query-results.png)

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Postico] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
