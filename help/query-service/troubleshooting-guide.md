---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;guide de dépannage;faq;dépannage;
solution: Experience Platform
title: Guide de dépannage de Query Service
topic-legacy: troubleshooting
description: Ce document contient des informations sur les codes d’erreur courants que vous rencontrez et les causes possibles.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 03cd013e35872bcc30c68508d9418cb888d9e260
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 14%

---

# Guide de dépannage du [!DNL Query Service]

Ce document fournit des réponses aux questions fréquentes sur Query Service et fournit une liste des codes d’erreur courants lors de l’utilisation de Query Service. Pour toute question ou dépannage concernant les autres services d’Adobe Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

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

### Comment modifier le fuseau horaire en horodatage UTC ?

Adobe Experience Platform conserve les données au format d’horodatage UTC (temps universel coordonné). Exemple de format UTC : `2021-12-22T19:52:05Z`

Query Service prend en charge les fonctions SQL intégrées pour convertir un horodatage donné au format UTC et à partir de ce format. Les deux `to_utc_timestamp()` et le `from_utc_timestamp()` Les méthodes prennent deux paramètres : horodatage et fuseau horaire.

| Paramètre | Description |
|---|---|
| Horodatage | L’horodatage peut être écrit au format UTC ou simple. `{year-month-day}` format. Si aucune heure n’est fournie, la valeur par défaut est minuit le matin du jour donné. |
| Fuseau horaire | Le fuseau horaire est écrit dans une `{continent/city})` format. Il doit s’agir de l’un des codes de fuseau horaire reconnus, comme indiqué dans la variable [base de données TZ du domaine public](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Convertir en horodatage UTC

Le `to_utc_timestamp()` interprète les paramètres donnés et les convertit **à l’horodatage de votre fuseau horaire local.** au format UTC. Par exemple, le fuseau horaire à Séoul, en Corée du Sud, est UTC/GMT +9 heures. En fournissant un horodatage date seule, la méthode utilise une valeur par défaut de minuit le matin. L’horodatage et le fuseau horaire sont convertis au format UTC de l’heure de cette région en horodatage UTC de votre région locale.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

La requête renvoie un horodatage à l’heure locale de l’utilisateur. Dans ce cas, la veille à 15h00 comme à Séoul, il y a neuf heures d&#39;avance.

```
2021-08-30 15:00:00
```

Autre exemple : si l’horodatage donné a été `2021-07-14 12:40:00.0` pour le `Asia/Seoul` fuseau horaire, l’horodatage UTC renvoyé serait `2021-07-14 03:40:00.0`

La sortie de console fournie dans l’interface utilisateur de Query Service est plus lisible :

```
8/30/2021, 3:00 PM
```

### Convertir à partir de l’horodatage UTC

Le `from_utc_timestamp()` interprète les paramètres donnés. **à partir de l’horodatage de votre fuseau horaire local** et fournit l’horodatage équivalent de la région souhaitée au format UTC. Dans l’exemple ci-dessous, l’heure est 14 h 40 dans le fuseau horaire local de l’utilisateur. Le fuseau horaire de Séoul passé en tant que variable est neuf heures avant le fuseau horaire local.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

La requête renvoie un horodatage au format UTC pour le fuseau horaire transmis en tant que paramètre. Le résultat est neuf heures avant le fuseau horaire qui a exécuté la requête.

```
8/31/2021, 11:40 PM
```

### Comment dois-je filtrer mes données de série temporelle ?

Lors de l’interrogation des données de série temporelle, vous devez utiliser le filtre d’horodatage chaque fois que cela est possible pour une analyse plus précise.

>[!NOTE]
>
> Chaîne de date **must** être au format `yyyy-mm-ddTHH24:MM:SS`.

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

Vous ne pouvez pas utiliser de caractères génériques pour obtenir toutes les données de vos lignes, car Query Service doit être traité comme un **columnar-store** plutôt qu’un système de magasin traditionnel basé sur les lignes.

### Dois-je utiliser `NOT IN` dans ma requête SQL ?

Le `NOT IN` est souvent utilisé pour récupérer les lignes qui ne figurent pas dans une autre table ou instruction SQL. Cet opérateur peut ralentir les performances et renvoyer des résultats inattendus si les colonnes comparées acceptent `NOT NULL`, ou vous avez un grand nombre d’enregistrements.

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

Si vous utilisez la variable `NOT EXISTS` , vous pouvez répliquer à l’aide de l’opérateur `NOT IN` en utilisant la requête suivante :

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Si vous utilisez la méthode `LEFT OUTER JOIN` , vous pouvez répliquer à l’aide de l’opérateur `NOT IN` en utilisant la requête suivante :

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### Quelle est la bonne utilisation de la variable `OR` et `UNION` opérateurs ?

### Comment utiliser correctement la variable `CAST` pour convertir mes horodatages dans les requêtes SQL ?

Lors de l’utilisation de la variable `CAST` pour convertir un horodatage, vous devez inclure la date **et** temps.

Par exemple, l’absence du composant temporel, comme illustré ci-dessous, entraînera une erreur :

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Une utilisation correcte de la variable `CAST` est illustré ci-dessous :

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

### Comment télécharger mes résultats de requête sous la forme d’un fichier CSV ?

Il ne s’agit pas d’une fonctionnalité que Query Service propose directement. Cependant, si la variable [!DNL PostgreSQL] Le client utilisé pour se connecter au serveur de base de données dispose de la fonctionnalité , la réponse d’une requête SELECT peut être écrite et téléchargée sous la forme d’un fichier CSV. Reportez-vous à la documentation de l’utilitaire ou de l’outil tiers que vous utilisez pour clarifier ce processus.

## Erreurs de l’API REST

| Code d’état HTTP | Description | Causes possibles |
| ---------------- | ----------- | --------------- |
| 400 | Mauvaise requête | Requête malformée ou illégale |
| 401 | Échec de l’authentification | Jeton d’authentification non valide |
| 500 | Erreur interne du serveur | Échec du système interne |

## Erreurs de l’API PostgreSQL

| Code erreur | État de la connexion | Description | Cause possible |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | S/O | Type de message non pris en charge | Type de message non pris en charge |
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
| **42501** | Requête DROP TABLE | Table de dépôt non créée par Query Service | La table en cours de suppression n’a pas été créée par Query Service à l’aide de l’événement `CREATE TABLE` statement |
| **42501** | Requête DROP TABLE | Tableau non créé par l’utilisateur authentifié | La table en cours de suppression n’a pas été créée par l’utilisateur actuellement connecté. |
| **42P01** | Requête DROP TABLE | Table introuvable | La table spécifiée dans la requête est introuvable. |
| **42P12** | Requête DROP TABLE | Aucune table trouvée pour `dbName`: veuillez consulter la section `dbName` | Aucune table n’a été trouvée dans la base de données actuelle |
