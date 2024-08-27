---
title: Packages de Query Service
description: Le document suivant décrit le regroupement des fonctionnalités et des produits disponibles pour Query Service et met en évidence les différences entre les requêtes ad hoc et les requêtes par lots.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 0970fd8fbea86115d92dc78cdba753da69cc2ee6
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 5%

---

# Package Query Service

Ce document décrit les différents types de fonctionnalités de création de package et d’exécution de requêtes disponibles dans Query Service.

Adobe Experience Platform Query Service peut être divisé en deux fonctionnalités basées sur les modèles de requête pouvant être exécutés :

- **Les requêtes ad hoc** sont des requêtes SQL utilisées pour explorer des jeux de données ingérés à des fins de vérification, de validation, d’expérimentation, etc. Ces requêtes n’écrivent pas de données dans le lac de données Platform.
- **Les requêtes par lots** sont des requêtes SQL utilisées pour effectuer le traitement post-ingestion des jeux de données ingérés. Ces requêtes nettoient, façonnent, manipulent et enrichissent des données, dont les résultats sont réécrits dans le lac de données Platform. Ces requêtes peuvent être planifiées, gérées et surveillées sous la forme de tâches par lots.

Les fonctionnalités de Query Service sont incluses dans les produits et modules complémentaires suivants :

- **Applications basées sur des plateformes** (Adobe Real-Time Customer Data Platform, Adobe Customer Journey Analytics et Adobe Journey Optimizer) : l’accès à Query Service pour exécuter des requêtes ad hoc est fourni dès le départ avec chaque variante et niveau d’applications basées sur des plateformes.
- **[!DNL Data Distiller]** (package de module complémentaire pouvant être acheté avec Adobe Real-Time CDP, Customer Journey Analytics et Adobe Journey Optimizer) : l’accès à Query Service pour exécuter des requêtes par lots est fourni avec [!DNL Data Distiller].

## Droits {#entitlements}

Le tableau suivant décrit les principaux droits de Query Service en fonction de leur mode de création :

