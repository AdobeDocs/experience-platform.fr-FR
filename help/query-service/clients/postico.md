---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de Requête ; service de requête ; postico ; Postico ; connexion au service de requête ;
solution: Experience Platform
title: Connecter Postico au service de Requête
topic-legacy: connect
description: Ce document contient le lien permettant d’installer le client de sauvegarde Postico pour Adobe Experience Platform Requête Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 16%

---

# Connectez [!DNL Postico] à Requête Service (Mac)

Ce document décrit les étapes de connexion de [!DNL Postico] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Postico] et que vous savez comment naviguer dans son interface. Vous trouverez plus d&#39;informations sur [!DNL Postico] dans la [documentation officielle [!DNL Postico] ](https://eggerapps.at/postico/docs).
> 
> De plus, [!DNL Postico] est **uniquement** disponible sur les périphériques macOS.

Pour connecter [!DNL Postico] à Requête Service, ouvrez [!DNL Postico] et sélectionnez **[!DNL New Favorite]**.

![](../images/clients/postico/open-postico.png)

Vous pouvez désormais entrer des valeurs pour vous connecter à Adobe Experience Platform.

Pour plus d’informations sur la manière dont trouver le nom, l’hôte et le port de la base de données ainsi que les informations d’identification de connexion, consultez la [page des informations d’identification sur Platform](https://platform.adobe.com/query/configuration). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, puis **[!UICONTROL Informations d’identification]**.

Après avoir inséré vos informations d’identification, sélectionnez **[!DNL Connect]** pour vous connecter à Requête Service.

![](../images/clients/postico/authentication-details.png)

Après la connexion à Platform, vous pourrez voir une liste de toutes les relations précédemment établies avec Requête Service.

![](../images/clients/postico/show-queries.png)

## Création d’instructions SQL

Pour créer une requête SQL, sélectionnez et ouvrez &quot;Requête SQL&quot;.

![](../images/clients/postico/create-query.png)

Une zone apparaît et vous pouvez saisir la requête à exécuter à partir de cette fenêtre. Lorsque vous avez terminé, sélectionnez **[!DNL Execute Statement]** pour exécuter la requête.

![](../images/clients/postico/run-statement.png)

Un tableau s’affiche, présentant les résultats de l’exécution de votre requête terminée.

![](../images/clients/postico/query-results.png)

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Postico] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
