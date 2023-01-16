---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;Power BI;Power bi;se connecter au service de requête;
solution: Experience Platform
title: Connexion de Power BI à Query Service
description: Ce document décrit les étapes à suivre pour connecter Power BI à Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 1%

---

# Connexion [!DNL Power BI] vers Query Service

Ce document décrit les étapes de connexion. [!DNL Power BI] Bureau avec Adobe Experience Platform Query Service.

## Prise en main

Ce guide nécessite que vous ayez déjà accès à la fonction [!DNL Power BI] de l’appli de bureau et connaissent comment naviguer dans son interface. Pour télécharger [!DNL Power BI] Bureau ou pour plus d’informations, voir [officiel [!DNL Power BI] documentation](https://docs.microsoft.com/fr-FR/power-bi/).

>[!IMPORTANT]
>
> Le [!DNL Power BI] L’appli de bureau est **only** disponible sur les périphériques Windows.

Pour acquérir les informations d’identification nécessaires à la connexion [!DNL Power BI] pour Experience Platform, vous devez avoir accès à l’espace de travail Requêtes dans l’interface utilisateur de Platform. Contactez l’administrateur de votre organisation si vous n’avez pas actuellement accès à l’espace de travail des requêtes.

Après installation [!DNL Power BI], vous devez installer . `Npgsql`, un package de pilote .NET pour PostgreSQL. Vous trouverez plus d’informations sur Npgsql dans la section [Documentation Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Vous devez télécharger la version v4.0.10 ou antérieure, car les versions plus récentes génèrent des erreurs.

Sous &quot;[!DNL Npgsql GAC Installation]&quot; sur l’écran de configuration personnalisé, sélectionnez **[!DNL Will be installed on local hard drive]**.

Pour vous assurer que Npgsql a été correctement installé, redémarrez votre ordinateur avant de passer aux étapes suivantes.

## Connexion [!DNL Power BI] vers Query Service {#connect-power-bi}

Pour se connecter [!DNL Power BI] à Query Service, ouvrez [!DNL Power BI] et sélectionnez **[!DNL Get Data]** dans le ruban du menu supérieur. Ensuite, saisissez &quot;[!DNL PostgreSQL]&quot; dans la barre de recherche pour limiter la liste des sources de données. Dans les résultats qui s’affichent, sélectionnez **[!DNL PostgreSQL database]**, suivie de **[!DNL Connect]**.

Le [!DNL PostgreSQL] la boîte de dialogue de base de données s’affiche, vous demandant des valeurs pour votre serveur et votre base de données. Instructions supplémentaires sur la manière de procéder [Connexion à une base de données PostgreSQL à partir de Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) peut être consulté dans la [!DNL PowerBI] documentation.

Ces valeurs requises proviennent de vos informations d’identification Adobe Experience Platform. Pour trouver vos informations d’identification, connectez-vous à l’interface utilisateur de Platform et sélectionnez **[!UICONTROL Requêtes]** à partir du volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour plus d’informations sur la recherche du nom de la base de données, de l’hôte, du port et des informations de connexion, consultez la section [guide des informations d’identification](../ui/credentials.md).

![L’espace de travail Requêtes Experience Platform avec l’onglet Informations d’identification et Informations d’identification arrivant à expiration est mis en surbrillance.](../images/clients/power-bi/query-service-credentials-page.png)

Dans le **[!DNL Server]** du champ [!DNL PostgreSQL database] boîte de dialogue, saisissez la valeur de l’hôte trouvé dans Query Service. [!UICONTROL Informations d’identification] . Pour la production, ajoutez le port `:80` à la fin de la chaîne hôte. Par exemple : `made-up.platform-query.adobe.io:80`.

Le **[!DNL Database]** peut être &quot;all&quot; ou un nom de table de jeu de données. Par exemple : `prod:all`.

>[!IMPORTANT]
>
>Les structures de données imbriquées dans des outils de BI tiers peuvent être aplaties afin d’améliorer leur convivialité et de réduire la charge de travail requise pour récupérer, analyser, transformer et générer des rapports sur les données. Consultez la documentation relative à la[`FLATTEN` fonctionnalité](../best-practices/flatten-nested-data.md) pour savoir comment activer ce paramètre lors de la connexion à une base de données.

### Mode Connectivité des données {#data-connectivity-mode}

Ensuite, vous pouvez sélectionner votre **[!DNL Data Connectivity mode]**. Dans le [!DNL PostgreSQL database] boîte de dialogue, sélectionnez **[!DNL Import]** suivie de **[!DNL OK]** pour afficher la liste de tous les tableaux disponibles, ou sélectionnez **[!DNL DirectQuery]** pour interroger directement la source de données sans importer ou copier directement des données dans [!DNL Power BI].

Pour en savoir plus sur la variable **[!DNL Import]** , veuillez lire la section sur [importation d&#39;un tableau](#import). Pour en savoir plus sur **[!DNL DirectQuery]** , veuillez lire la section sur [interrogation d’un jeu de données sans importer de données](#direct-query).

Sélectionner **[!DNL OK]** après avoir confirmé les détails de votre base de données.

### Authentification {#authentication}

Après avoir confirmé votre mode de connectivité des données, une invite vous demandant votre nom d’utilisateur, votre mot de passe et les paramètres de votre application s’affiche. Dans ce cas, le nom d’utilisateur est votre ID d’organisation et le mot de passe est votre jeton d’authentification. Les deux se trouvent sur la page des informations d’identification de Query Service.

Renseignez ces informations, puis sélectionnez **[!DNL Connect]** pour passer à l’étape suivante.

## Importer un tableau {#import}

En sélectionnant la variable **[!DNL Import]** [!DNL Data Connectivity mode], le jeu de données complet est importé, ce qui permet d’utiliser les tableaux et colonnes sélectionnés dans la variable [!DNL Power BI] application de bureau en l’état.

>[!IMPORTANT]
>
>Pour afficher les modifications de données qui se sont produites depuis l’importation initiale, vous devez actualiser les données dans [!DNL Power BI] en important à nouveau le jeu de données complet.

Pour importer un tableau, saisissez les détails du serveur et de la base de données. [comme décrit ci-dessus](#connect-power-bi) et sélectionnez la variable **[!DNL Import]** [!DNL Data Connectivity mode], suivie de **[!DNL OK]**. Le [!DNL Navigator] s’affiche, affichant une liste de tous les tableaux disponibles. Sélectionnez le tableau à prévisualiser, puis choisissez **[!DNL Load]** pour mettre en Power BI le jeu de données. Le tableau est maintenant importé dans [!DNL Power BI].

[Informations générales sur la connexion aux données dans PowerBi Desktop](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) L’application est disponible dans la documentation officielle.

### Importation de tableaux à l’aide de SQL personnalisé

[!DNL Power BI] et d’autres outils tiers tels que [!DNL Tableau] ne permettent pas actuellement aux utilisateurs d’importer des objets imbriqués, tels que des objets XDM dans Platform. Pour en tenir compte : [!DNL Power BI] vous permet d’utiliser du code SQL personnalisé pour accéder à ces champs imbriqués et créer une vue aplatie des données. [!DNL Power BI] charge ensuite cette vue aplatie des données précédemment imbriquées comme un tableau normal.

Dans la [!DNL PostgreSQL database] boîte de dialogue, sélectionnez **[!DNL Advanced options]** pour saisir une requête SQL personnalisée dans le **[!DNL SQL statement]** . Cette requête personnalisée doit être utilisée pour aplatir vos paires nom-valeur JSON dans un format de tableau. La documentation officielle fournit également des informations sur la manière de procéder. [connecter PowerBI à l’aide d’une instruction SQL dans les options avancées ;](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Après avoir saisi votre requête personnalisée, sélectionnez **[!DNL OK]** pour poursuivre la connexion à votre base de données. Voir [authentication](#authentication) pour plus d’informations sur la connexion d’une base de données à partir de cette partie du workflow.

Une fois l’authentification terminée, un aperçu des données aplaties s’affiche dans la [!DNL Power BI] Tableau de bord du bureau sous la forme d’un tableau. Le nom du serveur et du nom de la base de données sont répertoriés en haut de la boîte de dialogue. Sélectionner **[!DNL Load]** pour terminer le processus d’importation.

Les visualisations peuvent désormais être modifiées et exportées à partir du [!DNL Power BI] Application de bureau.

## Interrogation du jeu de données sans importation de données {#direct-query}

Le **[!DNL DirectQuery]** [!DNL Data Connectivity mode] interroge directement la source de données sans importer ou copier les données dans la variable [!DNL Power BI] Bureau. En utilisant ce mode de connexion, vous pouvez actualiser toutes les visualisations avec les données actives via l’interface utilisateur. Toutefois, le temps nécessaire à la création ou à l’actualisation de la visualisation varie en fonction des performances de la source de données sous-jacente.

Plus d’informations sur [l’utilisation de [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) ainsi qu&#39;une discussion approfondie sur son [options de connectivité, cas d’utilisation et limites](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) peut être consulté dans la [!DNL PowerBI] documentation.

Pour utiliser [!DNL Data Connectivity mode], sélectionnez la variable **[!DNL DirectQuery]** bascule puis **[!DNL Advanced options]** pour saisir une requête SQL personnalisée dans le **[!DNL SQL statement]** . Assurez-vous que **[!DNL Include relationship columns]** est sélectionnée. Une fois la requête terminée, sélectionnez **[!DNL OK]** pour continuer.

Un aperçu de votre requête s’affiche. Sélectionner **[!DNL Load]** pour afficher les résultats de la requête.

## Étapes suivantes

En lisant ce document, vous devez maintenant comprendre comment vous connecter à la [!DNL Power BI] Application de bureau et les différents modes de connexion aux données disponibles. Pour plus d’informations sur l’écriture et l’exécution de requêtes, reportez-vous à la section [conseils pour l’exécution des requêtes](../best-practices/writing-queries.md).
