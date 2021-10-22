---
title: Guide de l’API Privacy Service
description: Découvrez comment utiliser l’API du Privacy Service pour gérer par programme les tâches de confidentialité pour les applications Adobe Experience Cloud prises en charge.
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 32%

---

# Guide de l’API [!DNL Privacy Service]

L’API du Privacy Service fournit plusieurs points de terminaison qui vous permettent de gérer par programme les tâches de confidentialité pour votre entreprise. Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

>[!NOTE]
>
>Ce guide explique comment utiliser la [!DNL Privacy Service] API. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez la [présentation de l’interface utilisateur de Privacy Service](../ui/overview.md).

Pour afficher tous les points de terminaison et les opérations CRUD disponibles, consultez la page [Référence de l’API Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Tâches de confidentialité

Lorsque le Privacy Service reçoit une demande d’accès ou de suppression des données personnelles d’un sujet, le système crée des tâches de confidentialité pour répondre à cette demande. Chaque tâche de protection de la vie privée contient des informations d&#39;identité relatives à la personne concernée, des métadonnées sur le produit Adobe Experience Cloud auquel elle s&#39;applique et l&#39;état de traitement de la tâche.

Le `/jobs` endpoint vous permet de créer et de récupérer des tâches de confidentialité pour votre entreprise. Pour savoir comment utiliser ce point de terminaison, consultez la section [guide de fin des tâches de confidentialité](./privacy-jobs.md).

## Consentement

Certains règlements exigent un consentement explicite de la part des clients avant que leurs données personnelles puissent être collectées. Le `/consent` endpoint vous permet de traiter les demandes de consentement client et de les intégrer à votre flux de travaux de confidentialité. Voir la section [guide de point de terminaison de consentement](./consent.md) pour en savoir plus.

## Étapes suivantes

Pour commencer à effectuer des appels à lʼaide de lʼAPI Schema Registry, consultez le [guide de prise en main](./getting-started.md), puis sélectionnez lʼun des guides des points dʼentrée pour savoir comment utiliser des points dʼentrée spécifiques.
