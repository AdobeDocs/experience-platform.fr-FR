---
title: Annexe du guide de l’API pour l’outil Sandbox
description: Ce document fournit des informations supplémentaires relatives à l’utilisation de l’API Sandbox Tooling.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
TQID: https://experienceleague.adobe.com/8KgZMBnGDJXF4WTLW-K39GWcXExG3yyRNXaIh-gP1cQ
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 190
ht-degree: 2%

---

# Annexe du guide de l’API Sandbox

Ce document fournit des informations supplémentaires relatives à l’utilisation de l’API [!DNL Sandbox].

## Utiliser des paramètres de requête {#query}

L’API Sandbox Tooling prend en charge l’utilisation de paramètres de requête pour paginer et filtrer les résultats lors de l’énumération des packages.

>[!NOTE]
>
>Le `limit` peut être transmis et démarré individuellement.

| Paramètre | Description |
| --- | --- |
| `limit` | Nombre maximal d’enregistrements à renvoyer dans la réponse. La limite par défaut est de 20. |
| `start` | Début de l’emplacement où doit commencer une liste d’éléments sous-définie. |
| `targetSandbox` | Représente le nom du sandbox dans lequel vous souhaitez importer vos artefacts. |
| `jobType` | Type de tâche. Cette valeur peut être `NEW`, `RESUME` ou `ROLLBACK`. |
| `jobStatus` | Statut de la tâche. Cette valeur peut être `PENDING`, `IN_PROGRESS`, `SUCCESS`, `FAILED` ou `CANCELLED`. |
| `requestType` | Type de demande. Cette valeur peut être `EXPORT`, `IMPORT` ou `COPY`. |
| `expiryPeriod` | Cette période spécifiée par l’utilisateur définit la date d’expiration du package (en jours) à partir de l’heure de publication du package. Cette valeur ne doit pas être négative. La valeur par défaut est de 90 jours à compter de l’appel de l’API de mise à jour ou de publication. |
| `packageType` | Type de package. Cette valeur peut être `PARTIAL` ou `FULL`. |
| `status` | Statut du package. Cette valeur peut être `DRAFT`, `PUBLISHED`, `PUBLISH_IN_PROGRESS` ou `PUBLISH_FAILED`. |
