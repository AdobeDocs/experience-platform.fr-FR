---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;guide de dépannage;faq;dépannage;
solution: Experience Platform
title: Guide de dépannage de Query Service
topic-legacy: troubleshooting
description: Ce document contient des informations sur les codes d’erreur courants que vous rencontrez et les causes possibles.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: e3557fe75680153f051b8a864ad8f6aca5f743ee
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 40%

---

# Guide de dépannage du [!DNL Query Service]

Ce document fournit des réponses aux questions fréquentes sur Query Service et fournit une liste des codes d’erreur courants lors de l’utilisation de Query Service. Pour toute question ou dépannage concernant les autres services d’Adobe Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

## Questions fréquemment posées

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
WHERE timestamp >= To_timestamp('2021-01-21 12:00:00')
AND timestamp < To_timestamp('2021-01-21 13:00:00')
LIMIT 100;
```

### Comment dois-je filtrer mes données de série temporelle ?

Lors de l’interrogation des données de série temporelle, vous devez utiliser le filtre d’horodatage chaque fois que cela est possible pour une analyse plus précise.

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

## Erreurs de l’API REST

| Code d’état HTTP | Description | Causes possibles |
| ---------------- | ----------- | --------------- |
| 400 | Mauvaise requête | Requête malformée ou illégale |
| 401 | Échec de l’authentification | Jeton d’authentification non valide |
| 500 | Erreur interne du serveur | Échec du système interne |

## Erreurs de l’API PostgreSQL

| Code d’erreur et état de la connexion | Description | Cause possible |
| ------------------------------- | ----------- | -------------- |
| **28P01** Start-up - authentication | Mot de passe non valide | Jeton d’authentification non valide |
| **28000** Start-up - authentication | Type d’autorisation non valide | Type d’autorisation non valide. Doit être `AuthenticationCleartextPassword`. |
| **42P12** Start-up - authentication | Aucune table trouvée | Aucune table n’a été trouvée pour utilisation |
| **42601** Query | Erreur de syntaxe | Erreur de syntaxe ou de commande non valide |
| **58000** Query | Erreur système | Échec du système interne |
| **42P01** Query | Table introuvable | La table spécifiée dans la requête est introuvable |
| **42P07** Query | La table existe | La table porte déjà le même nom (CREATE TABLE) |
| **53400** Query | LIMIT dépasse la valeur maximale | L’utilisateur a spécifié une clause LIMIT supérieure à 100 000 |
| **53400** Requête | Délai d’expiration de la déclaration | La déclaration soumise en direct a duré plus de 10 minutes au maximum |
| **08P01** N/A | Type de message non pris en charge | Type de message non pris en charge |
