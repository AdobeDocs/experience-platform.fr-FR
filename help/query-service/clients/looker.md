---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;service de requête;observateur;observateur;se connecter au service de requête;
solution: Experience Platform
title: Connexion de Looker à Query Service
description: Ce document décrit les étapes à suivre pour connecter Looker à Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 7%

---

# Connecter [!DNL Looker] à Query Service

Ce document décrit les étapes de connexion de [!DNL Looker] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Looker] et que vous savez naviguer dans son interface. Vous trouverez plus d&#39;informations sur [!DNL Looker] dans la [documentation officielle [!DNL Looker] 3}.](https://docs.looker.com/)

## Créer une connexion à une base de données {#create-connection}

Après vous être connecté à [!DNL Looker], sélectionnez **[!DNL Admin]**, suivi de **[!DNL Connections]**. La page [!DNL Connections] s’ouvre. Sur la page [!DNL Connections], sélectionnez **[!DNL Add Connection]**.

À partir de là, saisissez les détails des paramètres de connexion répertoriés ci-dessous. Consultez la documentation officielle de Looker pour obtenir des instructions [ sur la création d’une connexion à la base de données et des descriptions des propriétés disponibles ](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Nom de la connexion.
- **[!DNL Dialect]:** dialecte utilisé pour la base de données SQL. [!DNL Query Service] utilise **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Le point d’entrée hôte et son port pour [!DNL Query Service].
- **[!DNL Database]:** base de données qui sera utilisée.
- **[!DNL Username and Password]:** Les informations d’identification de connexion qui seront utilisées. Le nom d’utilisateur se présente sous la forme `ORG_ID@AdobeOrg`.
- **SSL** : activez SSL pour garantir une connexion sécurisée sur le réseau.

Pour trouver les informations d’identification nécessaires à la connexion de Looker à Query Service, connectez-vous à l’interface utilisateur de Platform et sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche, puis **[!UICONTROL Informations d’identification]**. Pour plus d&#39;informations sur la recherche de vos **identifiants**, **port**, **base de données**, **nom d&#39;utilisateur** et **mot de passe**, consultez le [guide d&#39;identification](../ui/credentials.md).

![La page Informations d’identification de l’espace de travail Requêtes Experience Platform avec les informations d’identification et les informations d’identification arrivant à expiration est mise en surbrillance.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation de [ instructions complètes sur la génération et l&#39;utilisation des informations d&#39;identification non arrivant à expiration ](../ui/credentials.md#non-expiring-credentials). Il est nécessaire de terminer ce processus si vous souhaitez connecter Looker en tant que configuration unique. Les valeurs `credential` et `technicalAccountId` acquises constituent la valeur du paramètre Looker `password` .

Pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces dans Adobe Experience Platform, consultez la [[!DNL Query Service] documentation SSL](./ssl-modes.md). Ce document fournit des instructions sur la connexion à l’aide du mode SSL `verify-full`.

Après avoir saisi les détails de votre connexion, sélectionnez **[!DNL Test These Settings]** pour vous assurer que vos informations d’identification fonctionnent correctement. Vous trouverez plus d’informations sur le [test de vos paramètres de connexion](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) dans la documentation officielle de Looker. Une fois la connexion établie, un message s’affiche à l’écran pour indiquer que vous pouvez vous connecter. Une fois la connexion établie, sélectionnez **[!DNL Add Connection]** pour créer la connexion.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Looker] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
