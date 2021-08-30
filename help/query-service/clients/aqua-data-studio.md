---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;Aqua Data Studio;Aqua Data Studio;Aqua data studio;se connecter au service de requête ;
solution: Experience Platform
title: Connexion d’Aqua Data Studio à Query Service
topic-legacy: connect
description: Ce document décrit les étapes à suivre pour connecter Aqua Data Studio à Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 20%

---

# Connecter [!DNL Aqua Data Studio] à Query Service

Ce document décrit les étapes de connexion de [!DNL Aqua Data Studio] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Aqua Data Studio] et que vous savez comment naviguer dans son interface. Vous trouverez plus d’informations sur [!DNL Aqua Data Studio] dans la [documentation  [!DNL Aqua Data Studio] officielle](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

Après avoir installé [!DNL Aqua Data Studio], vous devez d&#39;abord enregistrer le serveur. Dans le menu principal, sélectionnez **[!DNL Server]**, suivi de **[!DNL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

La boîte de dialogue **[!DNL Register Server]** s’affiche. Sous l’onglet **[!DNL General]** , sélectionnez **[!DNL PostgreSQL]** dans la liste de gauche. Dans la boîte de dialogue qui s’affiche, saisissez les détails suivants pour les paramètres du serveur.

- **[!DNL Name]**: Nom de la connexion.
- **[!DNL Login Name and Password]**: Les identifiants de connexion qui seront utilisés. Le nom d’utilisateur prend la forme `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**: Le point de terminaison hôte et son port pour  [!DNL Query Service]. Vous devez utiliser le port 80 pour vous connecter à [!DNL Query Service].
- **[!DNL Database]:** base de données qui sera utilisée.

>[!NOTE]
>
>Pour plus d’informations sur la manière de trouver vos informations de connexion, l’hôte, le port et le nom de la base de données, consultez le [guide des informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivie de **[!UICONTROL Informations d’identification]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Sélectionnez l’onglet **[!DNL Driver]** . Sous **[!DNL Parameters]**, définissez la valeur sur `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Après avoir saisi les détails de votre connexion, sélectionnez **[!DNL Test Connection]** pour vous assurer que vos informations d’identification fonctionnent correctement. Si la connexion est établie, sélectionnez **[!DNL Save]** pour enregistrer votre serveur. La connexion s’affiche sur le tableau de bord lors d’un enregistrement réussi, confirmant que vous pouvez désormais vous connecter au serveur et afficher ses objets de schéma.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser **[!DNL Query Analyzer]** dans [!DNL Aqua Data Studio] pour exécuter et modifier des instructions SQL. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
