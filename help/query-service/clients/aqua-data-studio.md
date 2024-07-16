---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;Aqua Data Studio;Aqua Data Studio;Aqua data studio;se connecter au service de requête ;
solution: Experience Platform
title: Connexion d’Aqua Data Studio à Query Service
description: Ce document décrit les étapes à suivre pour connecter Aqua Data Studio à Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 8%

---

# Connecter [!DNL Aqua Data Studio] à Query Service

Ce document décrit les étapes de connexion de [!DNL Aqua Data Studio] à Adobe Experience Platform [!DNL Query Service].

## Commencer

Ce guide nécessite que vous ayez déjà accès à [!DNL Aqua Data Studio] et que vous sachiez comment naviguer dans son interface. Vous trouverez plus d&#39;informations sur [!DNL Aqua Data Studio] dans la [documentation officielle [!DNL Aqua Data Studio] 3}.](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1)

>[!NOTE]
>
>Il existe [!DNL Windows] et [!DNL macOS] versions de [!DNL Aqua Data Studio]. Des captures d’écran de ce guide ont été effectuées à l’aide de l’appli de bureau [!DNL macOS]. Il peut y avoir des incohérences mineures dans l’interface utilisateur entre les versions.

Pour obtenir les informations d’identification nécessaires à la connexion de [!DNL Aqua Data Studio] à l’Experience Platform, vous devez avoir accès à l’espace de travail [!UICONTROL Requêtes] dans l’interface utilisateur de Platform. Contactez l’administrateur de votre organisation si vous n’avez pas actuellement accès à l’espace de travail [!UICONTROL Requêtes].

## Enregistrement du serveur {#register-server}

Après l’installation de [!DNL Aqua Data Studio], vous devez d’abord enregistrer le serveur. Consultez la documentation officielle d’Aqua Data Studio pour savoir comment [lancer la  [!DNL Register Server] boîte de dialogue](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) et [enregistrer le serveur](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Une fois que la boîte de dialogue **[!DNL Register Server]** s’affiche pour un serveur PostgresSQL, fournissez les détails suivants pour les paramètres du serveur.

- **[!DNL Name]** : nom de la connexion. Il est recommandé de fournir un nom convivial pour reconnaître la connexion.
- **[!DNL Login Name]** : le nom de connexion est votre ID d’organisation de plateforme. Il prend la forme `ORG_ID@AdobeOrg`.
- **[!DNL Password]** : il s’agit d’une chaîne alphanumérique figurant dans le tableau de bord des informations d’identification [!DNL Query Service].
- **[!DNL Host and Port]** : le point d’entrée hôte et son port pour [!DNL Query Service]. Vous devez utiliser le port 80 pour vous connecter à [!DNL Query Service].
- **[!DNL Database]:** base de données qui sera utilisée. Utilisez la valeur pour les informations d’identification de l’interface utilisateur de Platform `dbname` : `prod:all`.

### [!DNL Query Service] credentials

Pour trouver vos informations d’identification, connectez-vous à l’interface utilisateur [!DNL Platform] et sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche, puis **[!UICONTROL Informations d’identification]**. Pour obtenir des instructions complètes afin de trouver vos informations de connexion, l’hôte, le port et le nom de la base de données, consultez le [guide d’identification](../ui/credentials.md).

[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation de [ instructions complètes sur la génération et l&#39;utilisation des informations d&#39;identification non arrivant à expiration ](../ui/credentials.md#non-expiring-credentials).

### Définition du mode SSL

Ensuite, vous devez définir la valeur du mode SSL sur `?sslmode=require`. Cette opération est effectuée à partir de l’onglet [!DNL Driver] de la boîte de dialogue [!DNL Edit Server Properties]. Consultez la documentation officielle d’Aqua Data Studio pour savoir comment [modifier les propriétés du pilote](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) et [configurer SSL pour [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Utilisez la barre de recherche pour trouver la propriété `sslmode`.

>[!IMPORTANT]
>
>Consultez la [[!DNL Query Service] documentation SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service et sur la connexion à l’aide du mode SSL `verify-full`.

Après avoir saisi les détails de votre connexion, dans le même onglet, sélectionnez **[!DNL Test Connection]** pour vous assurer que vos informations d’identification fonctionnent correctement. Si votre test de connexion réussit, sélectionnez **[!DNL Save]** pour enregistrer votre serveur. Une boîte de dialogue de confirmation s’affiche pour confirmer la connexion et l’icône de connexion s’affiche sur le tableau de bord. Vous pouvez désormais vous connecter au serveur et afficher ses objets de schéma.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser **[!DNL Query Analyzer]** dans [!DNL Aqua Data Studio] pour exécuter et modifier des instructions SQL. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
