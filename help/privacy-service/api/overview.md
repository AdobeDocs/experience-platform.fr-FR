---
title: Guide de l’API Privacy Service
description: Découvrez comment utiliser l’API Privacy Service pour gérer par programmation les tâches de confidentialité pour les applications Adobe Experience Cloud prises en charge.
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
TQID: https://experienceleague.adobe.com/R3W8RDh35UrxTL-ZQAHrRC6nr1Ix3snMEBD8v87nUY8
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: cb424651efb1b4d71717c06a4b0d6e9354f0dcc7
workflow-type: tm+mt
source-wordcount: 268
ht-degree: 17%

---

# Guide de l’API [!DNL Privacy Service]

L’API Privacy Service fournit plusieurs points d’entrée vous permettant de gérer par programmation les tâches de confidentialité de votre organisation. Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

>[!NOTE]
>
>Ce guide explique comment utiliser l’API [!DNL Privacy Service]. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez la présentation de l’interface utilisateur de Privacy Service [&#128279;](../ui/overview.md).

Pour afficher tous les points d’entrée et opérations CRUD disponibles, consultez la référence de l’API Privacy Service [&#128279;](https://developer.adobe.com/experience-platform-apis/references/privacy-service).

## Tâches de confidentialité

Lorsque Privacy Service reçoit une demande d’accès ou de suppression des données personnelles d’un sujet, le système crée des tâches de confidentialité pour répondre à cette demande. Chaque tâche de confidentialité contient des informations d’identité relatives au titulaire de données, des métadonnées sur le produit Adobe Experience Cloud auquel la tâche s’applique et l’état de traitement de la tâche.

Le point d’entrée `/jobs` vous permet de créer et de récupérer des tâches de confidentialité pour votre organisation. Pour savoir comment utiliser ce point d’entrée, consultez le guide [des points d’entrée des tâches de confidentialité](./privacy-jobs.md).

## Consentement

Certaines réglementations nécessitent le consentement explicite du client avant que ses données personnelles puissent être collectées. Le point d’entrée `/consent` vous permet de traiter les demandes de consentement des clients et de les intégrer à votre workflow de confidentialité. Pour en savoir plus[&#128279;](./consent.md) consultez le  guide des points d’entrée de consentement .

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API Privacy Service, lisez le [&#x200B; guide de prise en main &#x200B;](./getting-started.md) puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques.

