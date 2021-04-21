---
keywords: Experience Platform ; accueil ; rubriques populaires ; tableau ; Tableau ; service de requête ; service de Requête ; connexion au service de requête ;
solution: Experience Platform
title: Connexion de Tableau à Requête Service
topic-legacy: connect
description: Ce document passe en revue les étapes de connexion de Tableau à Adobe Experience Platform Requête Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 11%

---

# Connecter [!DNL Tableau] au service de Requête

Ce document décrit les étapes de connexion de Tableau à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Tableau] et que vous savez comment naviguer dans son interface. Vous trouverez plus d&#39;informations sur [!DNL Tableau] dans la [documentation officielle [!DNL Tableau] ](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Pour connecter [!DNL Tableau] à [!DNL Query Service], ouvrez [!DNL Tableau], et dans la section **[!DNL To a Server]** sélectionnez **[!DNL More]** suivi de **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

Vous pouvez désormais entrer des valeurs pour vous connecter à Adobe Experience Platform. Pour plus d’informations sur la manière dont trouver le nom, l’hôte et le port de la base de données ainsi que les informations d’identification de connexion, consultez la [page des informations d’identification sur Platform](https://platform.adobe.com/query/configuration). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, puis **[!UICONTROL Informations d’identification]**.

Vérifiez que vous avez coché la case **[!UICONTROL SSL Required]** avant de tenter de vous connecter.

Après avoir rempli toutes vos informations d’identification, sélectionnez **[!DNL Sign In]** pour continuer.

![](../images/clients/tableau/sign-in.png)

Vous êtes maintenant connecté à Adobe Experience Platform, avec une liste de vos tables affichée sur le côté.

![](../images/clients/tableau/connected.png)

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Tableau] pour écrire des requêtes. Pour plus d&#39;informations sur la façon d&#39;écrire et d&#39;exécuter des requêtes, veuillez lire le guide sur les [requêtes en cours d&#39;exécution](../best-practices/writing-queries.md).
