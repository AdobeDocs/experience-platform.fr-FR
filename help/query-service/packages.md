---
title: Packages Query Service
description: Le document suivant décrit les packages de fonctionnalités et de produits disponibles pour Query Service et met en évidence les différences entre les requêtes ad hoc et les requêtes par lots.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 4fb755d8936a6c2019421a064e29ab403092cf77
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 9%

---

# Packages Query Service

Ce document décrit les différents types de fonctionnalités de création de package et d’exécution de requêtes disponibles dans Query Service.

Adobe Experience Platform Query Service peut être divisé en deux fonctionnalités basées sur les modèles de requête pouvant être exécutés :

- **Requêtes ad hoc** sont des requêtes SQL utilisées pour explorer les jeux de données ingérés pour la vérification, la validation, l’expérimentation, etc. Ces requêtes n’écrivent pas de données dans le lac de données Platform.
- **Requêtes par lots** sont des requêtes SQL utilisées pour effectuer le traitement après ingestion des jeux de données ingérés. Ces requêtes nettoient, façonnent, manipulent et enrichissent des données, dont les résultats sont réécrits dans le lac de données Platform. Ces requêtes peuvent être planifiées, gérées et surveillées sous la forme de tâches par lots.

Les fonctionnalités de Query Service sont incluses dans les produits et modules complémentaires suivants :

- **Applications basées sur des plateformes** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics et Adobe Journey Optimizer) : l’accès à Query Service pour exécuter des requêtes ad hoc est fourni dès le départ avec chaque variante et niveau d’applications basées sur Platform.
- **[!DNL Data Distiller]** (package de module complémentaire pouvant être acheté avec Adobe Real-Time CDP, Customer Journey Analytics et Adobe Journey Optimizer) : l’accès à Query Service pour exécuter des requêtes par lots est fourni avec [!DNL Data Distiller].

## Terminologie {#terminology}

La section suivante fournit des définitions des termes clés liés aux packages Query Service :

- **Stockage du lac de données**: le lac de données sert principalement les objectifs suivants :
   - Il sert de zone de test pour l’intégration des données dans Experience Platform.
   - Il sert de stockage de données à long terme pour toutes les données Experience Platform.
   - Il permet des cas d’utilisation tels que l’analyse des données et la science des données.
- **Exportation des données**: la variable [dataset](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=fr) types que vous pouvez exporter en fonction de votre application, du niveau du produit et des modules complémentaires achetés. Les jeux de données dérivés peuvent être créés par le biais du module complémentaire Distiller de données Query Service et peuvent être [exporté depuis Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activation-overview.html) à un large éventail de destinations, y compris [destinations de stockage cloud](/help/destinations/ui/export-datasets.md).
- **Requêtes accélérées**: les requêtes accélérées renvoient des résultats en fonction de données agrégées afin de réduire le temps d’attente des résultats et de fournir un échange d’informations plus interactif. Les requêtes apatrides effectuées au magasin accéléré ne sont disponibles que dans le cadre du module complémentaire Data Distiller.
- **Calculer les heures**: les heures de calcul sont la mesure utilisée pour effectuer le suivi de l’analyse et de l’écriture de données avec des requêtes par lots à l’aide de l’API Query Service. Elle est calculée en heures par an et mesurée sur tous les environnements de test. Le nombre d’heures de calcul fourni à votre organisation est défini dans le processus de définition de la portée de l’opération.

## Droits {#entitlements}

Le tableau suivant décrit les principaux droits de Query Service en fonction de leur mode de création :

