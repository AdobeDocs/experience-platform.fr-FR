---
title: Guide de l’API Privacy Service
description: Découvrez comment utiliser l’API du Privacy Service pour gérer par programmation les tâches de confidentialité pour les applications Adobe Experience Cloud prises en charge.
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 15%

---

# Guide de l’API [!DNL Privacy Service]

L’API du Privacy Service fournit plusieurs points de terminaison qui vous permettent de gérer par programmation les tâches de confidentialité pour votre organisation. Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

>[!NOTE]
>
>Ce guide explique comment utiliser l’API [!DNL Privacy Service]. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez la [présentation de l’interface utilisateur de Privacy Service](../ui/overview.md).

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, consultez la [référence d’API Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Tâches de confidentialité

Lorsque Privacy Service reçoit une demande d’accès ou de suppression des données personnelles d’un sujet, le système crée des tâches de confidentialité pour répondre à cette demande. Chaque tâche de confidentialité contient des informations d’identité liées au sujet des données, des métadonnées sur le produit Adobe Experience Cloud auquel la tâche s’applique et l’état de traitement de la tâche.

Le point de terminaison `/jobs` vous permet de créer et de récupérer des tâches de confidentialité pour votre organisation. Pour savoir comment utiliser ce point de terminaison, consultez le [guide de point de terminaison des tâches de confidentialité](./privacy-jobs.md).

## Consentement

Certaines réglementations exigent un consentement explicite de la part du client avant que leurs données personnelles puissent être collectées. Le point de terminaison `/consent` vous permet de traiter les demandes de consentement des clients et de les intégrer à votre workflow de confidentialité. Pour en savoir plus, consultez le [guide de point de terminaison du consentement](./consent.md) .

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API de Privacy Service, lisez le [guide de prise en main](./getting-started.md) , puis sélectionnez l’un des guides de point de terminaison pour savoir comment utiliser des points de terminaison spécifiques.
