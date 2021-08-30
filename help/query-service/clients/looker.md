---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;service de requête;observateur;observateur;se connecter au service de requête;
solution: Experience Platform
title: Connexion de Looker à Query Service
topic-legacy: connect
description: Ce document décrit les étapes à suivre pour connecter Looker à Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 13%

---

# Connecter [!DNL Looker] à Query Service

Ce document décrit les étapes de connexion de [!DNL Looker] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Looker] et que vous savez comment naviguer dans son interface. Vous trouverez plus d’informations sur [!DNL Looker] dans la [documentation  [!DNL Looker] officielle](https://docs.looker.com/).

Après vous être connecté à [!DNL Looker], sélectionnez **[!DNL Admin]**, puis **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

Sur cette page, sélectionnez **[!DNL New Connection]**.

![](../images/clients/looker/click-new-connection.png)

À partir de là, vous pouvez remplir les détails des paramètres de connexion.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** nom de la connexion.
- **[!DNL Dialect]:** dialecte utilisé pour la base de données SQL. [!DNL Query Service] utilise  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** le point de terminaison hôte et son port pour  [!DNL Query Service].
- **[!DNL Database]:** base de données qui sera utilisée.
- **[!DNL Username and Password]:** Les identifiants de connexion qui seront utilisés. Le nom d’utilisateur se présente sous la forme `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Pour plus d’informations sur la recherche de l’hôte et du port, du nom de la base de données et des informations de connexion, consultez le [guide des informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivie de **[!UICONTROL Informations d’identification]**.

Après avoir saisi les détails de votre connexion, sélectionnez **[!DNL Test These Settings]** pour vous assurer que vos informations d’identification fonctionnent correctement. Si tel est le cas, un message indiquant que vous pouvez vous connecter s’affiche ci-dessous. Si votre connexion est réussie, sélectionnez **[!DNL Add Connection]** pour créer votre connexion.

![](../images/clients/looker/click-test-connection.png)

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Looker] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
