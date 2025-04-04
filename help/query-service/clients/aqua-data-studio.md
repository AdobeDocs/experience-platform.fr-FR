---
keywords: Experience Platform;accueil;rubriques populaires;query service;Query service;Aqua Data Studio;Aqua data studio;se connecter à query service;
solution: Experience Platform
title: Connecter Aqua Data Studio à Query Service
description: Ce document décrit les étapes à suivre pour connecter Aqua Data Studio à Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 8%

---

# Connecter [!DNL Aqua Data Studio] à Query Service

Ce document décrit les étapes à suivre pour connecter [!DNL Aqua Data Studio] à Adobe Experience Platform [!DNL Query Service].

## Commencer

Ce guide nécessite que vous ayez déjà accès à [!DNL Aqua Data Studio] et que vous sachiez comment naviguer dans son interface. Vous trouverez plus d’informations sur les [!DNL Aqua Data Studio] dans la [documentation [!DNL Aqua Data Studio] officielle](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Il existe des versions [!DNL Windows] et [!DNL macOS] de [!DNL Aqua Data Studio]. Les captures d’écran de ce guide ont été effectuées à l’aide de l’application de bureau [!DNL macOS]. Il peut y avoir des incohérences mineures dans l’interface utilisateur entre les versions.

Pour acquérir les informations d’identification nécessaires à la connexion de [!DNL Aqua Data Studio] à Experience Platform, vous devez avoir accès à l’espace de travail [!UICONTROL Requêtes] dans l’interface utilisateur d’Experience Platform. Veuillez contacter l’administrateur de votre organisation si vous n’avez pas actuellement accès à l’espace de travail [!UICONTROL Requêtes].

## Enregistrement du serveur {#register-server}

Après avoir installé [!DNL Aqua Data Studio], vous devez d’abord enregistrer le serveur. Consultez la documentation officielle d’Aqua Data Studio pour obtenir des instructions sur la [lancement de la boîte [!DNL Register Server] dialogue](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) et [enregistrement du serveur](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Une fois que la boîte de dialogue **[!DNL Register Server]** s’affiche pour un serveur PostgresSQL, fournissez les détails suivants pour les paramètres du serveur.

- **[!DNL Name]** : nom de votre connexion. Il est recommandé de fournir un nom convivial pour reconnaître la connexion.
- **[!DNL Login Name]** : le nom d’utilisateur est votre identifiant d’organisation Experience Platform. Elle prend la forme de `ORG_ID@AdobeOrg`.
- **[!DNL Password]** : il s’agit d’une chaîne alphanumérique figurant dans le tableau de bord des informations d’identification [!DNL Query Service].
- **[!DNL Host and Port]** : point d’entrée de l’hôte et son port pour [!DNL Query Service]. Vous devez utiliser le port 80 pour vous connecter à [!DNL Query Service].
- **[!DNL Database]:** base de données qui sera utilisée. Utilisez la valeur pour les informations d’identification de l’interface utilisateur d’Experience Platform `dbname` : `prod:all`.

### [!DNL Query Service] des informations d’identification

Pour trouver vos informations d’identification, connectez-vous à l’interface utilisateur de [!DNL Experience Platform] et sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour obtenir des instructions complètes afin de trouver vos informations de connexion, hôte, port et nom de base de données, veuillez lire le [ guide des informations d’identification ](../ui/credentials.md).

[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation pour obtenir des [instructions complètes sur la génération et l’utilisation d’informations d’identification non expirantes](../ui/credentials.md#non-expiring-credentials).

### Définition du mode SSL

Vous devez ensuite définir la valeur du mode SSL sur `?sslmode=require`. Cette opération est effectuée à partir de l’onglet [!DNL Driver] de la boîte de dialogue [!DNL Edit Server Properties] . Consultez la documentation officielle d’Aqua Data Studio pour obtenir des instructions sur la [modification des propriétés du pilote](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) et [configuration de SSL pour [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Utilisez la barre de recherche pour rechercher la propriété `sslmode`.

>[!IMPORTANT]
>
>Consultez la [[!DNL Query Service] documentation SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge SSL pour les connexions tierces à Adobe Experience Platform Query Service et comment se connecter à l’aide `verify-full` mode SSL.

Après avoir saisi les détails de votre connexion, dans le même onglet, sélectionnez **[!DNL Test Connection]** pour vous assurer que vos informations d’identification fonctionnent correctement. Si le test de la connexion réussit, sélectionnez **[!DNL Save]** pour enregistrer le serveur. Une boîte de dialogue de confirmation s’affiche pour confirmer la connexion, tandis que l’icône de connexion apparaît sur le tableau de bord. Vous pouvez maintenant vous connecter au serveur et afficher ses objets de schéma.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser le **[!DNL Query Analyzer]** dans [!DNL Aqua Data Studio] pour exécuter et modifier des instructions SQL. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
