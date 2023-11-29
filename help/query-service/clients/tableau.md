---
keywords: Experience Platform;accueil;rubriques populaires;tableau;Tableau;service de requête;service de requête;se connecter au service de requête ;
solution: Experience Platform
title: Connexion de Tableau à Query Service
description: Ce document décrit les étapes à suivre pour connecter Tableau à Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 12%

---

# Connecter [!DNL Tableau] à Query Service

Ce document fournit des informations sur la connexion. [!DNL Tableau] avec Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Tableau] et connaissent comment naviguer dans son interface. Plus d’informations sur [!DNL Tableau] se trouve dans la variable [officiel [!DNL Tableau] documentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Instructions sur la manière de procéder [Connexion à un serveur PostgreSQL avec Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) sont disponibles sur le site web officiel de Tableau. Une fois que la boîte de dialogue des paramètres de connexion s’affiche, saisissez vos informations d’identification Platform dans les champs de paramètre pour vous connecter à Adobe Experience Platform. Vous trouverez ci-dessous une liste des paramètres de connexion requis.

| Paramètre de connexion | Description |
|---|---|
| **[!DNL Server]** | Adresse de votre emplacement de stockage SFTP. Utiliser la valeur de votre Experience Platform **[!UICONTROL Hôte]** informations d’identification |
| **[!DNL Port]:** | Le port pour [!DNL Query Service]. Vous devez utiliser le port **80** ou **5432** pour vous connecter à [!DNL Query Service]. |
| **[!DNL Database]** | Les bases de données auxquelles vous souhaitez accéder. Utiliser la valeur de votre Experience Platform **[!UICONTROL Base]** credential : `prod:all`. |
| **[!DNL Authentication]:** | Méthode choisie pour prouver l’identité de l’utilisateur. Il est recommandé de sélectionner [!DNL Username and Password] dans les options disponibles du menu déroulant. |
| **[!DNL Username]** | Il s’agit de votre ID d’organisation Platform. Utiliser la valeur de votre Experience Platform **[!UICONTROL Nom d’utilisateur]** informations d’identification L’identifiant sera au format de `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Cette chaîne alphanumérique est votre Experience Platform **[!UICONTROL Password]** informations d’identification Si vous souhaitez utiliser des informations d’identification qui ne expirent pas, cette valeur correspond aux arguments concaténés du `technicalAccountID` et la variable `credential` téléchargé dans le fichier de configuration JSON. La valeur du mot de passe se présente comme suit : {technicalAccountId}:{credential}. Le fichier de configuration JSON pour les informations d’identification non arrivant à expiration est un téléchargement unique lors de leur initialisation, dont Adobe ne conserve pas de copie. |

Pour plus d’informations sur la recherche de votre nom d’utilisateur, de votre mot de passe et de vos informations de connexion, veuillez lire la section [guide des informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivie de **[!UICONTROL Informations d’identification]**.

Vérifiez que vous avez coché la variable **[!UICONTROL Require SSL]** avant de tenter de se connecter. Voir [Documentation sur les modes SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>Les structures de données imbriquées dans des outils de BI tiers peuvent être aplaties afin d’améliorer leur utilisation et réduire la charge de travail requise pour récupérer, analyser, transformer et présenter des données. Consultez la documentation relative à la[`FLATTEN` fonctionnalité](../key-concepts/flatten-nested-data.md) pour savoir comment activer ce paramètre lors de la connexion à une base de données.

Après avoir renseigné toutes vos informations d’identification, vérifiez vos paramètres pour continuer. Vous êtes maintenant connecté à Adobe Experience Platform.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Tableau] pour écrire des requêtes. Pour plus d’informations sur l’écriture et l’exécution de requêtes, veuillez lire le guide sur [exécution de requêtes](../best-practices/writing-queries.md).
