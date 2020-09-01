---
keywords: Experience Platform;home;popular topics;PSQL;psql;Query service;query service;metadata;commands;metadata commands;
solution: Experience Platform
title: Commandes de métadonnées
topic: metadata
description: Liste de commandes PSQL actuellement prises en charge pour interroger les métadonnées.
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 96%

---


# Commandes de métadonnées

Pour les métadonnées de votre jeu de données, les commandes PSQL suivantes sont actuellement prises en charge pour l’interrogation :

>[!NOTE]
>
>Les commandes énumérées ci-dessous sont sensibles à la casse.

| Commande | Description |
|------- | ------------|
| `\conninfo` | Génère des informations sur la connexion actuelle à la base de données. |
| `\d` | Affiche une liste de toutes les tables visibles, des vues, des vues matérialisées, des séquences et des tables étrangères. |
| `\dE` | Affiche une liste de tables étrangères. |
| `\df or \df+` | Affiche une liste de fonctions. |
| `\di` | Affiche une liste d’index. |
| `\dm` | Affiche une liste de vues matérialisées. |
| `\dn` | Affiche une liste de schémas (espace de noms). |
| `\ds` | Affiche une liste de séquences. |
| `\dS` | Affiche une liste de tables définies par PostgreSQL. |
| `\dt` | Affiche une liste de tableaux. |
| `\dT` | Affiche une liste de types de données. |
| `\dv` | Affiche une liste de vues. |
| `\encoding` | Répertorie le codage actuel du jeu de caractères client. |
| `\errverbose` | Répète le message d’erreur du serveur le plus récent avec une précision maximale. |
| `\l or \list` | Affiche une liste de bases de données dans le serveur. |
| `\set` | Affiche les noms et les valeurs de toutes les variables psql actuelles. |
| `\showtables` | Affiche les informations suivantes : <br>nom : le nom par lequel la table est désignée.<br>datasetId : identifiant du jeu de données stocké.<br>dataset : nom du jeu de données stocké.<br>description : description du jeu de données.<br>resolved : valeur booléenne indiquant si le jeu de données est résolu ou non dans la session en cours. |
| `\timing` | Active et désactive l’affichage. L’affichage est en millisecondes. Les intervalles de plus d’une seconde s’affichent au format minutes:seconds, les champs heures et jours étant ajoutés si besoin. |

Toutes les commandes qui commencent par `\d` peuvent être combinées. Par exemple, vous pouvez émettre `\dtsn` pour afficher une liste de tous les tableaux, les séquences et les schémas. `\d` en elle-même affiche toutes les tables visibles, les vues, les vues matérialisées et les séquences.

Pour plus d’informations sur les commandes énumérées ci-dessus, consultez la documentation à l’adresse [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Toutefois, sachez que toutes les options présentées dans la documentation PostgreSQL ne sont pas prises en charge par [!DNL Experience Platform].

