---
keywords: Experience Platform;accueil;rubriques populaires;query service;Query Service;Power BI;power bi;se connecter à query service;
solution: Experience Platform
title: Connecter Power BI à Query Service
description: Ce document décrit les étapes à suivre pour connecter Power BI à Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 89%

---

# Connecter [!DNL Power BI] à Query Service

Ce document décrit les étapes à suivre pour connecter [!DNL Power BI] Desktop à Adobe Experience Platform Query Service.

## Prise en main

Ce guide nécessite que vous ayez déjà accès à l’application [!DNL Power BI] Desktop et que vous sachiez comment naviguer dans son interface. Pour télécharger [!DNL Power BI] Desktop ou pour plus d’informations, consultez la [documentation officielle de  [!DNL Power BI] ](https://docs.microsoft.com/fr-FR/power-bi/).

>[!IMPORTANT]
>
> L’application [!DNL Power BI] Desktop est **uniquement** disponible sur les appareils Windows.

Pour acquérir les informations d’identification nécessaires à la connexion de [!DNL Power BI] à Experience Platform, vous devez avoir accès à l’espace de travail Requêtes dans l’interface utilisateur d’Experience Platform. Contactez l’administrateur ou administratrice de votre organisation si vous n’avez pas actuellement accès à l’espace de travail des requêtes.

## Connecter [!DNL Power BI] à Query Service {#connect-power-bi}

Pour connecter [!DNL Power BI] à Query Service, ouvrez [!DNL Power BI] et sélectionnez **[!DNL Get Data]** dans le ruban du menu supérieur. Ensuite, saisissez « [!DNL PostgreSQL] » dans la barre de recherche pour affiner la liste des sources de données. Dans les résultats qui s’affichent, sélectionnez **[!DNL PostgreSQL database]**, puis **[!DNL Connect]**.

La boîte de dialogue de base de données [!DNL PostgreSQL] s’affiche, vous demandant des valeurs pour votre serveur et votre base de données. Vous pouvez consulter des instructions supplémentaires sur la manière de [se connecter à la base de données PostgreSQL à partir de Power Query Desktop](https://learn.microsoft.com/fr-fr/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) dans la documentation de [!DNL PowerBI].

Ces valeurs requises proviennent de vos informations d’identification Adobe Experience Platform. Pour trouver vos informations d’identification, connectez-vous à l’interface utilisateur d’Experience Platform et sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour plus d’informations sur la manière dont trouver le nom, l’hôte et le port de votre base de données ainsi que vos informations d’identification de connexion, consultez le [guide des informations d’identification](../ui/credentials.md).

>[!IMPORTANT]
>
>En tant qu’utilisateur de Power BI ou de Tableau, vous pouvez connecter Customer Journey Analytics à vos outils BI à partir de l’onglet des informations d’identification de Query Service. Consultez la documentation des informations d’identification pour obtenir des instructions sur la [connexion de vos outils BI à Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

![L’espace de travail Requêtes Experience Platform avec l’onglet Informations d’identification et Informations d’identification arrivant à expiration en surbrillance.](../images/clients/power-bi/query-service-credentials-page.png)

Dans le champ **[!DNL Server]** de la boîte de dialogue [!DNL PostgreSQL database], saisissez la valeur de l’hôte trouvé dans la section [!UICONTROL Informations d’identification] de Query Service. Pour la production, ajoutez le port `:80` à la fin de la chaîne hôte. Par exemple : `made-up.platform-query.adobe.io:80`.

Le champ **[!DNL Database]** peut être « all » ou un nom de table de jeu de données. Par exemple : `prod:all`.

>[!IMPORTANT]
>
>Les structures de données imbriquées dans des outils de BI tiers peuvent être aplaties afin d’améliorer leur utilisation et réduire la charge de travail requise pour récupérer, analyser, transformer et présenter des données. Consultez la documentation relative à la[`FLATTEN` fonctionnalité](../key-concepts/flatten-nested-data.md) pour savoir comment activer ce paramètre lors de la connexion à une base de données.

### Mode Connectivité des données {#data-connectivity-mode}

Ensuite, vous pouvez sélectionner votre **[!DNL Data Connectivity mode]**. Dans la boîte de dialogue [!DNL PostgreSQL database], sélectionnez **[!DNL Import]** puis **[!DNL OK]** pour afficher la liste de toutes les tables disponibles, ou sélectionnez **[!DNL DirectQuery]** pour interroger directement la source de données sans importer ou copier directement des données dans [!DNL Power BI].

Pour en savoir plus sur le mode **[!DNL Import]**, consultez la section sur l’[importation d’un tableau](#import). Pour en savoir plus sur **[!DNL DirectQuery]**, consultez la section sur l’[interrogation d’un jeu de données sans importer de données](#direct-query).

Sélectionnez **[!DNL OK]** après avoir confirmé les détails de votre base de données.

### Authentification {#authentication}

Après avoir confirmé votre mode de connectivité des données, une invite vous demandant votre nom d’utilisateur, votre mot de passe et les paramètres de votre application s’affiche. Dans ce cas, le nom d’utilisateur est votre identifiant d’organisation et le mot de passe est votre jeton d’authentification. Les deux se trouvent sur la page des informations d’identification de Query Service.

Renseignez ces informations, puis sélectionnez **[!DNL Connect]** pour passer à l’étape suivante.

## Importer un tableau {#import}

En sélectionnant le **[!DNL Import]** [!DNL Data Connectivity mode], le jeu de données complet est importé, ce qui permet d’utiliser les tableaux et colonnes sélectionnés dans l’application [!DNL Power BI] Desktop en l’état.

>[!IMPORTANT]
>
>Pour afficher les modifications de données qui se sont produites depuis l’importation initiale, vous devez actualiser les données dans [!DNL Power BI] en important à nouveau le jeu de données complet.

Pour importer une table, saisissez les détails du serveur et de la base de données [comme décrit ci-dessus](#connect-power-bi) et sélectionnez le **[!DNL Import]**&#x200B;[!DNL Data Connectivity mode], puis **[!DNL OK]**. La boîte de dialogue [!DNL Navigator] apparaît, affichant une liste de tous les tableaux disponibles. Sélectionnez le tableau à prévisualiser, puis choisissez **[!DNL Load]** pour mettre le jeu de données dans Power BI. Le tableau est maintenant importé dans [!DNL Power BI].

L’application [Informations générales sur la connexion aux données dans PowerBi Desktop](https://learn.microsoft.com/fr-fr/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) est disponible dans la documentation officielle.

### Importer des tableaux à l’aide du SQL personnalisé

[!DNL Power BI] et d’autres outils tiers tels que [!DNL Tableau] ne permettent actuellement pas aux utilisateurs d’importer des objets imbriqués, tels que des objets XDM dans Experience Platform. Pour en tenir compte, [!DNL Power BI] vous permet d’utiliser du code SQL personnalisé pour accéder à ces champs imbriqués et créer une vue aplatie des données. [!DNL Power BI] charge ensuite cette vue aplatie des données précédemment imbriquées comme un tableau normal.

Dans la boîte de dialogue [!DNL PostgreSQL database], sélectionnez **[!DNL Advanced options]** pour saisir une requête SQL personnalisée dans la section **[!DNL SQL statement]**. Cette requête personnalisée doit être utilisée pour aplatir vos paires nom-valeur JSON dans un format de tableau. La documentation officielle fournit également des informations sur la manière de [connecter PowerBI à l’aide d’une instruction SQL dans les options avancées](https://learn.microsoft.com/fr-fr/power-query/connectors/postgresql#connect-using-advanced-options).

Après avoir saisi votre requête personnalisée, sélectionnez **[!DNL OK]** pour poursuivre la connexion à votre base de données. Consultez la section [authentification](#authentication) ci-dessus pour plus d’informations sur la connexion d’une base de données à partir de cette partie du workflow.

Une fois l’authentification terminée, un aperçu des données aplaties s’affiche dans le tableau de bord [!DNL Power BI] Desktop sous la forme d’un tableau. Le nom du serveur et le nom de la base de données sont répertoriés en haut de la boîte de dialogue. Sélectionnez **[!DNL Load]** pour terminer le processus d’importation.

Les visualisations peuvent désormais être modifiées et exportées à partir de l’application [!DNL Power BI] Desktop.

## Interroger le jeu de données sans importer les données {#direct-query}

Les requêtes **[!DNL DirectQuery]** [!DNL Data Connectivity mode] interrogent directement la source de données sans importer ni copier les données sur [!DNL Power BI] Desktop. En utilisant ce mode de connexion, vous pouvez actualiser toutes les visualisations avec les données actives via l’interface utilisateur. Toutefois, le temps nécessaire à la création ou à l’actualisation de la visualisation varie en fonction des performances de la source de données sous-jacente.

Plus d’informations sur [l’utilisation de  [!DNL DirectQuery]](https://learn.microsoft.com/fr-fr/power-bi/connect-data/desktop-use-directquery) ainsi qu’une discussion approfondie sur ses [options de connectivité, cas d’utilisation et limites](https://learn.microsoft.com/fr-fr/power-bi/connect-data/desktop-directquery-about) sont disponibles dans la documentation [!DNL PowerBI].

Pour utiliser ce [!DNL Data Connectivity mode], sélectionnez le bouton **[!DNL DirectQuery]** puis **[!DNL Advanced options]** pour saisir une requête SQL personnalisée dans la section **[!DNL SQL statement]**. Assurez-vous que **[!DNL Include relationship columns]** est sélectionné. Une fois la requête terminée, sélectionnez **[!DNL OK]** pour continuer.

Un aperçu de votre requête s’affiche. Sélectionnez **[!DNL Load]** pour afficher les résultats de la requête.

## Étapes suivantes

En lisant ce document, vous devez maintenant comprendre comment vous connecter à l’application [!DNL Power BI] Desktop et les différents modes de connexion aux données disponibles. Pour plus d’informations sur l’écriture et l’exécution de requêtes, reportez-vous aux [conseils pour l’exécution des requêtes](../best-practices/writing-queries.md).
