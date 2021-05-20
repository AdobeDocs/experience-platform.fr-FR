---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;Power BI;Power bi;se connecter au service de requête;
solution: Experience Platform
title: Connexion de Power BI à Query Service
topic-legacy: connect
description: Ce document décrit les étapes à suivre pour connecter Power BI à Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 2109abd02b9c6c321c21a8fe3826509d22b1c2e2
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 7%

---

# Connecter [!DNL Power BI] à Query Service (PC)

Ce document décrit les étapes de connexion de Power BI à Adobe Experience Platform Query Service.

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Power BI] et que vous savez comment naviguer dans son interface. Vous trouverez plus d’informations sur [!DNL Power BI] dans la [documentation  [!DNL Power BI] officielle](https://docs.microsoft.com/fr-FR/power-bi/).
>
> En outre, Power BI est **uniquement** disponible sur les périphériques Windows.

Une fois Power BI installé, vous devez installer `Npgsql`, un package de pilote .NET pour PostgreSQL. Vous trouverez plus d’informations sur Npgsql dans la [documentation Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Vous devez télécharger la version v4.0.10 ou antérieure, car les versions plus récentes génèrent des erreurs.

Sous &quot;[!DNL Npgsql GAC Installation]&quot; dans l’écran de configuration personnalisée, sélectionnez **[!DNL Will be installed on local hard drive]**.

Pour vous assurer que npgsql est correctement installé, redémarrez votre ordinateur avant de passer aux étapes suivantes.

## Connectez [!DNL Power BI] à [!DNL Query Service]

Pour connecter [!DNL Power BI] à [!DNL Query Service], ouvrez [!DNL Power BI] et sélectionnez **[!DNL Get Data]** dans le ruban du menu supérieur.

![](../images/clients/power-bi/open-power-bi.png)

Sélectionnez **[!DNL PostgreSQL database]**, suivi de **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Vous pouvez désormais saisir des valeurs pour le serveur et la base de données. Pour plus d’informations sur la manière dont trouver le nom, l’hôte et le port de la base de données ainsi que les informations d’identification de connexion, consultez la [page des informations d’identification sur Platform](https://platform.adobe.com/query/configuration). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivie de **[!UICONTROL Informations d’identification]**.

**[!DNL Server]** est l’hôte trouvé sous les détails de la connexion. Pour la production, ajoutez le port `:80` à la fin de la chaîne hôte. **[!DNL Database]** peut être &quot;all&quot; ou un nom de table de jeu de données.

De plus, vous pouvez sélectionner votre **[!DNL Data Connectivity mode]**. Sélectionnez **[!DNL Import]** pour afficher la liste de tous les tableaux disponibles ou **[!DNL DirectQuery]** pour créer directement une requête.

Pour en savoir plus sur le mode **[!DNL Import]**, consultez la section [aperçu et import d&#39;une table](#preview). Pour en savoir plus sur le mode **[!DNL DirectQuery]**, consultez la section sur la [création d’instructions SQL](#create). Sélectionnez **[!DNL OK]** après avoir confirmé les détails de votre base de données.

![](../images/clients/power-bi/connectivity-mode.png)

Une invite vous demandant votre nom d’utilisateur, votre mot de passe et vos paramètres d’application s’affiche. Renseignez ces détails, puis sélectionnez **[!DNL Connect]** pour passer à l’étape suivante.

![](../images/clients/power-bi/import-mode.png)

## Prévisualiser et importer un tableau {#preview}

Si vous avez sélectionné le mode **[!DNL Import]** , une boîte de dialogue s’affiche, affichant la liste de tous les tableaux disponibles. Sélectionnez le tableau à prévisualiser, suivi de **[!DNL Load]** pour importer le jeu de données dans [!DNL Power BI].

![](../images/clients/power-bi/preview-table.png)

Le tableau est maintenant importé dans Power BI.

![](../images/clients/power-bi/import-table.png)

## Création d’instructions SQL {#create}

Si vous avez sélectionné le mode **[!DNL DirectQuery]** , vous devrez remplir la section Options avancées avec la requête SQL que vous souhaitez créer.

Sous **[!DNL SQL statement]**, insérez la requête SQL que vous souhaitez créer. Assurez-vous que la case **[!DNL Include relationship columns]** est cochée. Une fois la requête rédigée, sélectionnez **[!DNL OK]** pour continuer.

![](../images/clients/power-bi/direct-query-mode.png)

Un aperçu de votre requête s’affiche. Sélectionnez **[!DNL Load]** pour afficher les résultats de la requête.

![](../images/clients/power-bi/preview-direct-query.png)

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Power BI] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, consultez le guide sur [l’exécution des requêtes](../best-practices/writing-queries.md).
