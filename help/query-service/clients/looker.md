---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;service de requête;observateur;observateur;se connecter au service de requête;
solution: Experience Platform
title: Connexion de Looker à Query Service
description: Ce document décrit les étapes à suivre pour connecter Looker à Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 7%

---

# Connexion [!DNL Looker] vers Query Service

Ce document décrit les étapes de connexion. [!DNL Looker] avec Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Looker] et connaissent comment naviguer dans son interface. Plus d’informations sur [!DNL Looker] se trouve dans la variable [officiel [!DNL Looker] documentation](https://docs.looker.com/).

## Création d’une connexion à une base de données {#create-connection}

Après vous être connecté à [!DNL Looker], sélectionnez **[!DNL Admin]**, suivie de **[!DNL Connections]**. Le [!DNL Connections] s’ouvre. Sur le [!DNL Connections] page, sélectionnez **[!DNL Add Connection]**.

À partir de là, saisissez les détails des paramètres de connexion répertoriés ci-dessous. Consultez la documentation officielle de Looker pour [instructions pour créer une connexion à la base de données et descriptions des propriétés disponibles](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Nom de la connexion.
- **[!DNL Dialect]:** Le dialecte utilisé pour la base de données SQL. [!DNL Query Service] uses **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Le point de terminaison hôte et son port pour [!DNL Query Service].
- **[!DNL Database]:** La base de données qui sera utilisée.
- **[!DNL Username and Password]:** Les identifiants de connexion qui seront utilisés. Le nom d’utilisateur se présente sous la forme `ORG_ID@AdobeOrg`.
- **SSL**: Activez SSL pour garantir une connexion sécurisée sur le réseau.

Pour trouver les informations d’identification nécessaires à la connexion de Looker à Query Service, connectez-vous à l’interface utilisateur de Platform et sélectionnez **[!UICONTROL Requêtes]** à partir du volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour plus d’informations sur la recherche de **hôte**, **port**, **base**, **username**, et **password** informations d’identification, veuillez lire [guide des informations d’identification](../ui/credentials.md).

![La page Informations d’identification de l’espace de travail Requêtes Experience Platform avec les informations d’identification et les informations d’identification arrivant à expiration est mise en surbrillance.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation pour [instructions complètes sur la génération et l’utilisation des informations d’identification non arrivant à expiration](../ui/credentials.md#non-expiring-credentials). Il est nécessaire de terminer ce processus si vous souhaitez connecter Looker en tant que configuration unique. Le `credential` et `technicalAccountId` les valeurs acquises constituent la valeur du Looker. `password` .

Pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces dans Adobe Experience Platform, voir [[!DNL Query Service] Documentation SSL](./ssl-modes.md). Ce document explique comment se connecter à l’aide de `verify-full` Mode SSL.

Une fois que vous avez saisi les détails de la connexion, sélectionnez **[!DNL Test These Settings]** pour vous assurer que vos informations d’identification fonctionnent correctement. Plus d’informations sur [test de vos paramètres de connexion](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) sont fournis dans la documentation officielle de Looker. Une fois la connexion établie, un message s’affiche à l’écran pour indiquer que vous pouvez vous connecter. Une fois la connexion établie, sélectionnez **[!DNL Add Connection]** pour créer votre connexion.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Looker] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
