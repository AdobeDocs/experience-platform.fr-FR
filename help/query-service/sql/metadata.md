---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Commandes de métadonnées
topic: metadata
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Commandes de métadonnées

Pour les métadonnées de votre jeu de données, les commandes PSQL suivantes sont actuellement prises en charge pour l’interrogation :

>[!NOTE] Les commandes répertoriées ci-dessous sont sensibles à la casse.

| La commande | Description |
|------- | ------------|
| `\conninfo` | Génère des informations sur la connexion actuelle à la base de données. |
| `\d` | Affiche un  de toutes les tables visibles, les  de, les  matérialisées, les séquences et les tables étrangères. |
| `\dE` | Affiche un  de tables étrangères. |
| `\df or \df+` | Affiche un  de fonctions. |
| `\di` | Affiche un  d’index. |
| `\dm` | Affiche un  de  de matérialisé. |
| `\dn` | Affiche un de  ( de). |
| `\ds` | Affiche un  de séquences. |
| `\dS` | Affiche un de tables définies par PostgreSQL. |
| `\dt` | Affiche un  de tableaux. |
| `\dT` | Affiche un  de types de données. |
| `\dv` | Affiche un  de  de. |
| `\encoding` | le codage actuel du jeu de caractères client. |
| `\errverbose` | Répète le message d’erreur du serveur le plus récent avec une précision maximale. |
| `\l or \list` | Affiche un  de bases de données dans le serveur. |
| `\set` | Affiche les noms et les valeurs de toutes les variables psql actuelles. |
| `\showtables` | Affiche les informations suivantes : <br>nom : Nom auquel la table sera référencée.<br>datasetId : ID du jeu de données stocké.<br>dataset : Nom du jeu de données stocké.<br>description : Description du jeu de données.<br>résolu : Valeur booléenne indiquant si le jeu de données est résolu ou non dans la session en cours. |
| `\timing` | Active et désactive l’affichage. L’affichage est en millisecondes. Les intervalles de plus d’une seconde sont affichés au format minutes:secondes, avec les champs heures et jours ajoutés au besoin. |

Toutes les commandes avec lesquelles vous  peuvent être combinées. `\d` Par exemple, vous pouvez publier `\dtsn` pour afficher un  de tous les tableaux, séquences et  de. `\d` affiche toutes les tables visibles, les , les  matérialisées et les séquences.

Pour plus d&#39;informations sur les commandes listées ci-dessus, consultez la documentation de [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Toutefois, sachez que toutes les options présentées dans la documentation PostgreSQL ne sont pas prises en charge par Experience Platform.

