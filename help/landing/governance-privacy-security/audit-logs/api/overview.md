---
title: Guide de l’API Query Audit
description: La requête d’audit est une API RESTful qui permet aux développeurs de voir qui a effectué les actions dans Adobe Experience Platform.
role: Developer
feature: Audits, API
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 9%

---

# Guide de l’API [!DNL Audit Query]

L’API [!DNL Audit Query] fournit des points de terminaison qui vous permettent de récupérer et de surveiller par programmation les données d’événement pour diverses fonctionnalités de Adobe Experience Platform. Les points de terminaison sont décrits ci-dessous. Consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d’exemples d’appels API, etc.

Pour afficher tous les points d’entrée et opérations CRUD disponibles, consultez le document Swagger de l’[[!DNL Audit Query] API](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Événements

Les événements d’audit fournissent des informations sur les actions de l’utilisateur dans Platform, notamment le type d’action, la date et l’heure, l’e-mail de l’utilisateur qui a exécuté l’action et des attributs supplémentaires liés au type d’action pour diverses fonctionnalités de Adobe Experience Platform. Pour savoir comment récupérer des mesures à l’aide de l’API, consultez le [guide de point de terminaison events](./events.md).

## Exporter

L’exportation d’audit vous permet de récupérer des données d’événements en spécifiant les événements que vous souhaitez récupérer dans la payload. Pour savoir comment récupérer des mesures à l’aide de l’API, consultez le [guide de point de terminaison d’exportation](./export.md).
