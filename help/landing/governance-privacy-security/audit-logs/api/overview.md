---
title: Guide de l’API Audit Query
description: La requête d’audit est une API RESTful qui permet aux développeurs de voir qui a effectué quelles actions dans Adobe Experience Platform.
role: Developer
feature: Audits, API
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
TQID: https://experienceleague.adobe.com/vLh0ElepKDmpAAhvlc3e5XvBSgvjqfkdGqI3ELKgZkg
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: e1e0219c-f879-479f-8427-888ed2a6e9c2id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 9eb5b266c15495d852a671829d46fd127ad33ac9
workflow-type: tm+mt
source-wordcount: 179
ht-degree: 8%

---

# Guide de l’API [!DNL Audit Query]

L’API [!DNL Audit Query] fournit des points d’entrée qui vous permettent de récupérer et de surveiller par programmation les données d’événement pour diverses fonctionnalités de Adobe Experience Platform. Les points d’entrée sont décrits ci-dessous. Consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d’exemples d’appels API, etc.

Pour afficher tous les points d’entrée et opérations CRUD disponibles, consultez le document Swagger de l’[[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query).

## Événements

Les événements d’audit fournissent des informations sur les actions des utilisateurs dans Experience Platform, notamment le type d’action, la date et l’heure, l’ID d’e-mail de l’utilisateur qui a exécuté l’action et des attributs supplémentaires liés au type d’action pour diverses fonctionnalités de Adobe Experience Platform. Pour savoir comment récupérer des mesures à l’aide de l’API, consultez le guide [point d’entrée des événements](./events.md).

## Exporter

L’exportation d’audit vous permet de récupérer les données d’événement en spécifiant les événements que vous souhaitez récupérer dans la payload. Pour savoir comment récupérer des mesures à l’aide de l’API, consultez le guide [d’exportation des points d’entrée](./export.md).
