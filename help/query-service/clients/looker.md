---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de Requête ; service de requête ; observateur ; observateur ; connexion au service de requête ;
solution: Experience Platform
title: Connexion à Looker
topic: connect
description: Ce document passe par les étapes de connexion de Looker à Adobe Experience Platform Requête Service.
translation-type: tm+mt
source-git-commit: bc1bbdddd75b11ac180b5e6faa391fd74e5f7e02
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 24%

---


# [!DNL Looker]

Ce document décrit les étapes de connexion de [!DNL Looker] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Looker] et que vous savez comment naviguer dans son interface. Vous trouverez plus d&#39;informations sur [!DNL Looker] dans la [documentation officielle [!DNL Looker] ](https://docs.looker.com/).

## Connecter [!DNL Looker] à la plate-forme

Après vous être connecté à [!DNL Looker], sélectionnez **[!DNL Admin]**, puis **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

Sur cette page, sélectionnez **[!DNL New Connection]**.

![](../images/clients/looker/click-new-connection.png)

A partir de là, vous pouvez remplir les détails des paramètres de connexion.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** nom de votre connexion.
- **[!DNL Dialect]:** dialecte utilisé pour la base de données SQL. [!DNL Query Service] utilise  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Point de terminaison hôte et son port pour  [!DNL Query Service].
- **[!DNL Database]:** base de données qui sera utilisée.
- **[!DNL Username and Password]:** Les identifiants de connexion qui seront utilisés. Le nom d’utilisateur se présente sous la forme `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Pour plus d’informations sur la manière de trouver l’hôte et le port, le nom de la base de données ainsi que les informations de connexion, consultez la [page des informations d’identification de Platform](https://platform.adobe.com/query/configuration). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, puis **[!UICONTROL Informations d’identification]**.

Après avoir saisi les détails de votre connexion, sélectionnez **[!DNL Test These Settings]** pour vous assurer que vos informations d’identification fonctionnent correctement. Si tel est le cas, un message indiquant que vous pouvez vous connecter s’affiche ci-dessous. Si votre connexion est effectivement réussie, sélectionnez **[!DNL Add Connection]** pour créer votre connexion.

![](../images/clients/looker/click-test-connection.png)

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Looker] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).