| Droit de Query Service | Modules avec les applications basées sur Platform | Packé avec [!DNL Data Distiller] |
|---|---|---|
| Motif de requête pris en charge | Requêtes ad hoc uniquement | Requête par lots |
| Cas d’utilisation pris en charge | <ul><li>Exploration &#x200B;</li><li>&#x200B; de détection des données</li><li>Validation des données</li><li>Expérimentation</li></ul> | <ul><li>Nettoyage</li><li>Forme</li><li>Manipulation</li><li>Enrichir</li></ul> |
| Sémantique pris en charge | <ul><li>SELECT requêtes</li></ul> | <ul><li>Requêtes CTAS et ITAS</li></ul> |
| Durée maximale d’exécution | 10 minutes | 24 heures |
| Mesure de licence | **Condevise de l’utilisateur de requête** : <ul><li>1 utilisateur simultané (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 utilisateurs simultanés (Customer Journey Analytics) &#x200B;</li></ul> **Condevise de requête** : <ul><li>1 requête en cours d’exécution simultanée (toutes les applications) &#x200B;</li></ul> **Un module complémentaire d’utilisateurs de requête ad hoc** peut être acheté pour augmenter vos droits de requête ad hoc autorisés. <ul><li>+5 utilisateurs simultanés supplémentaires par pack</li><li>+1 requête d’exécution simultanée supplémentaire par pack</li></ul> | **Heures de calcul** : <ul><li>Variable (définie selon les droits de votre application)</li></ul> **Compute Hours** est une mesure du temps nécessaire au moteur Query Service pour lire, traiter et écrire des données dans le lac de données lors de l’exécution d’une requête par lots. <br>Avec le SKU de Data Distiller, vous obtenez également une simultanéité de requête et d’utilisateur supplémentaire, qui peut être utilisée pour l’exécution de requêtes ad hoc.  Le SKU du Distiller de données comprend :<br><ul><li>+5 utilisateurs simultanés supplémentaires</li><li>+1 requête en exécution simultanée supplémentaire</li></ul> |
| Utilisation accélérée des requêtes et des rapports | Non | Oui : les requêtes accélérées simultanées vous permettent de lire les données de la boutique accélérée et de les afficher dans vos tableaux de bord. Un droit dédié pour le stockage des modèles de rapports et des jeux de données dans le magasin accéléré est également fourni. |
| Capacité de stockage du lac de données | Le total de vos droits de stockage dépend des licences d’applications basées sur la plateforme. Par exemple, Real-Time CDP, AJO, CJA, etc. | Oui - Un droit de stockage supplémentaire est fourni pour conserver vos jeux de données bruts et dérivés pour les cas d’utilisation de Data Distiller au-delà d’une date d’expiration de données de sept jours.<br> La capacité de stockage de votre lac de données est mesurée en téraoctets (To) et dépend de la quantité d’heures de calcul que vous avez achetées. Pour plus d’informations, consultez la description du produit. |
| Frais d&#39;exportation de données | Le total de vos droits d’exportation dépend des licences d’applications basées sur la plateforme. Par exemple, Real-Time CDP, AJO, CJA, etc. | Oui - Un droit d’exportation supplémentaire est fourni pour permettre l’exportation des jeux de données dérivés créés à l’aide de Data Distiller.<br>Votre capacité d’exportation de données annuelle est mesurée en téraoctets (TB) et dépend de la quantité d’heures de calcul que vous avez achetées. Pour plus d’informations, consultez la description du produit. |
| Interface d’exécution de requête | <ul><li>Interface utilisateur de Query Service</li><li>Interface utilisateur cliente tierce</li><li>[!DNL PostgresSQL] interface utilisateur cliente</li></ul> | <ul><li>Interface utilisateur de Query Service </li><li>Interface utilisateur cliente tierce</li><li>[!DNL PostgresSQL] interface utilisateur cliente</li><li>API REST</li></ul> |
| Résultats de la requête renvoyés via | Interface utilisateur du client | Jeu de données dérivé stocké dans le lac de données |
| Limite de résultat | <ul><li>Interface utilisateur de Query Service : le nombre de lignes de sortie peut être [ configuré avec un paramètre d’interface utilisateur ](./ui/user-guide.md#result-count) entre 50 et 500 lignes.</li><li>Clients tiers - 50 000</li><li>[!DNL PostgresSQL] client - 50 000</li></ul> | Les requêtes CTAS et ITAS ne génèrent des messages de succès que lorsque la sortie de la requête est stockée dans des jeux de données dérivés. |
| Lecture de la capacité du jeu de données | Oui | Oui |
| Écriture de la capacité du jeu de données | Non | Oui |
| Capacité de planification | Non | Oui |
| Capacité de surveillance | Oui | Oui |
| Capacité de configuration des alertes de requête | Non | Oui |

{style="table-layout:auto"}

## Contrôle d’accès {#access-control}

Le contrôle d’accès pour les Experience Platform est géré par le [Adobe Admin Console](https://adminconsole.adobe.com/) où les profils de produit lient les utilisateurs à des autorisations et des environnements de test. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).

Pour obtenir des instructions détaillées sur la demande d’accès aux autorisations de profil de produit, consultez les documents [Gérer les autorisations d’un profil de produit](../access-control/ui/permissions.md) et [ Gérer les utilisateurs pour un profil de produit](../access-control/ui/users.md) .

### Autorisations de Query Service pertinentes {#query-service-permissions}

Pour utiliser Query Service, l’autorisation **[!DNL Manage Queries]** doit être activée dans Admin Console. Cette autorisation permet aux utilisateurs d’exécuter des requêtes ad hoc et par lots.

Le tableau suivant décrit les effets de l’autorisation [!DNL Manage Queries] :

| Autorisation | Fonction |
|---|---|
| [!DNL Manage Queries] (sans autorisation d’écriture de données) | Permet d’accéder à l’exécution de requêtes ad hoc |
| [!DNL Manage Queries] (avec autorisation d’écriture de données) | Permet d’accéder à l’exécution de requêtes par lots |

{style="table-layout:auto"}

### Autorisations SQL Insights pertinentes {#sql-insights-permissions}

Pour créer Data Distiller [SQL Insights](./data-distiller/sql-insights/overview.md) dans les tableaux de bord, les autorisations suivantes **doivent** être activées dans Admin Console.

| Autorisation | Fonction |
|---|---|
| [!DNL View Custom Dashboard] | Permet d’accéder aux tableaux de bord définis par l’utilisateur |
| [!DNL Manage Custom Dashboard] | Permet de gérer l’accès aux tableaux de bord définis par l’utilisateur |

{style="table-layout:auto"}

## Prise en charge des sandbox {#sandbox-support}

Les sandbox sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque instance de Platform prend en charge plusieurs environnements de test de production et hors production, chacun conservant sa propre bibliothèque de ressources de Platform. Les environnements de test hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter vos environnements de test de production. Pour plus d’informations sur les environnements de test, consultez la [présentation des environnements de test](../sandboxes/home.md). Tous les droits de Query Service sont partagés sur tous les environnements de test.

## Étapes suivantes

En lisant ce document, vous devez mieux comprendre les différents types de packages et les fonctionnalités d’exécution de requêtes disponibles dans Query Service. Pour en savoir plus sur Query Service, comme les cas d’utilisation connus du secteur, consultez la [documentation sur les cas d’utilisation](./use-cases/abandoned-browse.md). Pour plus d’informations, consultez la [présentation de Query Service](./home.md).

