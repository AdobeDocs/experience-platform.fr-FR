---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;Aqua Data Studio;Aqua Data Studio;Aqua data studio;se connecter au service de requête ;
solution: Experience Platform
title: Connexion d’Aqua Data Studio à Query Service
topic-legacy: connect
description: Ce document décrit les étapes à suivre pour connecter Aqua Data Studio à Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 10%

---

# Connexion [!DNL Aqua Data Studio] vers Query Service

Ce document décrit les étapes de connexion. [!DNL Aqua Data Studio] avec Adobe Experience Platform [!DNL Query Service].

## Prise en main

Ce guide nécessite que vous ayez déjà accès à [!DNL Aqua Data Studio] et vous familiariser avec la navigation dans son interface. Plus d’informations sur [!DNL Aqua Data Studio] se trouve dans la variable [officiel [!DNL Aqua Data Studio] documentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Il y a [!DNL Windows] et [!DNL macOS] versions de [!DNL Aqua Data Studio]. Les captures d’écran de ce guide ont été réalisées à l’aide de la méthode [!DNL macOS] application de bureau . Il peut y avoir des incohérences mineures dans l’interface utilisateur entre les versions.

Pour acquérir les informations d’identification nécessaires à la connexion [!DNL Aqua Data Studio] pour être Experience Platform, vous devez avoir accès au [!UICONTROL Requêtes] dans l’interface utilisateur de Platform. Contactez votre administrateur de l’organisation IMS si vous n’avez pas actuellement accès à la variable [!UICONTROL Requêtes] workspace.

## Enregistrement du serveur {#register-server}

Après installation [!DNL Aqua Data Studio], vous devez d’abord enregistrer le serveur. Dans le menu principal, sélectionnez **[!DNL Server]**, suivie de **[!DNL Register Server]**.

![Le menu déroulant Serveur avec l’option Enregistrer le serveur en surbrillance.](../images/clients/aqua-data-studio/register-server.png)

Le **[!DNL Register Server]** s’affiche. Sous , **[!DNL General]** onglet, sélectionnez **[!DNL PostgreSQL]** dans la liste située à gauche. Dans la boîte de dialogue qui s’affiche, saisissez les détails suivants pour les paramètres du serveur.

- **[!DNL Name]**: Nom de la connexion. Il est recommandé de fournir un nom convivial pour reconnaître la connexion.
- **[!DNL Login Name]**: Le nom de connexion est votre ID d’organisation de Platform. Il prend la forme de `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Chaîne alphanumérique figurant sur la variable [!DNL Query Service] tableau de bord des informations d’identification.
- **[!DNL Host and Port]**: Le point de terminaison hôte et son port pour [!DNL Query Service]. Vous devez utiliser le port 80 pour vous connecter à [!DNL Query Service].
- **[!DNL Database]:** La base de données qui sera utilisée. Utiliser la valeur des informations d’identification de l’interface utilisateur de Platform `dbname`: `prod:all`.

![Le [!DNL Aqua Data Studio] Onglet Général avec les champs de saisie obligatoires en surbrillance.](../images/clients/aqua-data-studio/register-server-general-tab.png)

### [!DNL Query Service] informations

Pour trouver vos informations d’identification, connectez-vous au [!DNL Platform] Interface utilisateur et sélectionnez **[!UICONTROL Requêtes]** à partir du volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour obtenir des instructions complètes afin de trouver vos informations d’identification de connexion, l’hôte, le port et le nom de la base de données, veuillez lire la section [guide des informations d’identification](../ui/credentials.md).

[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation pour [instructions complètes sur la génération et l’utilisation des informations d’identification non arrivant à expiration](../ui/credentials.md#non-expiring-credentials).

### Définition du mode SSL

Sélectionnez ensuite le **[!DNL Driver]** . Sous **[!DNL Parameters]**, définissez la valeur sur `?sslmode=require`

>[!IMPORTANT]
>
>Voir [[!DNL Query Service] Documentation SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service et sur la connexion à l’aide de `verify-full` Mode SSL.

![Le [!DNL Aqua Data Studio] Onglet Pilote avec le champ Paramètres en surbrillance.](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Après avoir saisi les détails de votre connexion, sélectionnez **[!DNL Test Connection]** pour vous assurer que vos informations d’identification fonctionnent correctement. Si le test de connexion réussit, sélectionnez **[!DNL Save]** pour enregistrer votre serveur. Une boîte de dialogue de confirmation s’affiche pour confirmer la connexion et celle-ci s’affiche dans le tableau de bord. Vous pouvez désormais vous connecter au serveur et afficher ses objets de schéma.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser la variable **[!DNL Query Analyzer]** dans [!DNL Aqua Data Studio] pour exécuter et modifier des instructions SQL. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
