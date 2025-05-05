---
keywords: Experience Platform;accueil;rubriques les plus consultées;Query service;query service;Rechercheur;rechercheuse;se connecter à query service;
solution: Experience Platform
title: Connexion de la recherche à Query Service
description: Ce document décrit les étapes à suivre pour connecter Looker à Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 7%

---

# Connecter [!DNL Looker] à Query Service

Ce document décrit les étapes à suivre pour connecter [!DNL Looker] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Looker] et que vous savez comment naviguer dans son interface. Vous trouverez plus d’informations sur les [!DNL Looker] dans la [documentation [!DNL Looker] officielle](https://docs.looker.com/).

## Créer une connexion à la base de données {#create-connection}

Après vous être connecté à [!DNL Looker], sélectionnez **[!DNL Admin]**, puis **[!DNL Connections]**. La page [!DNL Connections] s’ouvre. Sur la page [!DNL Connections], sélectionnez **[!DNL Add Connection]**.

À partir de là, saisissez les détails des paramètres de connexion répertoriés ci-dessous. Consultez la documentation officielle sur Looker pour obtenir des [instructions sur la création d’une connexion à la base de données et des descriptions des propriétés disponibles](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Nom de la connexion.
- **[!DNL Dialect]:** dialecte utilisé pour la base de données SQL. [!DNL Query Service] utilise **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** point d’entrée hôte et son port pour [!DNL Query Service].
- **[!DNL Database]:** base de données qui sera utilisée.
- **[!DNL Username and Password]:** informations d’identification de connexion qui seront utilisées. Le nom d’utilisateur se présente sous la forme `ORG_ID@AdobeOrg`.
- **SSL** : activez SSL pour assurer une connexion sécurisée sur le réseau.

Pour trouver les informations d’identification nécessaires à la connexion de Looker à Query Service, connectez-vous à l’interface utilisateur d’Experience Platform et sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour plus d’informations sur la recherche de vos informations d’identification **hôte**, **port**, **base de données**, **nom d’utilisateur** et **mot de passe**, veuillez lire le guide [&#128279;](../ui/credentials.md) credentials.

![Page Informations d’identification de l’espace de travail Requêtes Experience Platform avec les Informations d’identification et les Informations d’identification arrivant à expiration en surbrillance.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation pour obtenir des [instructions complètes sur la génération et l’utilisation d’informations d’identification non expirantes](../ui/credentials.md#non-expiring-credentials). Il est nécessaire de terminer ce processus si vous souhaitez connecter Looker en tant que configuration ponctuelle. Les valeurs `credential` et `technicalAccountId` acquises comprennent la valeur du paramètre Looker `password`.

Pour en savoir plus sur la prise en charge SSL pour les connexions tierces dans Adobe Experience Platform, consultez la [[!DNL Query Service] documentation SSL](./ssl-modes.md). Ce document fournit des instructions sur la connexion à l’aide `verify-full` mode SSL.

Une fois que vous avez saisi les détails de votre connexion, sélectionnez **[!DNL Test These Settings]** pour vous assurer que vos informations d’identification fonctionnent correctement. Vous trouverez plus d’informations sur le [test des paramètres de connexion](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) dans la documentation officielle de Looker. Une fois la connexion établie, un message s’affiche à l’écran pour indiquer que vous pouvez vous connecter. Une fois la connexion établie, sélectionnez **[!DNL Add Connection]** pour créer la connexion.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Looker] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
