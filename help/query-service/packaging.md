---
title: Package Query Service
description: Le document suivant décrit l’emballage des fonctionnalités et des produits disponibles pour Query Service et met en évidence les différences entre les requêtes ad hoc et par lots.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 33b3534a2c3f9b5da54fa4f3897d1e107f7c1976
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 5%

---

# Package du service de requête

Ce document décrit les différents types de package et les fonctionnalités d’exécution de requête disponibles dans Query Service.

Adobe Experience Platform Query Service peut être divisé en deux fonctionnalités en fonction des modèles de requête qui peuvent être exécutés :

- Les **requêtes ad hoc** sont des requêtes SQL utilisées pour explorer les jeux de données ingérés à des fins de vérification, de validation, d’expérimentation, etc. Ces requêtes ne réécrivent pas de données dans le lac de données Experience Platform.
- Les **requêtes par lots** sont des requêtes SQL utilisées pour effectuer le traitement post-ingestion des jeux de données ingérés. Ces requêtes nettoient, mettent en forme, manipulent et enrichissent les données, dont les résultats sont réécrits dans le lac de données Experience Platform. Ces requêtes peuvent être planifiées, gérées et surveillées en tant que traitements par lots.

Les fonctionnalités de Query Service sont incluses avec les produits et modules complémentaires suivants :

- **Applications basées sur Experience Platform** (Adobe Real-Time Customer Data Platform, Adobe Customer Journey Analytics et Adobe Journey Optimizer) : l’accès à Query Service pour exécuter des requêtes ad hoc est fourni dès le départ avec chaque variation et niveau des applications basées sur Experience Platform.
- **[!DNL Data Distiller]** (package complémentaire pouvant être acheté avec Adobe Real-Time CDP, Customer Journey Analytics et Adobe Journey Optimizer) : l’accès à Query Service pour exécuter des requêtes par lots est fourni avec [!DNL Data Distiller].

## Droits {#entitlements}

Le tableau suivant décrit les droits clés de Query Service en fonction de leur package :

