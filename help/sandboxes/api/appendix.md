---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;sandbox;Sandbox;sandbox
solution: Experience Platform
title: Annexe du guide de l’API Sandbox
description: Ce document fournit des informations supplémentaires relatives à l’utilisation de l’API Sandbox.
role: Developer
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
TQID: https://experienceleague.adobe.com/2g4jpjQ-UIrUXjk-PnmtFkxr-2d-ZpO06dKOT-oMvkI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 128
ht-degree: 9%

---

# Annexe du guide de l’API Sandbox

Ce document fournit des informations supplémentaires relatives à l’utilisation de l’API [!DNL Sandbox].

## Utiliser des paramètres de requête {#query}

L’[[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) prend en charge l’utilisation de paramètres de requête pour paginer et filtrer les résultats lors de l’énumération des sandbox.

>[!NOTE]
>
>Les paramètres de requête `limit` et `offset` doivent être spécifiés ensemble. Si vous n’en spécifiez qu’une seule, l’API renvoie une erreur. Si vous ne spécifiez aucun, la limite par défaut est 50 et le décalage est 0.

| Paramètre | Description |
| --- | --- |
| `limit` | Nombre maximal d’enregistrements à renvoyer dans la réponse. |
| `offset` | Nombre d’entités du premier enregistrement à partir duquel démarrer (décaler) la liste de réponse. |
