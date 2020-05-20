---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Commandes de métadonnées
topic: metadata
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Commandes de métadonnées

Pour les métadonnées de votre jeu de données, les commandes PSQL suivantes sont actuellement prises en charge pour l’interrogation :

>[!NOTE] Les commandes répertoriées ci-dessous sont sensibles à la casse.

| La commande | Description |
|------- | ------------|
| `\conninfo` | Génère des informations sur la connexion à la base de données active. |
| `\d` | Affiche une liste de toutes les tables visibles, vues, vues matérialisées, séquences et tables étrangères. |
| `\dE` | Affiche une liste de tables étrangères. |
| `\df or \df+` | Affiche une liste de fonctions. |
| `\di` | Affiche une liste d&#39;index. |
| `\dm` | Affiche une liste de vues matérialisées. |
| `\dn` | Affiche une liste de schémas (espaces de nommage). |
| `\ds` | Affiche une liste de séquences. |
| `\dS` | Affiche une liste de tables définies par PostgreSQL. |
| `\dt` | Affiche une liste de tableaux. |
| `\dT` | Affiche une liste de types de données. |
| `\dv` | Affiche une liste de vues. |
| `\encoding` | Liste le codage actuel du jeu de caractères client. |
| `\errverbose` | Répète le message d’erreur le plus récent du serveur avec une précision maximale. |
| `\l or \list` | Affiche une liste de bases de données dans le serveur. |
| `\set` | Affiche les noms et les valeurs de toutes les variables SQL actuelles. |
| `\showtables` | Affiche les informations suivantes : <br>name: Nom auquel la table sera référencée.<br>datasetId : ID du jeu de données stocké.<br>dataset : Nom du jeu de données stocké.<br>description : Description du jeu de données.<br>résolu : Valeur booléenne indiquant si le jeu de données est résolu ou non dans la session en cours. |
| `\timing` | Active ou désactive l’affichage. L’affichage est en millisecondes. Les intervalles de plus d’une seconde sont affichés au format minutes:secondes, avec des champs d’heures et de jours ajoutés au besoin. |

Toutes les commandes avec lesquelles ce début `\d` peut être combiné. Par exemple, vous pouvez publier `\dtsn` pour afficher une liste de tous les tableaux, séquences et schémas. `\d` affiche toutes les tables, vues, vues matérialisées et séquences visibles.

Pour plus d&#39;informations sur les commandes listées ci-dessus, veuillez consulter la documentation à [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Cependant, sachez que toutes les options présentées dans la documentation PostgreSQL ne sont pas prises en charge par Experience Platform.

