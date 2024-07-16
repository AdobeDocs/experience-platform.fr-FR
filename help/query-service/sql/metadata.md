---
keywords: Experience Platform;accueil;rubriques populaires;PSQL;psql;service de requête;service de requête;métadonnées;commandes;commandes de métadonnées;
solution: Experience Platform
title: Commandes de métadonnées PostgreSQL dans Query Service
description: Liste des commandes PostgreSQL actuellement prises en charge pour interroger des métadonnées dans Adobe Experience Platform Query Service.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 75%

---

# Commandes de métadonnées [!DNL PostgreSQL] dans Query Service

Pour les métadonnées de votre jeu de données, les commandes [!DNL PostgreSQL] suivantes sont actuellement prises en charge pour l’interrogation :

>[!NOTE]
>
>Les commandes répertoriées ci-dessous sont sensibles à la casse.

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

Pour plus d’informations sur les commandes énumérées ci-dessus, consultez la documentation à l’adresse [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Toutefois, sachez que toutes les options présentées dans la documentation [!DNL PostgreSQL] ne sont pas prises en charge par [!DNL Experience Platform].
