---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;Aqua Data Studio;Aqua Data Studio;Aqua data studio;se connecter au service de requête ;
solution: Experience Platform
title: Connexion d’Aqua Data Studio à Query Service
description: Ce document décrit les étapes à suivre pour connecter Aqua Data Studio à Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 11%

---

# Connecter [!DNL Aqua Data Studio] à Query Service

Ce document décrit les étapes de connexion. [!DNL Aqua Data Studio] avec Adobe Experience Platform [!DNL Query Service].

## Prise en main

Ce guide nécessite que vous ayez déjà accès à [!DNL Aqua Data Studio] et vous familiariser avec la navigation dans son interface. Plus d’informations sur [!DNL Aqua Data Studio] se trouve dans la variable [officiel [!DNL Aqua Data Studio] documentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Il y a [!DNL Windows] et [!DNL macOS] versions de [!DNL Aqua Data Studio]. Les captures d’écran de ce guide ont été réalisées à l’aide de la méthode [!DNL macOS] application de bureau . Il peut y avoir des incohérences mineures dans l’interface utilisateur entre les versions.

Pour acquérir les informations d’identification nécessaires à la connexion de [!DNL Aqua Data Studio] à Experience Platform, vous devez avoir accès à l’espace de travail Requêtes dans l’interface utilisateur de Platform.  Contactez l’administrateur de votre entreprise si vous n’avez pas actuellement accès à la variable [!UICONTROL Requêtes] workspace.

## Enregistrement du serveur {#register-server}

Après installation [!DNL Aqua Data Studio], vous devez d’abord enregistrer le serveur. Consultez la documentation officielle d’Aqua Data Studio pour savoir comment [lancer la [!DNL Register Server] dialog](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) et [enregistrer le serveur ;](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Une fois que la variable **[!DNL Register Server]** s’affiche pour un serveur PostgresSQL. Indiquez les détails suivants pour les paramètres du serveur.

- **[!DNL Name]**: Nom de la connexion. Il est recommandé de fournir un nom convivial pour reconnaître la connexion.
- **[!DNL Login Name]**: Le nom de connexion est votre ID d’organisation de Platform. Il prend la forme de `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Chaîne alphanumérique figurant sur la variable [!DNL Query Service] tableau de bord des informations d’identification.
- **[!DNL Host and Port]**: Le point de terminaison hôte et son port pour [!DNL Query Service]. Vous devez utiliser le port 80 pour vous connecter à [!DNL Query Service].
- **[!DNL Database]:** La base de données qui sera utilisée. Utiliser la valeur des informations d’identification de l’interface utilisateur de Platform `dbname`: `prod:all`.

### [!DNL Query Service] informations

Pour trouver vos informations d’identification, connectez-vous au [!DNL Platform] Interface utilisateur et sélectionnez **[!UICONTROL Requêtes]** à partir du volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour obtenir des instructions complètes afin de trouver vos informations d’identification de connexion, l’hôte, le port et le nom de la base de données, veuillez lire la section [guide des informations d’identification](../ui/credentials.md).

[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation pour [instructions complètes sur la génération et l’utilisation des informations d’identification non arrivant à expiration](../ui/credentials.md#non-expiring-credentials).

### Définition du mode SSL

Ensuite, vous devez définir la valeur du mode SSL sur `?sslmode=require`. Cette opération s’effectue à partir de la fonction [!DNL Driver] de l’onglet [!DNL Edit Server Properties] boîte de dialogue. Consultez la documentation officielle d’Aqua Data Studio pour savoir comment [modification des propriétés du pilote](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) et [configuration de SSL pour [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Utilisez la barre de recherche pour trouver le `sslmode` .

>[!IMPORTANT]
>
>Voir [[!DNL Query Service] Documentation SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service et sur la connexion à l’aide de `verify-full` Mode SSL.

Après avoir saisi les détails de votre connexion, dans le même onglet, sélectionnez **[!DNL Test Connection]** pour vous assurer que vos informations d’identification fonctionnent correctement. Si le test de connexion réussit, sélectionnez **[!DNL Save]** pour enregistrer votre serveur. Une boîte de dialogue de confirmation s’affiche pour confirmer la connexion et l’icône de connexion s’affiche sur le tableau de bord. Vous pouvez désormais vous connecter au serveur et afficher ses objets de schéma.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser la variable **[!DNL Query Analyzer]** dans [!DNL Aqua Data Studio] pour exécuter et modifier des instructions SQL. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
