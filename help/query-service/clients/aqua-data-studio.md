---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Connexion avec Aqua Data Studio
topic: connect
description: Ce document décrit les étapes à suivre pour connecter Aqua Data Studio à Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 74%

---


# Connexion à [!DNL Aqua Data Studio]

Ce document passe en revue les étapes de connexion de [!DNL Aqua Data Studio] à Adobe Experience Platform [!DNL Query Service].

Après avoir installé [!DNL Aqua Data Studio], vous devez d&#39;abord enregistrer le serveur. Dans le menu principal, cliquez sur **[!UICONTROL Serveur]**, puis sur **[!UICONTROL Enregistrer le serveur]**.

![](../images/clients/aqua-data-studio/register-server.png)

La boîte de dialogue **[!UICONTROL Enregistrer le serveur]** s’affiche. Sous l’onglet **[!UICONTROL Général]**, sélectionnez **[!UICONTROL PostgreSQL]** dans la liste de gauche. Dans la boîte de dialogue qui s’affiche, saisissez les détails suivants pour les paramètres du serveur.

- **[!UICONTROL Nom]** : le nom de la connexion.
- **[!UICONTROL Identifiant de connexion et mot de passe]** : Ies informations de connexion qui seront utilisées. Le nom d’utilisateur prend la forme `ORG_ID@AdobeOrg`.
- **[!UICONTROL Hôte et port]** : le point de terminaison hôte et son port pour [!DNL Query Service]. Vous devez utiliser le port 80 pour vous connecter à [!DNL Query Service].
- **[!UICONTROL Base de données] :** base de données qui sera utilisée.

>[!NOTE]
>
>Pour plus d’informations sur la façon de trouver vos informations de connexion, l’hôte, le port et le nom de la base de données, consultez la [page des informations d’identification de Platform](https://platform.adobe.com/query/configuration). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], cliquez sur **[!UICONTROL Requêtes]**, puis sur **[!UICONTROL Informations d’identification]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Sélectionnez l’onglet **[!UICONTROL Pilote]**. Sous **[!UICONTROL Paramètres]**, définissez la valeur sur `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Après avoir saisi les détails de votre connexion, cliquez sur **[!UICONTROL Tester la connexion]** pour vous assurer que vos informations d’identification fonctionnent correctement. Si vous réussissez à vous connecter, cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer votre serveur. La connexion s’affiche sur le **Tableau de bord** une fois l’enregistrement réussi, confirmant que vous pouvez désormais vous connecter au serveur et visualiser ses objets de schéma.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser l&#39;**[!UICONTROL analyseur de Requêtes]** dans [!DNL Aqua Data Studio] pour exécuter et modifier des instructions SQL. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).