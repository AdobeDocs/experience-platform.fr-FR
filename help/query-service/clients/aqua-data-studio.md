---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Connexion avec Aqua Data Studio
topic: connect
description: Ce document décrit les étapes à suivre pour connecter Aqua Data Studio à Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 74%

---


# Connect with [!DNL Aqua Data Studio]

This document walks through the steps for connecting [!DNL Aqua Data Studio] with Adobe Experience Platform [!DNL Query Service].

After installing [!DNL Aqua Data Studio], you must first register the server. Dans le menu principal, cliquez sur **[!UICONTROL Serveur]**, puis sur **[!UICONTROL Enregistrer le serveur]**.

![](../images/clients/aqua-data-studio/register-server.png)

La boîte de dialogue **[!UICONTROL Enregistrer le serveur]** s’affiche. Sous l’onglet **[!UICONTROL Général]**, sélectionnez **[!UICONTROL PostgreSQL]** dans la liste de gauche. Dans la boîte de dialogue qui s’affiche, saisissez les détails suivants pour les paramètres du serveur.

- **[!UICONTROL Nom]** : le nom de la connexion.
- **[!UICONTROL Identifiant de connexion et mot de passe]** : Ies informations de connexion qui seront utilisées. Le nom d’utilisateur prend la forme `ORG_ID@AdobeOrg`.
- **[!UICONTROL Hôte et port]** : le point de terminaison hôte et son port pour [!DNL Query Service]. Vous devez utiliser le port 80 pour vous connecter à [!DNL Query Service].
- **[!UICONTROL Base de données]:** Base de données qui sera utilisée.

>[!NOTE]
>
>Pour plus d’informations sur la façon de trouver vos informations de connexion, l’hôte, le port et le nom de la base de données, consultez la [page des informations d’identification de Platform](https://platform.adobe.com/query/configuration). To find your credentials, log in to [!DNL Platform], click **[!UICONTROL Queries]**, then click **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Sélectionnez l’onglet **[!UICONTROL Pilote]**. Sous **[!UICONTROL Paramètres]**, définissez la valeur sur `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Après avoir saisi les détails de votre connexion, cliquez sur **[!UICONTROL Tester la connexion]** pour vous assurer que vos informations d’identification fonctionnent correctement. Si vous réussissez à vous connecter, cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer votre serveur. La connexion s’affiche sur le *Tableau de bord* une fois l’enregistrement réussi, confirmant que vous pouvez désormais vous connecter au serveur et visualiser ses objets de schéma.

## Étapes suivantes

Now that you have connected to [!DNL Query Service], you can use the **[!UICONTROL Query Analyzer]** within [!DNL Aqua Data Studio] to execute and edit SQL statements. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../creating-queries/creating-queries.md).