---
keywords: Experience Platform;accueil;rubriques populaires;tableau;Tableau;query service;Query service;se connecter à query service;
solution: Experience Platform
title: Connexion de Tableau à Query Service
description: Ce document décrit les étapes à suivre pour connecter Tableau à Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 10%

---

# Connecter [!DNL Tableau] à Query Service

Ce document fournit des informations sur la connexion des [!DNL Tableau] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Tableau] et que vous savez comment naviguer dans son interface. Vous trouverez plus d’informations sur les [!DNL Tableau] dans la [documentation [!DNL Tableau] officielle](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Les instructions sur la [connexion à un serveur PostgreSQL avec Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) sont disponibles sur le site Web officiel de Tableau. Une fois que la boîte de dialogue des paramètres de connexion s’affiche, saisissez vos informations d’identification Experience Platform dans les champs de paramètre pour vous connecter à Adobe Experience Platform. Vous trouverez ci-dessous une liste des paramètres de connexion requis.

| Paramètre de connexion | Description |
|---|---|
| **[!DNL Server]** | Adresse de l’emplacement de stockage de votre SFTP. Utilisez la valeur de vos informations d’identification Experience Platform **[!UICONTROL hôte]**. |
| **[!DNL Port]:** | Port de [!DNL Query Service]. Vous devez utiliser le port **80** ou **5432** pour vous connecter à [!DNL Query Service]. |
| **[!DNL Database]** | La ou les bases de données auxquelles vous souhaitez accéder. Utilisez la valeur de vos informations d’identification Experience Platform **[!UICONTROL Base de données]** : `prod:all`. |
| **[!DNL Authentication]:** | Méthode choisie pour prouver l’identité de l’utilisateur. Il est recommandé de sélectionner [!DNL Username and Password] dans les options disponibles du menu déroulant. |
| **[!DNL Username]** | Il s’agit de votre identifiant d’organisation Experience Platform. Utilisez la valeur de vos informations d’identification Experience Platform **[!UICONTROL Nom d’utilisateur]**. L’ID aura le format `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Cette chaîne alphanumérique correspond à vos informations d’identification Experience Platform **[!UICONTROL mot de passe]**. Si vous souhaitez utiliser des informations d’identification non expirantes, cette valeur correspond aux arguments concaténés des `technicalAccountID` et `credential` téléchargés dans le fichier de configuration JSON. La valeur du mot de passe se présente comme suit : {technicalAccountId}:{credential}. Le fichier JSON de configuration pour les informations d’identification non expirantes est un téléchargement unique pendant leur initialisation dont Adobe ne conserve pas de copie. |

Pour plus d’informations sur la recherche de votre nom d’utilisateur, de votre mot de passe et de vos informations de connexion, veuillez lire le guide [informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Experience Platform], puis sélectionnez **[!UICONTROL Requêtes]**, **[!UICONTROL Informations d’identification]**.

>[!IMPORTANT]
>
>En tant qu’utilisateur de Tableau ou Power BI, vous pouvez connecter Customer Journey Analytics à vos outils BI à partir de l’onglet des informations d’identification de Query Service. Consultez la documentation des informations d’identification pour obtenir des instructions sur la [connexion de vos outils BI à Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

Assurez-vous d’avoir coché la case **[!UICONTROL Exiger SSL]** avant d’essayer de vous connecter. Consultez la [documentation sur les modes SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge SSL pour les connexions tierces à Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>Les structures de données imbriquées dans des outils de BI tiers peuvent être aplaties afin d’améliorer leur utilisation et réduire la charge de travail requise pour récupérer, analyser, transformer et présenter des données. Consultez la documentation relative à la[`FLATTEN` fonctionnalité](../key-concepts/flatten-nested-data.md) pour savoir comment activer ce paramètre lors de la connexion à une base de données.

Après avoir renseigné toutes vos informations d’identification, confirmez vos paramètres pour continuer. Vous êtes désormais connecté à Adobe Experience Platform.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Tableau] pour écrire des requêtes. Pour plus d’informations sur l’écriture et l’exécution de requêtes, consultez le guide sur l’[exécution de requêtes](../best-practices/writing-queries.md).
