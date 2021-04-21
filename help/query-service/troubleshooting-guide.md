---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de requête ; service de Requête ; guide de dépannage ; faq ; dépannage ;
solution: Experience Platform
title: Guide de dépannage de requête Service
topic-legacy: troubleshooting
description: Ce document contient des informations sur les codes d'erreur courants que vous rencontrez et les causes possibles.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 82%

---

# [!DNL Query Service] Guide de dépannage

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
