---
keywords: Experience Platform;requête;query service;dépannage;mécanismes de sécurisation;instructions;limite;
title: Mécanismes de sécurisation pour Query Service
description: Ce document fournit des informations sur les limites d’utilisation des données de Query Service afin de vous aider à optimiser l’utilisation de vos requêtes.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 23c7a4590b365a49edb066567b6ebe2ac08c67e8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 4%

---

# Mécanismes de sécurisation pour Query Service

Les mécanismes de sécurisation sont des seuils qui guident l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Adobe Experience Platform.
Ce document fournit des limites d’utilisation par défaut pour les données Query Service afin de vous aider à optimiser les performances du système lors de l’interrogation de données relatives à vos droits de licence.

>[!IMPORTANT]
>
>Vérifiez vos droits de licence dans votre commande client et la [Description du produit](https://helpx.adobe.com/fr/legal/product-descriptions.html) correspondante sur les limites d’utilisation réelles en plus de cette page de mécanismes de sécurisation.

## Conditions préalables

Avant de poursuivre avec ce document, vous devez avoir une bonne compréhension des définitions et fonctionnalités clés de Query Service. Elles sont décrites ci-dessous :

* **Requêtes ad hoc** : pour exécuter des requêtes `SELECT` afin d’explorer, d’expérimenter et de valider des données là où les résultats des requêtes **ne sont pas stockés** dans le lac de données.

* **Requêtes par lots** : pour exécuter des requêtes `INSERT TABLE AS SELECT` et `CREATE TABLE AS SELECT` afin de nettoyer, mettre en forme, manipuler et enrichir les données. Les résultats de ces requêtes **sont stockés** dans le lac de données. La mesure permettant de mesurer la consommation de cette fonctionnalité est constituée d’heures de calcul.

* **Utilisateurs de Query Service** : les utilisateurs de Query Service fournis dans votre licence actuelle pour Customer Journey Analytics, Adobe Real-Time Customer Data Platform et/ou Adobe Journey Optimizer peuvent également être utilisés avec Data Distiller. Les utilisateurs de Query Service sont partagés entre les fonctionnalités.

* **Utilisateurs ad hoc** : les utilisateurs ad hoc sont ceux qui exécutent des requêtes ad hoc.

* **Utilisateurs par lots** : ce sont les utilisateurs par lots qui exécutent les requêtes par lots.

* **API de création de rapports** : API pour effectuer des appels de récupération de données (en interne ou en externe). Les modèles de données de rapports étendus sont dérivés des modèles de données de rapports natifs de Adobe Experience Platform, tels que le modèle de données des tableaux de bord Real-Time CDP.

## Types de mécanismes de sécurisation

Ce document comprend deux types de limites par défaut :

| Type de mécanisme de sécurisation | Description |
|----------|---------|
| **Mécanisme de sécurisation des performances (limite soft)** | Les mécanismes de sécurisation de performances sont des limites d’utilisation liées à la portée de vos cas d’utilisation. Si vous dépassez les mécanismes de sécurisation des performances, vous pouvez rencontrer une dégradation des performances et une latence. Adobe n’est pas responsable de cette dégradation des performances. Les clients qui dépassent régulièrement un mécanisme de sécurisation des performances peuvent choisir de se procurer une licence pour une capacité supplémentaire afin d’éviter une dégradation des performances. |
| **Mécanismes de sécurisation appliqués par le système (limite Hard)** | Les mécanismes de sécurisation appliqués par le système sont appliqués par l’interface utilisateur ou l’API Real-Time CDP. Il s’agit de limites que vous ne pouvez pas dépasser, car l’interface utilisateur et l’API vous en empêcheront ou renverront une erreur. |

{style="table-layout:auto"}

>[!NOTE]
>
>Les limites par défaut décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour.

## Mécanismes de sécurisation des performances des entités de Principal

Les tableaux ci-dessous fournissent les limites et descriptions recommandées du mécanisme de sécurisation pour l’exécution de requêtes lors de l’utilisation d’un modèle de requête particulier.

**Requêtes ad hoc**

| Mécanisme de sécurisation | Limite | Type de limite | Description |
|---|---|---|---|
| Durée maximale d’exécution | 10 minutes | Mécanisme de sécurisation mis en œuvre par le système | Cela définit le temps de sortie maximal d’une requête SQL ad hoc. Le dépassement du délai imparti pour renvoyer un résultat renvoie le code d’erreur 53400. |
| Utilisateurs Query Service simultanés | <ul><li>Tel que spécifié dans la description du produit d&#39;application.</li><li>+5 (avec chaque pack de modules complémentaires d’utilisateurs de requêtes ad hoc acheté)</li></ul> | Mécanisme de sécurisation mis en œuvre par le système | Cela définit le nombre d’utilisateurs et d’utilisatrices qui peuvent créer des sessions simultanément pour une organisation particulière. Si la limite de simultanéité est dépassée, l’utilisateur ou l’utilisatrice reçoit une erreur de `Session Limit Reached`. |
| Simultanéité des requêtes | <ul><li>Tel que spécifié dans la description du produit d&#39;application.</li><li>+1 (avec chaque pack de SKU de module complémentaire d’utilisateur de requête ad hoc acheté)</li></ul> | Mécanisme de sécurisation mis en œuvre par le système | Cela définit le nombre de requêtes pouvant être exécutées simultanément pour une organisation particulière. Si la limite de simultanéité est dépassée, les requêtes sont mises en file d’attente. |
| Connecteur client et limite de sortie de résultat | Connecteur client<ul><li>Interface utilisateur de requête (100 lignes)</li><li>Client tiers (50 000)</li><li>[!DNL PostgresSQL] client (50 000)</li></ul> | Mécanisme de sécurisation mis en œuvre par le système | Le résultat d’une requête peut être reçu par les moyens suivants :<ul><li>Interface utilisateur de Query Service</li><li>Client tiers</li><li>client [!DNL PostgresSQL]</li></ul>Remarque : l’ajout d’une limitation au nombre de sorties peut renvoyer des résultats plus rapidement. Par exemple, `LIMIT 5`, `LIMIT 10`, etc. |
| Résultats renvoyés via | Interface utilisateur du client | S/O | Cela définit la manière dont les résultats sont mis à la disposition des utilisateurs. |

{style="table-layout:auto"}

**Requêtes par lots**

| **Mécanisme de sécurisation** | **Limite** | **Type de limite** | **Description** |
|---|---|---|---|
| Durée maximale d’exécution | 24 heures | Mécanisme de sécurisation mis en œuvre par le système | Cela définit le temps d’exécution maximal d’une requête SQL par lots.<br>Le temps de traitement d’une requête dépend du volume de données à traiter et de la complexité de la requête. |
| Utilisateurs simultanés de Query Service pour un lot non planifié | <ul><li>Tel que spécifié dans la description du produit d&#39;application.</li><li>+5 (avec chaque pack de modules complémentaires d’utilisateurs de requêtes ad hoc acheté)</li></ul> | Mécanisme de sécurisation mis en œuvre par le système | Pour les requêtes par lots non planifiées (par exemple, les requêtes CTAS/ITAS en mode interactif), cela définit le nombre d’utilisateurs et d’utilisatrices qui peuvent créer des sessions simultanément pour une organisation particulière. Si la limite de simultanéité est dépassée, l’utilisateur ou l’utilisatrice reçoit une erreur de `Session Limit Reached`. |
| Utilisateurs et utilisatrices simultanés de Query Service pour le lot planifié | Aucune limitation utilisateur | S/O | Les requêtes par lots planifiées sont des tâches asynchrones, il n’existe donc aucune limitation utilisateur. |
| Heures de calcul pour le traitement des données par lots | Comme indiqué dans la commande client de SKU personnalisé de requête d’intelligence de Adobe Experience Platform | Mécanisme de sécurisation des performances | Cela définit la durée de calcul par an pendant laquelle un client est autorisé à exécuter des requêtes par lots pour analyser, traiter et écrire des données dans le lac de données. |
| Simultanéité des requêtes | Pris en charge | S/O | Les requêtes par lots planifiées sont des tâches asynchrones, par conséquent les requêtes simultanées sont prises en charge. |
| Connecteur client et limite de sortie de résultat | Connecteur client<ul><li>Interface utilisateur de requête (aucune limite supérieure de lignes)</li><li>Client tiers (aucune limite supérieure de lignes)</li><li>[!DNL PostgresSQL] client (pas de limite supérieure à lignes)</li><li>API REST (pas de limite supérieure à lignes)</li></ul> | Mécanisme de sécurisation mis en œuvre par le système | Le résultat d’une requête peut être rendu disponible en utilisant les méthodes suivantes :<ul><li>Peuvent être stockés en tant que jeux de données dérivés</li><li>Peuvent être insérées dans les jeux de données dérivés existants</li></ul>Remarque : il n&#39;existe pas de limite supérieure au nombre d&#39;enregistrements à partir du résultat de la requête. |
| Résultats renvoyés via | Jeu de données | S/O | Cela définit la manière dont les résultats sont mis à la disposition des utilisateurs. |

{style="table-layout:auto"}

## Magasin de requêtes accélérées {#query-accelerated-store}

Le tableau ci-dessous fournit les limites de mécanisme de sécurisation recommandées et la description de la boutique de requêtes accélérées.

| Mécanisme de sécurisation | Limite | Type de limite | Description |
|---|---|---|---|
| Simultanéité des requêtes | 4 | Mécanisme de sécurisation mis en œuvre par le système | Pour s’assurer que les requêtes sur les données agrégées via l’API de création de rapports (y compris les requêtes qui améliorent les modèles de données tels que les modèles de données Real-Time CDP) disposent des ressources nécessaires pour s’exécuter efficacement, l’API de création de rapports effectue le suivi de l’utilisation des ressources en attribuant des emplacements d’accès simultané à chaque requête. Le système place les requêtes dans une file d’attente et attend que des emplacements d’accès simultané soient disponibles ou qu’elles puissent être diffusées à partir du cache. Un maximum de quatre emplacements de requête simultanés est disponible à tout moment.<br>Si vous accédez à l’API de création de rapports par le biais d’un outil BI et que vous avez besoin de plus d’accès simultanés, un serveur BI est requis. |

{style="table-layout:auto"}

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous devriez mieux comprendre les limites par défaut de l’exécution des requêtes avec les modèles de requête disponibles.

Pour plus d’informations sur Query Service, consultez la documentation suivante :

* [API Query Service](./api/getting-started.md)
* [Interface utilisateur de Query Service](./ui/overview.md)

Consultez la documentation suivante pour plus d’informations sur les autres mécanismes de sécurisation des services Experience Platform, sur les informations de latence de bout en bout et les informations de licence dans les documents de description du produit Real-Time CDP :

* [Mécanismes de sécurisation de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) pour divers services Experience Platform.
* [Real-Time Customer Data Platform (édition B2C - packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)