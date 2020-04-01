---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de dépannage du service de  Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda

---


# Erreurs et dépannage

## Erreurs d’API REST

| Code d’état HTTP | Description | Causes possibles |
| ---------------- | ----------- | --------------- |
| 400 | Requête incorrecte | malformé ou illégal |
| 401 | Échec de l&#39;authentification | Jeton d&#39;authentification non valide |
| 500 | Erreur du serveur interne | Échec du système interne |

## Erreurs de l&#39;API PostgreSQL

| Code d’erreur et état de connexion | Description | Cause possible |
| ------------------------------- | ----------- | -------------- |
| **28P01** - authentification | Mot de passe non valide | Jeton d’authentification non valide |
| **28000**  - authentification | Type d&#39;autorisation non valide | Type d&#39;autorisation non valide. Ça doit être `AuthenticationCleartextPassword`. |
| **42P12**  - authentification | Aucune table trouvée | Aucune table n&#39;a été trouvée pour utilisation |
| **42601**  | Erreur de syntaxe | Erreur de commande ou de syntaxe non valide |
| **58000**  | Erreur système | Échec du système interne |
| **42P01**  | Tableau introuvable | La table spécifiée dans le  du est introuvable |
| **42P07** | Le tableau existe | Le tableau porte déjà le même nom (CREATE TABLE) |
| **53400**  | LIMIT dépasse la valeur maximale | L’utilisateur a spécifié une clause LIMIT supérieure à 100 000 |
| **53400**  | Délai d’expiration du relevé | La déclaration en direct soumise a duré plus de 10 minutes au maximum. |
| **08P01** S/O | Type de message non pris en charge | Type de message non pris en charge |
