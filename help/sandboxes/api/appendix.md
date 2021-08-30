---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;environnement de test;environnement de test;environnements de test;environnements de test
solution: Experience Platform
title: Annexe du guide de l’API Sandbox
description: Ce document fournit des informations supplémentaires sur l’utilisation de l’API Sandbox.
topic-legacy: developer guide
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---

# Annexe du guide de l’API Sandbox

Ce document fournit des informations supplémentaires sur l’utilisation de l’API [!DNL Sandbox].

## Utilisation des paramètres de requête {#query}

L’ [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) prend en charge l’utilisation de paramètres de requête pour la page et le filtrage des résultats lors de la mise en liste des environnements de test.

>[!NOTE]
>
>Les paramètres de requête `limit` et `offset` doivent être spécifiés ensemble. Si vous n’en spécifiez qu’une seule, l’API renvoie une erreur. Si vous n’indiquez aucun paramètre, la limite par défaut est de 50 et le décalage est de 0.

| Paramètre | Description |
| --- | --- |
| `limit` | Nombre maximal d’enregistrements à renvoyer dans la réponse. |
| `offset` | Nombre d’entités du premier enregistrement à partir duquel commencer (décaler) la liste de réponses. |
