---
title: Annexe du guide de l’API des outils Sandbox
description: Ce document fournit des informations supplémentaires sur l’utilisation de l’API Sandbox Tooling.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 2%

---

# Annexe du guide de l’API Sandbox

Ce document fournit des informations supplémentaires sur l’utilisation de l’API [!DNL Sandbox].

## Utilisation des paramètres de requête {#query}

L’API d’outils Sandbox prend en charge l’utilisation de paramètres de requête pour paginer et filtrer les résultats lors de la mise en liste de modules.

>[!NOTE]
>
>Le `limit` peut être transmis et démarré individuellement.

| Paramètre | Description |
| --- | --- |
| `limit` | Nombre maximal d’enregistrements à renvoyer dans la réponse. La limite par défaut est 20. |
| `start` | Début de l’emplacement où une liste d’éléments sous-définie doit commencer. |
| `targetSandbox` | Représente le nom de l’environnement de test dans lequel vous souhaitez importer vos artefacts. |
| `jobType` | Type de tâche. Cette valeur peut être NEW, RESUME et ROLLBACK. |
| `jobStatus` | État de la tâche. Cette valeur peut être EN ATTENTE, IN_PROGRESS, SUCCESS, FAILED et CANCELLED. |
| `requestType` | Type de requête. Cette valeur peut être EXPORT, IMPORT et COPY. |
| `expiryPeriod ` | Cette période spécifiée par l’utilisateur définit la date d’expiration du module (en jours) à partir du moment où le module a été publié. Cette valeur ne doit pas être négative. La valeur par défaut est de 90 jours à compter de l’appel de l’API de mise à jour ou de publication. |