| Droit de Query Service | Modules avec les applications basées sur Platform | Packé avec [!DNL Data Distiller] |
|---|---|---|
| Motif de requête pris en charge | Requêtes ad hoc uniquement | Requête par lots |
| Cas d’utilisation pris en charge | <ul><li>Exploration &#x200B;</li><li>&#x200B; de détection des données</li><li>Validation des données</li><li>Expérimentation</li></ul> | <ul><li>Nettoyage</li><li>Forme</li><li>Manipulation</li><li>Enrichir</li></ul> |
| Sémantique pris en charge | <ul><li>SELECT requêtes</li></ul> | <ul><li>Requêtes CTAS et ITAS</li></ul> |
| Durée maximale d’exécution | 10 minutes | 24 heures |
| Mesure de licence | **Concurrence des utilisateurs de la requête**: <ul><li>1 utilisateur simultané (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 utilisateurs simultanés (Customer Journey Analytics) &#x200B;</li></ul> **Requête simultanée**: <ul><li>1 requête en cours d’exécution simultanée (toutes les applications) &#x200B;</li></ul> **Module complémentaire pour utilisateurs de requêtes ad hoc** peuvent être achetés pour augmenter les droits de requête ad hoc autorisés des clients. <ul><li>+5 utilisateurs simultanés supplémentaires par pack</li><li>+1 requête d’exécution simultanée supplémentaire par pack</li></ul> | **Heures de calcul**: <ul><li>Variable (définie selon les droits d’application du client)</li></ul> **Heures de calcul** mesure le temps nécessaire au moteur Query Service pour lire, traiter et écrire des données dans le lac de données lors de l’exécution d’une requête par lots. |
| Utilisation accélérée des requêtes et des rapports | Non | Oui : les requêtes accélérées simultanées vous permettent de lire les données de la boutique accélérée et de les afficher dans vos tableaux de bord. Un droit dédié pour le stockage des modèles de rapports et des jeux de données dans le magasin accéléré est également fourni. |
| Capacité de stockage du lac de données | Oui - Le total des droits de stockage dépend des licences d’applications basées sur la plateforme. Par exemple, Real-Time CDP, AJO, CJA, etc. | Oui - Un droit de stockage supplémentaire est fourni pour conserver vos jeux de données bruts et dérivés pour les cas d’utilisation de Data Distiller au-delà d’une date d’expiration de données de sept jours.<br>La capacité de stockage de votre lac de données est mesurée en téraoctets (To) et dépend de la quantité d’heures de calcul que vous avez achetées. |
| Frais d&#39;exportation de données | Oui - Le total des droits à l’exportation dépend des licences d’applications basées sur la plateforme. Par exemple, Real-Time CDP, AJO, CJA, etc. | Oui - Des droits d’exportation supplémentaires sont fournis pour permettre l’exportation des jeux de données dérivés créés à l’aide de Data Distiller.<br>Votre capacité d’exportation annuelle des données est mesurée en téraoctets (TB) et dépend de la quantité d’heures de calcul que vous avez achetées. |
| Interface d’exécution de requête | <ul><li>UI Query Service</li><li>Interface utilisateur cliente tierce</li><li>[!DNL PostgresSQL] Interface utilisateur client</li></ul> | <ul><li>UI Query Service </li><li>Interface utilisateur cliente tierce</li><li>[!DNL PostgresSQL] Interface utilisateur client</li><li>API REST</li></ul> |
| Résultats de la requête renvoyés via | Interface utilisateur du client | Jeu de données dérivé stocké dans le lac de données |
| Limite de résultat | <ul><li>Interface utilisateur de Query Service - 100 lignes</li><li>Clients tiers - 50 000</li><li>[!DNL PostgresSQL] client - 50 000</li></ul> | <ul><li>Interface utilisateur de Query Service : le nombre de lignes de sortie peut être [configuré avec un paramètre d’interface utilisateur](./ui/user-guide.md#result-count) entre 50 et 500 lignes.</li><li>Clients tiers (pas de limite supérieure aux lignes)</li><li>[!DNL PostgresSQL] client (aucune limite supérieure aux lignes)</li><li>API REST (pas de limite supérieure pour les lignes)</li></ul> |
| Lecture de la capacité du jeu de données | Oui | Oui |
| Écriture de la capacité du jeu de données | Non | Oui |
| Capacité de planification | Non | Oui |
| Capacité de surveillance | Oui | Oui |
| Capacité de configuration des alertes de requête | Non | Oui |

{style="table-layout:auto"}

## Contrôle d’accès {#access-control}

Le contrôle d’accès de l’Experience Platform est géré à l’aide de la variable [Adobe Admin Console](https://adminconsole.adobe.com/) où les profils de produit lient les utilisateurs à des autorisations et des environnements de test. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).

Pour utiliser Query Service, la variable [!DNL Manage Queries] l’autorisation doit être activée dans Admin Console. Cette autorisation permet aux utilisateurs d’exécuter des requêtes ad hoc et par lots. Instructions détaillées sur la demande d’accès au profil de produit [!DNL Manage Queries] ont été décrites dans la section [gestion des autorisations d’un profil de produit](../access-control/ui/permissions.md) et [gestion des utilisateurs pour un profil de produit](../access-control/ui/users.md) documents.

Après avoir acheté la variable [!DNL Data Distiller] module complémentaire, le [!DNL Write Dataset] La permission doit être accordée. Cette autorisation permet [!DNL Data Distiller] utilisateurs pour exécuter des requêtes par lots.

Le tableau suivant décrit les effets de la variable [!DNL Manage Queries] autorisation :

| Autorisation | Fonction |
|---|---|
| [!DNL Manage Queries] (sans autorisation d’écriture de données) | Permet d’accéder à l’exécution de requêtes ad hoc |
| [!DNL Manage Queries] (avec autorisation pour écrire des données) | Permet d’accéder à l’exécution de requêtes par lots |

{style="table-layout:auto"}

## Prise en charge des sandbox {#sandbox-support}

Les sandbox sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque instance de Platform prend en charge plusieurs environnements de test de production et hors production, chacun conservant sa propre bibliothèque de ressources de Platform. Les environnements de test hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter vos environnements de test de production. Pour plus d’informations sur les sandbox, consultez la [présentation des sandbox](../sandboxes/home.md). Tous les droits de Query Service sont partagés sur tous les environnements de test.

## Étapes suivantes

En lisant ce document, vous devez mieux comprendre les différents types de packages et les fonctionnalités d’exécution de requêtes disponibles dans Query Service. Pour en savoir plus sur Query Service, comme les cas d’utilisation connus du secteur, lisez la section [documentation sur les cas d’utilisation](./use-cases/abandoned-browse.md). Pour obtenir des informations plus générales, consultez la [Présentation de Query Service](./home.md).
