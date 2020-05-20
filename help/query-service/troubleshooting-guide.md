---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de dépannage d’Adobe Experience Platform Requête Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 5%

---


# Erreurs et dépannage

## Erreurs d’API REST

| Code d’état HTTP | Description | Causes possibles |
| ---------------- | ----------- | --------------- |
| 400 | Requête incorrecte | requête incorrecte ou illégale |
| 401 | Échec de l&#39;authentification | Jeton d&#39;authentification non valide |
| 500 | Erreur interne du serveur | Échec du système interne |

## Erreurs de l&#39;API PostgreSQL

| Code d’erreur et état de connexion | Description | Cause possible |
| ------------------------------- | ----------- | -------------- |
| **Début 28P01** - authentification | Mot de passe non valide | Jeton d&#39;authentification non valide |
| **Début 28000** - authentification | Type d&#39;autorisation non valide | Type d&#39;autorisation non valide. Ça doit être `AuthenticationCleartextPassword`. |
| **Début 42P12** - authentification | Aucune table trouvée | Aucune table trouvée à utiliser |
| **Requête 42601** | Erreur de syntaxe | Erreur de syntaxe ou de commande non valide |
| **58000** Requête | Erreur système | Échec du système interne |
| **Requête 42P01** | Tableau introuvable | La table spécifiée dans la requête est introuvable |
| **Requête 42P07** | La table existe | La table porte déjà le même nom (CREATE TABLE) |
| **Requête 53400** | LIMIT dépasse la valeur maximale | L&#39;utilisateur a spécifié une clause LIMIT supérieure à 100 000 |
| **Requête 53400** | Délai d’expiration du relevé | La déclaration en direct soumise a duré plus de 10 minutes au maximum. |
| **08P01** S/O | Type de message non pris en charge | Type de message non pris en charge |
