---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;environnement de test;environnement de test;environnements de test;environnements de test
solution: Experience Platform
title: Annexe du guide de l’API Sandbox
description: Ce document fournit des informations supplémentaires sur l’utilisation de l’API Sandbox.
role: Developer
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---

# Annexe du guide de l’API Sandbox

Ce document fournit des informations supplémentaires sur l’utilisation de l’API [!DNL Sandbox].

## Utilisation des paramètres de requête {#query}

L’ [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) prend en charge l’utilisation des paramètres de requête pour la page et le filtrage des résultats lors de la liste des environnements de test.

>[!NOTE]
>
>Les paramètres de requête `limit` et `offset` doivent être spécifiés ensemble. Si vous n’en spécifiez qu’une seule, l’API renvoie une erreur. Si vous n’indiquez aucun paramètre, la limite par défaut est de 50 et le décalage est de 0.

| Paramètre | Description |
| --- | --- |
| `limit` | Nombre maximal d’enregistrements à renvoyer dans la réponse. |
| `offset` | Nombre d’entités du premier enregistrement à partir duquel commencer (décaler) la liste de réponses. |
