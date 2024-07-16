---
keywords: Experience Platform;accueil;rubriques populaires;tableau;Tableau;service de requête;service de requête;se connecter au service de requête ;
solution: Experience Platform
title: Connexion de Tableau à Query Service
description: Ce document décrit les étapes à suivre pour connecter Tableau à Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 10%

---

# Connecter [!DNL Tableau] à Query Service

Ce document fournit des informations pour la connexion de [!DNL Tableau] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Tableau] et que vous savez naviguer dans son interface. Vous trouverez plus d&#39;informations sur [!DNL Tableau] dans la [documentation officielle [!DNL Tableau] 3}.](https://help.tableau.com/current/pro/desktop/en-us/default.htm)

Les instructions sur la [connexion à un serveur PostgreSQL avec Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) sont disponibles sur le site web officiel de Tableau. Une fois que la boîte de dialogue des paramètres de connexion s’affiche, saisissez vos informations d’identification Platform dans les champs de paramètre pour vous connecter à Adobe Experience Platform. Vous trouverez ci-dessous une liste des paramètres de connexion requis.

| Paramètre de connexion | Description |
|---|---|
| **[!DNL Server]** | Adresse de votre emplacement de stockage SFTP. Utilisez la valeur de vos informations d’identification **[!UICONTROL Host]** d’Experience Platform. |
| **[!DNL Port]:** | Port de [!DNL Query Service]. Vous devez utiliser le port **80** ou **5432** pour vous connecter à [!DNL Query Service]. |
| **[!DNL Database]** | Les bases de données auxquelles vous souhaitez accéder. Utilisez la valeur de vos informations d’identification **[!UICONTROL Base de données]** Experience Platform : `prod:all`. |
| **[!DNL Authentication]:** | Méthode choisie pour prouver l’identité de l’utilisateur. Il est recommandé de sélectionner [!DNL Username and Password] parmi les options disponibles du menu déroulant. |
| **[!DNL Username]** | Il s’agit de votre ID d’organisation Platform. Utilisez la valeur de vos informations d’identification d’Experience Platform **[!UICONTROL Username]**. L’ID sera au format `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Cette chaîne alphanumérique est votre identifiant Experience Platform **[!UICONTROL Password]**. Si vous souhaitez utiliser des informations d’identification qui n’expirent pas, cette valeur correspond aux arguments concaténés de `technicalAccountID` et de `credential` téléchargés dans le fichier JSON de configuration. La valeur du mot de passe se présente comme suit : {technicalAccountId}:{credential}. Le fichier de configuration JSON pour les informations d’identification non arrivant à expiration est un téléchargement unique lors de leur initialisation, dont Adobe ne conserve pas de copie. |

Pour plus d’informations sur la recherche de votre nom d’utilisateur, de votre mot de passe et de vos informations de connexion, consultez le [guide d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivi de **[!UICONTROL Informations d’identification]**.

>[!IMPORTANT]
>
>En tant qu’utilisateur Tableau ou Power BI, vous pouvez connecter Customer Journey Analytics à vos outils de BI à partir de l’onglet Informations d’identification de Query Service. Consultez la documentation des informations d’identification pour obtenir des instructions sur la [connexion de vos outils de BI à Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

Vérifiez que vous avez coché la case **[!UICONTROL Require SSL]** avant de tenter de vous connecter. Pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service, consultez la [documentation sur les modes SSL](./ssl-modes.md).

>[!IMPORTANT]
>
>Les structures de données imbriquées dans des outils de BI tiers peuvent être aplaties afin d’améliorer leur utilisation et réduire la charge de travail requise pour récupérer, analyser, transformer et présenter des données. Consultez la documentation relative à la[`FLATTEN` fonctionnalité](../key-concepts/flatten-nested-data.md) pour savoir comment activer ce paramètre lors de la connexion à une base de données.

Après avoir renseigné toutes vos informations d’identification, vérifiez vos paramètres pour continuer. Vous êtes maintenant connecté à Adobe Experience Platform.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Tableau] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, consultez le guide sur l’ [exécution de requêtes](../best-practices/writing-queries.md).