| Droits de Query Service | Ajout d’applications Experience Platform | Emballé avec [!DNL Data Distiller] |
|---|---|---|
| Modèle de requête pris en charge | Requêtes ad hoc uniquement | Requête par lots |
| Cas d’utilisation pris en charge | <ul><li>Exploration&#x200B;</li><li>Découverte de données&#x200B;</li><li>Validation des données</li><li>Expérimentation</li></ul> | <ul><li>Nettoyage</li><li>Mise en forme</li><li>Manipulation</li><li>Enrichissement</li></ul> |
| Sémantique prise en charge | <ul><li>Requêtes SELECT</li></ul> | <ul><li>Requêtes CTAS et ITAS</li></ul> |
| Durée Maximale D’Exécution | 10 minutes | 24 heures |
| Mesure de licence | **Simultanéité de l&#39;utilisateur de requête** : <ul><li>1 utilisateur simultané (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 utilisateurs simultanés (Customer Journey Analytics, Adobe Mix Modeler) &#x200B;</li></ul> **Simultanéité des requêtes** : <ul><li>1 requête en cours d’exécution (toutes les applications) &#x200B;</li></ul> **Vous pouvez acheter un module complémentaire supplémentaire de package d’utilisateurs de requêtes ad hoc** pour augmenter vos droits de requête ad hoc autorisés. <ul><li>+5 utilisateurs simultanés supplémentaires par pack</li><li>+1 requête d’exécution simultanée supplémentaire par pack</li></ul> | **Heures de calcul** : <ul><li>Variable (étendue en fonction des droits de votre application)</li></ul> Le **nombre d’heures de calcul** est une mesure du temps pris par le moteur de Query Service pour lire, traiter et écrire des données dans le lac de données lorsqu’une requête par lots est exécutée. <br>Avec le SKU Data Distiller, vous obtenez également un utilisateur supplémentaire et une simultanéité des requêtes, qui peut être utilisée pour l’exécution de requêtes ad hoc.  Le SKU de Data Distiller comprend les éléments suivants <br><ul><li>+5 utilisateurs simultanés supplémentaires</li><li>+1 requête supplémentaire en cours d’exécution</li></ul> |
| Utilisation accélérée des requêtes et des rapports | Non | Oui - Les requêtes accélérées simultanées vous permettent de lire les données de la boutique accélérée et de les afficher dans vos tableaux de bord. Un droit dédié pour le stockage des modèles de création de rapports et des jeux de données dans la boutique accélérée est également fourni. |
| Capacité de stockage du lac de données | Le droit total au stockage dépend de vos licences d’applications basées sur la plateforme. Par exemple, Real-Time CDP, AJO, CJA, etc. | Oui - Un droit d’enregistrement supplémentaire est fourni pour conserver vos jeux de données bruts et dérivés pour les cas d’utilisation de Data Distiller au-delà d’une date d’expiration de sept jours.<br>La capacité de stockage de votre lac de données est mesurée en téraoctets (To) et dépend de la quantité d’heures de calcul que vous avez achetées. Pour plus d’informations, consultez la description du produit . |
| Allocation d&#39;exportation de données | Le droit d’exportation total dépend de vos licences d’applications basées sur Platform. Par exemple, Real-Time CDP, AJO, CJA, etc. | Oui - Un droit d’exportation supplémentaire est fourni pour permettre l’exportation de jeux de données dérivés créés à l’aide de Data Distiller.<br>Votre allocation annuelle d’exportation de données est mesurée en téraoctets (To) et dépend de la quantité d’heures de calcul que vous avez achetées. Veuillez consulter la description du produit pour plus de détails. |
| Interface d’exécution de requête | <ul><li>Interface utilisateur de Query Service</li><li>Interface utilisateur du client tiers</li><li>Interface utilisateur du client [!DNL PostgresSQL]</li></ul> | <ul><li>Interface utilisateur de Query Service </li><li>Interface utilisateur du client tiers</li><li>Interface utilisateur du client [!DNL PostgresSQL]</li><li>API REST</li></ul> |
| Résultats De La Requête Renvoyés Via | Interface utilisateur du client | Jeu de données dérivé stocké dans le lac de données |
| Limite de résultat | <ul><li>Interface utilisateur de Query Service - Le nombre de lignes de sortie peut être [configuré avec un paramètre d’interface utilisateur](./ui/user-guide.md#result-count) compris entre 50 et 500 lignes.</li><li>Clients tiers - 50 000</li><li>[!DNL PostgresSQL] client - 50 000</li></ul> | Les requêtes CTAS et ITAS ne génèrent que des messages de réussite, car la sortie de la requête est stockée dans des jeux de données dérivés. |
| Capacité de lecture du jeu de données | Oui | Oui |
| Capacité en écriture du jeu de données | Non | Oui |
| Capacité de planification | Non | Oui |
| Capacité de surveillance | Oui | Oui |
| Capacité de configuration des alertes de requête | Non | Oui |

{style="table-layout:auto"}

## Contrôle d’accès {#access-control}

Le contrôle d’accès d’Experience Platform est géré à l’aide de [Adobe Admin Console](https://adminconsole.adobe.com/) où les profils de produit lient les utilisateurs à des autorisations et à des sandbox. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).

Consultez les documents [Gérer les autorisations pour un profil de produit](../access-control/ui/permissions.md) et [Gérer les utilisateurs pour un profil de produit](../access-control/ui/users.md) pour obtenir des instructions détaillées sur la demande d’accès aux autorisations de profil de produit

### Autorisations pertinentes pour Query Service {#query-service-permissions}

Pour utiliser Query Service, l’autorisation **[!DNL Manage Queries]** doit être activée dans Admin Console. Cette autorisation permet aux utilisateurs et utilisatrices d’exécuter des requêtes ad hoc et par lots.

Le tableau suivant décrit les effets de l’autorisation [!DNL Manage Queries] :

| Autorisation | Fonction |
|---|---|
| [!DNL Manage Queries] (sans autorisation d&#39;écriture) | Permet d’accéder à l’exécution de requêtes ad hoc |
| [!DNL Manage Queries] (avec autorisation en écriture) | Fournit un accès pour exécuter des requêtes par lots |

{style="table-layout:auto"}

### Autorisations SQL Insights pertinentes {#sql-insights-permissions}

Pour créer Data Distiller [SQL Insights](./data-distiller/sql-insights/overview.md) dans les tableaux de bord, les autorisations suivantes **doivent** doivent être activées dans Admin Console.

| Autorisation | Fonction |
|---|---|
| [!DNL View Custom Dashboard] | Fournit un accès en affichage aux tableaux de bord définis par l’utilisateur |
| [!DNL Manage Custom Dashboard] | Permet de gérer l’accès aux tableaux de bord définis par l’utilisateur |

{style="table-layout:auto"}

## Prise en charge des sandbox {#sandbox-support}

Les sandbox sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque instance Experience Platform prend en charge plusieurs sandbox de production et hors production, chacun conservant sa propre bibliothèque de ressources Experience Platform. Les sandbox hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter vos sandbox de production. Pour plus d’informations sur les sandbox, consultez la [présentation des sandbox](../sandboxes/home.md). Tous les droits de Query Service sont partagés dans tous les sandbox.

## Étapes suivantes

En lisant ce document, vous devriez mieux comprendre les différents types de packages et les fonctionnalités d’exécution de requête disponibles dans Query Service. Pour en savoir plus sur Query Service, tel que les cas d’utilisation bien connus du secteur, consultez la [ documentation sur les cas d’utilisation ](./use-cases/abandoned-browse.md). Pour des informations plus générales, consultez la [présentation de Query Service](./home.md).

