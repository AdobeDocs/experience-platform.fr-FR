---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;guide de dépannage;faq;dépannage;
solution: Experience Platform
title: Guide de dépannage de Query Service
topic-legacy: troubleshooting
description: Ce document contient des informations sur les codes d’erreur courants que vous rencontrez et les causes possibles.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 42288ae7db6fb19bc0a0ee8e4ecfa50b7d63d017
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 22%

---

# Guide de dépannage du [!DNL Query Service]

Ce document fournit des réponses aux questions fréquentes sur Query Service et fournit une liste des codes d’erreur courants lors de l’utilisation de Query Service. Pour toute question ou dépannage concernant les autres services d’Adobe Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

## Questions fréquentes

Vous trouverez ci-dessous une liste de réponses aux questions les plus courantes sur Query Service.

### Comment puis-je obtenir uniquement les métadonnées d’une requête ?

Pour obtenir uniquement les métadonnées d’une requête, vous pouvez exécuter une requête qui renvoie zéro ligne, comme suit :

```sql
SELECT * FROM <table> WHERE 1=0
```

Cette requête renvoie uniquement les métadonnées de la table spécifiée.

### Comment puis-je itérer rapidement sur une requête CTAS (Create Table as Select) sans la matérialiser ?

Vous pouvez créer des tableaux temporaires pour itérer rapidement une requête et la tester avant de la matérialiser pour l’utiliser. Vous pouvez également utiliser des tableaux temporaires pour vérifier si une requête est fonctionnelle.

Vous pouvez par exemple créer un tableau temporaire :

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

Vous pouvez ensuite utiliser le tableau temporaire comme suit :

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

### Comment dois-je filtrer mes données de série temporelle ?

Lors de l’interrogation des données de série temporelle, vous devez utiliser le filtre d’horodatage chaque fois que cela est possible pour une analyse plus précise.

>[!NOTE]
>
> La chaîne de date **doit** être au format `yyyy-mm-ddTHH24:MM:SS`.

Vous trouverez ci-dessous un exemple d’utilisation du filtre d’horodatage :

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

### Dois-je utiliser des caractères génériques, tels que * pour obtenir toutes les lignes de mes jeux de données ?

Vous ne pouvez pas utiliser de caractères génériques pour obtenir toutes les données de vos lignes, car Query Service doit être traité comme **columnar-store** plutôt que comme un système de magasin basé sur les lignes traditionnel.

### Dois-je utiliser `NOT IN` dans ma requête SQL ?

L’opérateur `NOT IN` est souvent utilisé pour récupérer les lignes qui ne se trouvent pas dans une autre table ou instruction SQL. Cet opérateur peut ralentir les performances et renvoyer des résultats inattendus si les colonnes comparées acceptent `NOT NULL`, ou si vous avez un grand nombre d&#39;enregistrements.

Au lieu d’utiliser `NOT IN`, vous pouvez utiliser `NOT EXISTS` ou `LEFT OUTER JOIN`.

Par exemple, si les tables suivantes sont créées :

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Si vous utilisez l’opérateur `NOT EXISTS`, vous pouvez effectuer une réplication à l’aide de l’opérateur `NOT IN` à l’aide de la requête suivante :

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Si vous utilisez l’opérateur `LEFT OUTER JOIN`, vous pouvez également effectuer une réplication à l’aide de l’opérateur `NOT IN` à l’aide de la requête suivante :

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### Quelle est l’utilisation correcte des opérateurs `OR` et `UNION` ?

### Comment utiliser correctement l’opérateur `CAST` pour convertir mes horodatages dans les requêtes SQL ?

Lorsque vous utilisez l’opérateur `CAST` pour convertir un horodatage, vous devez inclure à la fois la date **et l’heure**.

Par exemple, l’absence du composant temporel, comme illustré ci-dessous, entraînera une erreur :

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

L’utilisation correcte de l’opérateur `CAST` est présentée ci-dessous :

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

## Erreurs de l’API REST

| Code d’état HTTP | Description | Causes possibles |
| ---------------- | ----------- | --------------- |
| 400 | Mauvaise requête | Requête malformée ou illégale |
| 401 | Échec de l’authentification | Jeton d’authentification non valide |
| 500 | Erreur interne du serveur | Échec du système interne |

## Erreurs de l’API PostgreSQL

| Code erreur | État de la connexion | Description | Cause possible |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | S.O. | Type de message non pris en charge | Type de message non pris en charge |
| **28P01** | Démarrage - authentification | Mot de passe non valide | Jeton d’authentification non valide |
| **28000** | Démarrage - authentification | Type d’autorisation non valide | Type d’autorisation non valide. Doit être `AuthenticationCleartextPassword`. |
| **42P12** | Démarrage - authentification | Aucune table trouvée | Aucune table n’a été trouvée pour utilisation |
| **42601** | Requête | Erreur de syntaxe | Erreur de syntaxe ou de commande non valide |
| **42P01** | Requête | Table introuvable | La table spécifiée dans la requête est introuvable |
| **42P07** | Requête | La table existe | Il existe déjà une table portant le même nom (CREATE TABLE) |
| **53400** | Requête | LIMIT dépasse la valeur maximale | L’utilisateur a spécifié une clause LIMIT supérieure à 100 000 |
| **53400** | Requête | Délai d’expiration de la déclaration | La déclaration soumise en direct a duré plus de 10 minutes au maximum |
| **58000** | Requête | Erreur système | Échec du système interne |
| **0A000** | Requête/Commande | Non pris en charge | La fonctionnalité de la requête/commande n’est pas prise en charge |
| **42501** | Requête DROP TABLE | Table de dépôt non créée par Query Service | La table en cours de suppression n’a pas été créée par Query Service à l’aide de l’instruction `CREATE TABLE` |
| **42501** | Requête DROP TABLE | Tableau non créé par l’utilisateur authentifié | La table en cours de suppression n’a pas été créée par l’utilisateur actuellement connecté. |
| **42P01** | Requête DROP TABLE | Table introuvable | La table spécifiée dans la requête est introuvable. |
| **42P12** | Requête DROP TABLE | Aucune table trouvée pour `dbName` : consultez la section `dbName` | Aucune table n’a été trouvée dans la base de données actuelle |
