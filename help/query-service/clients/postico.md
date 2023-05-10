---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;postico;Postico;se connecter au service de requête;
solution: Experience Platform
title: Connexion de Postico à Query Service
description: Ce document contient le lien d’installation du client de sauvegarde Postico pour Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 8%

---

# Connexion [!DNL Postico] vers Query Service (Mac)

Ce document décrit les étapes de connexion. [!DNL Postico] avec Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Postico] et connaissent comment naviguer dans son interface. Plus d’informations sur [!DNL Postico] se trouve dans la variable [officiel [!DNL Postico] documentation](https://eggerapps.at/postico/docs).
> 
> En outre, [!DNL Postico] is **only** disponibles sur les appareils macOS.

Pour se connecter [!DNL Postico] à Query Service, ouvrez [!DNL Postico] et sélectionnez **[!DNL New Favorite]**. La boîte de dialogue des paramètres de connexion s’affiche. À partir de là, vous pouvez saisir des valeurs de paramètre pour vous connecter à Adobe Experience Platform. Renseignez les paramètres de connexion répertoriés ci-dessous. Instructions sur la manière de procéder [connexion à un serveur PostgreSQL avec Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) sont également disponibles sur le site officiel de Postico.

| Paramètre de connexion | Description |
|---|---|
| **[!DNL Host]:** | Nom d’hôte du serveur PostgreSQL. |
| **[!DNL Port]:** | Le port pour [!DNL Query Service]. Vous devez utiliser le port **80** ou **5432** pour vous connecter à [!DNL Query Service]. |
| **[!DNL User]** | Créez un nom pour votre connexion spécifique. Laissez le champ vide pour utiliser votre nom de connexion Mac. |
| **[!DNL Password]** | Cette chaîne alphanumérique est votre Experience Platform **[!UICONTROL Mot de passe]** informations d’identification. Si vous souhaitez utiliser des informations d’identification qui ne expirent pas, cette valeur correspond aux arguments concaténés du `technicalAccountID` et le `credential` téléchargé dans le fichier de configuration JSON. La valeur du mot de passe se présente comme suit : {technicalAccountId}:{credential}. Le fichier de configuration JSON pour les informations d’identification non arrivant à expiration est un téléchargement unique lors de leur initialisation, dont Adobe ne conserve pas de copie. |
| **[!DNL Database]** | Utilisez votre Experience Platform **[!UICONTROL Base]** valeur d’identification : `prod:all`. |

Pour plus d’informations sur la manière dont trouver le nom, l’hôte et le port de votre base de données ainsi que vos informations d’identification de connexion, consultez le [guide des informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivie de **[!UICONTROL Informations d’identification]**.

Après avoir inséré vos informations d’identification, sélectionnez **[!DNL Connect]** pour vous connecter à Query Service.

Après la connexion à Platform, vous pourrez voir la liste de toutes les relations précédemment établies avec Query Service.

## Création d’instructions SQL

Pour créer une requête SQL, sélectionnez **[!DNL SQL Query]** dans la barre latérale. Vous pouvez également utiliser le raccourci clavier (⇧ ⌘ T) pour accéder au mode Requête et saisir la requête à exécuter. Lorsque vous avez terminé, sélectionnez **[!DNL Execute Statement]** pour exécuter la requête. Un tableau s’affiche avec les résultats de l’exécution de requête terminée.

Consultez la documentation officielle de Postico pour plus d’informations sur [utilisation de la vue de requête](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Postico] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
