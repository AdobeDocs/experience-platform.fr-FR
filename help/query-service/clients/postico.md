---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;postico;Postico;se connecter au service de requête;
solution: Experience Platform
title: Connexion de Postico à Query Service
description: Ce document contient le lien d’installation du client de sauvegarde Postico pour Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 4%

---

# Connecter [!DNL Postico] à Query Service (Mac)

Ce document décrit les étapes de connexion de [!DNL Postico] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Postico] et que vous savez naviguer dans son interface. Vous trouverez plus d&#39;informations sur [!DNL Postico] dans la [documentation officielle [!DNL Postico] 3}.](https://eggerapps.at/postico/docs)
> 
> De plus, [!DNL Postico] est **uniquement** disponible sur les appareils macOS.

Pour connecter [!DNL Postico] à Query Service, ouvrez [!DNL Postico] et sélectionnez **[!DNL New Favorite]**. La boîte de dialogue des paramètres de connexion s’affiche. À partir de là, vous pouvez saisir des valeurs de paramètre pour vous connecter à Adobe Experience Platform. Renseignez les paramètres de connexion répertoriés ci-dessous. Les instructions pour [se connecter à un serveur PostgreSQL avec Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) sont également disponibles sur le site web officiel de Postico.

| Paramètre de connexion | Description |
|---|---|
| **[!DNL Host]:** | Nom d’hôte du serveur PostgreSQL. |
| **[!DNL Port]:** | Port de [!DNL Query Service]. Vous devez utiliser le port **80** ou **5432** pour vous connecter à [!DNL Query Service]. |
| **[!DNL User]** | Créez un nom pour votre connexion spécifique. Laissez le champ vide pour utiliser votre nom de connexion Mac. |
| **[!DNL Password]** | Cette chaîne alphanumérique est votre identifiant Experience Platform **[!UICONTROL Password]**. Si vous souhaitez utiliser des informations d’identification qui n’expirent pas, cette valeur correspond aux arguments concaténés de `technicalAccountID` et de `credential` téléchargés dans le fichier JSON de configuration. La valeur du mot de passe se présente comme suit : {technicalAccountId}:{credential}. Le fichier de configuration JSON pour les informations d’identification non arrivant à expiration est un téléchargement unique lors de leur initialisation, dont Adobe ne conserve pas de copie. |
| **[!DNL Database]** | Utilisez la valeur d&#39;identification **[!UICONTROL Database]** de votre Experience Platform : `prod:all`. |

Pour plus d’informations sur la recherche de votre nom de base de données, de votre hôte, de votre port et de vos informations de connexion, consultez le [guide d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivi de **[!UICONTROL Informations d’identification]**.

Après avoir inséré vos informations d’identification, sélectionnez **[!DNL Connect]** pour vous connecter à Query Service.

Après la connexion à Platform, vous pourrez voir la liste de toutes les relations précédemment établies avec Query Service.

## Création d’instructions SQL

Pour créer une requête SQL, sélectionnez **[!DNL SQL Query]** dans la barre latérale. Vous pouvez également utiliser le raccourci clavier (⇧ ⌘ T) pour accéder au mode Requête et saisir la requête à exécuter. Lorsque vous avez terminé, sélectionnez **[!DNL Execute Statement]** pour exécuter la requête. Un tableau s’affiche avec les résultats de l’exécution de requête terminée.

Consultez la documentation officielle de Postico pour plus d’informations sur [à l’aide de la vue de requête ](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Postico] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
