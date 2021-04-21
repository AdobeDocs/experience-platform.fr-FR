---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de requête ; service de Requête ; Power BI ; alimentation ; connexion au service de requête ;
solution: Experience Platform
title: Connexion de Power BI à Query Service
topic-legacy: connect
description: Ce document passe par les étapes de connexion de Power BI avec Adobe Experience Platform Requête Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 6%

---

# Connectez [!DNL Power BI] à Requête Service (PC)

Ce document décrit les étapes de connexion de Power BI au service de Requête Adobe Experience Platform.

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL Power BI] et que vous savez comment naviguer dans son interface. Vous trouverez plus d&#39;informations sur [!DNL Power BI] dans la [documentation officielle [!DNL Power BI] ](https://docs.looker.com/).
>
> De plus, le Power BI est **uniquement** disponible sur les périphériques Windows.

Après avoir installé Power BI, vous devrez installer `Npgsql`, un package de pilotes .NET pour PostgreSQL. Pour plus d&#39;informations sur Npgsql, consultez la [documentation Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Vous devez télécharger la version 4.0.10 ou ultérieure, car les versions plus récentes génèrent des erreurs.

Sous &quot;[!DNL Npgsql GAC Installation]&quot; dans l’écran de configuration personnalisée, sélectionnez **[!DNL Will be installed on local hard drive]**.

Pour vous assurer que npgsql a été correctement installé, redémarrez votre ordinateur avant de passer aux étapes suivantes.

## Connecter [!DNL Power BI] à [!DNL Query Service]

Pour connecter [!DNL Power BI] à [!DNL Query Service], ouvrez [!DNL Power BI] et sélectionnez **[!DNL Get Data]** dans le ruban du menu supérieur.

![](../images/clients/power-bi/open-power-bi.png)

Sélectionnez **[!DNL PostgreSQL database]**, puis **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Vous pouvez désormais saisir des valeurs pour le serveur et la base de données. Pour plus d’informations sur la manière dont trouver le nom, l’hôte et le port de la base de données ainsi que les informations d’identification de connexion, consultez la [page des informations d’identification sur Platform](https://platform.adobe.com/query/configuration). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, puis **[!UICONTROL Informations d’identification]**.

**[!DNL Server]** est l&#39;hôte trouvé sous les détails de la connexion. Pour la production, ajoutez le port `:80` à la fin de la chaîne hôte. **[!DNL Database]** peut être &quot;all&quot; ou un nom de table de jeu de données.

De plus, vous pouvez sélectionner votre **[!DNL Data Connectivity mode]**. Sélectionnez **[!DNL Import]** pour afficher une liste de toutes les tables disponibles ou **[!DNL DirectQuery]** pour créer directement une requête.

Pour en savoir plus sur le mode **[!DNL Import]**, consultez la section [prévisualisation et importation d&#39;un tableau](#preview). Pour en savoir plus sur le mode **[!DNL DirectQuery]**, lisez la section [Création d&#39;instructions SQL](#create). Sélectionnez **[!DNL OK]** après avoir confirmé les détails de votre base de données.

![](../images/clients/power-bi/connectivity-mode.png)

Une invite vous demandant votre nom d’utilisateur, votre mot de passe et vos paramètres d’application s’affiche. Renseignez ces informations, puis sélectionnez **[!DNL Connect]** pour passer à l’étape suivante.

![](../images/clients/power-bi/import-mode.png)

## Prévisualisation et importation d’un tableau {#preview}

Si vous avez sélectionné le mode **[!DNL Import]**, une boîte de dialogue s&#39;affiche, affichant une liste de toutes les tables disponibles. Sélectionnez la table à prévisualisation, puis **[!DNL Load]** pour importer le jeu de données dans [!DNL Power BI].

![](../images/clients/power-bi/preview-table.png)

Le tableau est maintenant importé dans le Power BI.

![](../images/clients/power-bi/import-table.png)

## Créer des instructions SQL {#create}

Si vous avez sélectionné le mode **[!DNL DirectQuery]**, vous devrez remplir la section Options avancées avec la requête SQL que vous souhaitez créer.

Sous **[!DNL SQL statement]**, insérez la requête SQL à créer. Assurez-vous que la case **[!DNL Include relationship columns]** est cochée. Une fois que vous avez écrit votre requête, sélectionnez **[!DNL OK]** pour continuer.

![](../images/clients/power-bi/direct-query-mode.png)

Une prévisualisation de votre requête s&#39;affiche. Sélectionnez **[!DNL Load]** pour afficher les résultats de la requête.

![](../images/clients/power-bi/preview-direct-query.png)

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser [!DNL Power BI] pour écrire des requêtes. Pour plus d&#39;informations sur la façon d&#39;écrire et d&#39;exécuter des requêtes, veuillez lire le guide sur les [requêtes en cours d&#39;exécution](../best-practices/writing-queries.md).
