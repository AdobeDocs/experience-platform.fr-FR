---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;environnement de test;environnement de test;environnements de test;environnements de test
solution: Experience Platform
title: Annexe du guide de l’API Sandbox
description: Ce document fournit des informations supplémentaires sur l’utilisation de l’API Sandbox.
topic-legacy: developer guide
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---

# Annexe du guide de l’API Sandbox

Ce document fournit des informations supplémentaires relatives à l’utilisation de la fonction [!DNL Sandbox] API.

## Utilisation des paramètres de requête {#query}

Le [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) prend en charge l’utilisation de paramètres de requête pour la page et le filtrage des résultats lors de la liste des environnements de test.

>[!NOTE]
>
>Le `limit` et `offset` les paramètres de requête doivent être spécifiés ensemble. Si vous n’en spécifiez qu’une seule, l’API renvoie une erreur. Si vous n’indiquez aucun paramètre, la limite par défaut est de 50 et le décalage est de 0.

| Paramètre | Description |
| --- | --- |
| `limit` | Nombre maximal d’enregistrements à renvoyer dans la réponse. |
| `offset` | Nombre d’entités du premier enregistrement à partir duquel commencer (décaler) la liste de réponses. |
