---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Connexion à Looker
topic: connect
description: Ce document passe par les étapes de connexion de Looker à Adobe Experience Platform Requête Service.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 71%

---


# Connect with [!DNL Looker]

To connect [!DNL Looker] with [!DNL Query Service] on Adobe Experience Platform, please follow the steps below:

After logging into [!DNL Looker], click on **[!UICONTROL Admin]**, followed by **[!UICONTROL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

Sur cette page, cliquez sur **Nouvelle connexion**.

![](../images/clients/looker/click-new-connection.png)

À partir de là, vous pouvez remplir les détails des paramètres de connexion.

![](../images/clients/looker/new-connection.png)

- **Nom** : le nom de la connexion.
- **Dialecte** : le dialecte utilisé pour la base de données SQL. [!DNL Query Service] utilise **[!DNL PostgreSQL]**.
- **Hôte et port** : le point de terminaison hôte et son port pour [!DNL Query Service].
- **Base de données** : la base de données qui sera utilisée.
- **Identifiant de connexion et mot de passe** : les informations de connexion qui seront utilisées. Le nom d’utilisateur se présente sous la forme `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Pour plus d’informations sur la manière de trouver l’hôte et le port, le nom de la base de données ainsi que les informations de connexion, consultez la [page des informations d’identification de Platform](https://platform.adobe.com/query/configuration). To find your credentials, log in to [!DNL Platform], click **[!UICONTROL Queries]**, then click **[!UICONTROL Credentials]**.

Après avoir saisi vos informations de connexion, cliquez sur **[!UICONTROL Tester ces paramètres]** pour vous assurer qu’elles fonctionnent correctement. Si c’est le cas, un message indiquant que vous pouvez vous connecter s’affiche en dessous. Si la connexion est établie, cliquez sur **[!UICONTROL Ajouter connexion]** pour créer votre connexion.

![](../images/clients/looker/click-test-connection.png)

## Étapes suivantes

Now that you&#39;ve connected with [!DNL Query Service], you can use [!DNL Looker] to write queries. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../creating-queries/creating-queries.md).