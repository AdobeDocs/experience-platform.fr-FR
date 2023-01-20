---
title: Packages Query Service
description: Le document suivant décrit les packages de fonctionnalités et de produits disponibles pour Query Service et met en évidence les différences entre les requêtes ad hoc et les requêtes par lots.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 8%

---

# Packages Query Service

Ce document décrit les différents types de fonctionnalités de création de package et d’exécution de requêtes disponibles dans Query Service.

Adobe Experience Platform Query Service peut être divisé en deux fonctionnalités basées sur les modèles de requête pouvant être exécutés :

- **Requêtes ad hoc** sont des requêtes SQL utilisées pour explorer les jeux de données ingérés à des fins de vérification, de validation, d’expérimentation, etc. Ces requêtes n’écrivent pas de données dans le lac de données Platform.
- **Requêtes par lots** sont des requêtes SQL utilisées pour effectuer le traitement après ingestion des jeux de données ingérés. Ces requêtes nettoient, forment, manipulent et enrichissent des données, dont les résultats sont réécrits dans le lac de données Platform. Ces requêtes peuvent être planifiées, gérées et surveillées sous la forme de tâches par lots.

Les fonctionnalités de Query Service sont incluses dans les produits et modules complémentaires suivants :

- **Applications basées sur des plateformes** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics et Adobe Journey Optimizer) : L’accès à Query Service pour exécuter des requêtes ad hoc est fourni dès le départ avec chaque variante et niveau d’applications basées sur Platform.
- **[!DNL Data Distiller]** (module complémentaire pouvant être acheté avec Adobe Real-Time CDP, Customer Journey Analytics et Adobe Journey Optimizer) : L’accès à Query Service pour exécuter des requêtes par lots est fourni avec [!DNL Data Distiller].

Le tableau suivant décrit les principaux droits de Query Service en fonction de leur mode de création :

| Droit de Query Service | Modules avec les applications basées sur Platform | Packé avec [!DNL Data Distiller] |
|---|---|---|
| Motif de requête pris en charge | Requête ad hoc uniquement | Requête par lots |
| Cas d’utilisation pris en charge | <ul><li>Exploration &#x200B;</li><li>&#x200B; de détection des données</li><li>Validation des données</li><li>Expérimentation</li></ul> | <ul><li>Nettoyage</li><li>Forme</li><li>Manipulation</li><li>Enrichir</li></ul> |
| Sémantique pris en charge | <ul><li>SELECT requêtes</li></ul> | <ul><li>Requêtes CTAS et ITAS</li></ul> |
| Durée maximale d’exécution | 10 minutes | 24 heures |
| Mesure de licence | **Concurrence des utilisateurs de la requête**: <ul><li>1 utilisateur simultané (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 utilisateurs simultanés (Customer Journey Analytics) &#x200B;</li></ul> **Requête simultanée**: <ul><li>1 requête en cours d’exécution simultanée (toutes les applications) &#x200B;</li></ul> **Module complémentaire pour utilisateurs de requêtes ad hoc** peuvent être achetés pour augmenter les droits de requête ad hoc autorisés des clients. <ul><li>+5 utilisateurs simultanés supplémentaires par pack</li><li>+1 requête d’exécution simultanée supplémentaire par pack</li></ul> | **Heures de calcul**: <ul><li>Variable (définie selon les droits d’application du client)</li></ul> **Heures de calcul** mesure le temps nécessaire au moteur Query Service pour lire, traiter et écrire des données dans le lac de données lors de l’exécution d’une requête par lots. |
| Interface d’exécution de requête | <ul><li>UI Query Service</li><li>Interface utilisateur cliente tierce</li><li>[!DNL PostgresSQL] Interface utilisateur client</li></ul> | <ul><li>Interface utilisateur de la requête </li><li>Interface utilisateur cliente tierce</li><li>[!DNL PostgresSQL] Interface utilisateur client</li><li>API REST</li></ul> |
| Résultats de la requête renvoyés via | Interface utilisateur du client | Jeu de données dérivé stocké dans le lac de données |
| Limite de résultat | <ul><li>Interface utilisateur de requête - 100 lignes</li><li>Client tiers - 50 000</li><li>[!DNL PostgresSQL] client - 50 000</li></ul> | <ul><li>Interface utilisateur de requête (pas de limite supérieure pour les lignes)</li><li>Clients tiers (pas de limite supérieure aux lignes)</li><li>[!DNL PostgresSQL] client (aucune limite supérieure aux lignes)</li><li>API REST (pas de limite supérieure pour les lignes)</li></ul> |
| Lecture de la capacité du jeu de données | Oui | Oui |
| Écriture de la capacité du jeu de données | Non | Oui |
| Capacité de planification | Non | Oui |
| Capacité de surveillance | Oui | Oui |
| Capacité de configuration des alertes de requête | Non | Oui |

{style=&quot;table-layout:auto&quot;}

## Contrôle d’accès

Le contrôle d’accès de l’Experience Platform est géré à l’aide de la variable [Adobe Admin Console](https://adminconsole.adobe.com/) où les profils de produit lient les utilisateurs à des autorisations et des environnements de test. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).

Pour utiliser Query Service, la variable [!DNL Manage Queries] La permission doit être activée dans admin console. Cette autorisation permet aux utilisateurs d’exécuter des requêtes ad hoc et par lots. Instructions détaillées sur la demande d’accès au profil de produit [!DNL Manage Queries] ont été décrites dans la section [gestion des autorisations d’un profil de produit](../access-control/ui/permissions.md) et [gestion des utilisateurs pour un profil de produit](../access-control/ui/users.md) documents.

Après avoir acheté la variable [!DNL Data Distiller] module complémentaire, le [!DNL Write Dataset] La permission doit être accordée. Cette autorisation permet [!DNL Data Distiller] utilisateurs pour exécuter des requêtes par lots.

Le tableau suivant décrit les effets de la variable [!DNL Manage Queries] autorisation :

| Autorisation | Fonction |
|---|---|
| [!DNL Manage Queries] (sans autorisation d’écriture de données) | Permet d’accéder à l’exécution de requêtes ad hoc |
| [!DNL Manage Queries] (avec autorisation pour écrire des données) | Permet d’accéder à l’exécution de requêtes par lots |

{style=&quot;table-layout:auto&quot;}

## Prise en charge des environnements de test

Les environnements de test sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque instance de Platform prend en charge plusieurs environnements de test de production et autres, chacun conservant sa propre bibliothèque de ressources de Platform. Les environnements de test hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter vos environnements de test de production. Pour plus d’informations sur les environnements de test, consultez la [présentation des environnements de test](../sandboxes/home.md). Tous les droits de Query Service sont partagés sur tous les environnements de test.

## Étapes suivantes

En lisant ce document, vous devez mieux comprendre les différents types de packages et les fonctionnalités d’exécution de requêtes disponibles dans Query Service. Pour en savoir plus sur Query Service, comme les cas d’utilisation connus du secteur, veuillez lire la section [documentation sur les cas d’utilisation](./use-cases/abandoned-browse.md). Pour obtenir des informations plus générales, consultez la [Présentation de Query Service](./home.md).
