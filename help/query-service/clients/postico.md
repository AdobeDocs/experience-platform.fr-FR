---
keywords: Experience Platform;accueil;rubriques les plus consultées;Query service;query service;postico;Postico;se connecter à query service;
solution: Experience Platform
title: Connecter Postico à Query Service
description: Ce document contient le lien permettant d’installer le client de sauvegarde Postico pour Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 4%

---

# Connexion de [!DNL Postico] à Query Service (Mac)

Ce document décrit les étapes à suivre pour connecter [!DNL Postico] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Postico] et que vous savez comment naviguer dans son interface. Vous trouverez plus d’informations sur les [!DNL Postico] dans la [documentation [!DNL Postico] officielle](https://eggerapps.at/postico/docs).
> 
> En outre, [!DNL Postico] est **uniquement** disponible sur les appareils macOS.

Pour connecter [!DNL Postico] à Query Service, ouvrez [!DNL Postico] et sélectionnez **[!DNL New Favorite]**. La boîte de dialogue des paramètres de connexion s’affiche. À partir de là, vous pouvez saisir des valeurs de paramètre pour vous connecter à Adobe Experience Platform. Saisissez les paramètres de connexion répertoriés ci-dessous. Des instructions sur la manière de [se connecter à un serveur PostgreSQL avec Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) sont également disponibles sur le site web officiel de Postico.

| Paramètre de connexion | Description |
|---|---|
| **[!DNL Host]:** | Nom d’hôte du serveur PostgreSQL. |
| **[!DNL Port]:** | Port de [!DNL Query Service]. Vous devez utiliser le port **80** ou **5432** pour vous connecter à [!DNL Query Service]. |
| **[!DNL User]** | Créez un nom pour votre connexion spécifique. Laissez le champ vide pour utiliser votre nom d’utilisateur Mac. |
| **[!DNL Password]** | Cette chaîne alphanumérique correspond à vos informations d’identification Experience Platform **[!UICONTROL mot de passe]**. Si vous souhaitez utiliser des informations d’identification non expirantes, cette valeur correspond aux arguments concaténés des `technicalAccountID` et `credential` téléchargés dans le fichier de configuration JSON. La valeur du mot de passe se présente comme suit : {technicalAccountId}:{credential}. Le fichier JSON de configuration pour les informations d’identification non expirantes est un téléchargement unique pendant leur initialisation dont Adobe ne conserve pas de copie. |
| **[!DNL Database]** | Utilisez votre valeur d’informations d’identification Experience Platform **[!UICONTROL Base de données]** : `prod:all`. |

Pour plus d’informations sur la recherche du nom, de l’hôte, du port et des informations de connexion de votre base de données, consultez le guide [informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Experience Platform], puis sélectionnez **[!UICONTROL Requêtes]**, **[!UICONTROL Informations d’identification]**.

Après avoir inséré vos informations d’identification, sélectionnez **[!DNL Connect]** pour vous connecter à Query Service.

Après vous être connecté à Experience Platform, vous pourrez voir une liste de toutes les relations précédemment établies avec Query Service.

## Création d’instructions SQL

Pour créer une requête SQL, sélectionnez **[!DNL SQL Query]** dans la barre latérale. Vous pouvez également utiliser le raccourci clavier (⇧⌘T) pour accéder à la vue de la requête et saisir la requête à exécuter. Lorsque vous avez terminé, sélectionnez **[!DNL Execute Statement]** pour exécuter la requête. Un tableau s’affiche avec les résultats de l’exécution de la requête terminée.

Consultez la documentation officielle de Postico pour plus d’informations sur [l’utilisation de la vue de requête](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Postico] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
