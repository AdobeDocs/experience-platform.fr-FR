---
solution: Experience Platform
title: Présentation de la collecte de données
description: Découvrez comment envoyer des données à Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
TQID: https://experienceleague.adobe.com/cZl7JCCNUNwni6DKqQeyyH7qaup0HFDpxm0NiJYN4S8
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: abc02dd6-664f-446a-9aaa-675bc0f2fe4aid: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1c
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 296
ht-degree: 7%

---

# Présentation de la collecte de données

Adobe Experience Platform fournit un ensemble de technologies qui vous permettent de collecter des données d’expérience client à partir de diverses sources et de les envoyer à Adobe Experience Platform Edge Network. Ces données peuvent ensuite être enrichies, transformées et distribuées vers des destinations Adobe ou autres qu’Adobe.

Adobe prend en charge les langages de code suivants avec des bibliothèques dédiées pour la collecte de données :

* **** : pour les sites web et les applications web
* **Kotlin** : pour les appareils Android
* **Swift** : pour les appareils iOS
* **Brightscript** : pour les appareils Roku
* **Flutter** : pour les applications Android + iOS utilisant Flutter
* **** : pour les applications Android + iOS utilisant React Native

L’interface utilisateur des balises dans la collecte de données Adobe Experience Platform comprend une extension Web SDK et Mobile SDK.

Si aucun des SDK ci-dessus ne répond aux besoins de votre projet, vous pouvez utiliser l’API [Adobe Experience Platform Edge Network](https://developer.adobe.com/data-collection-apis/docs/) pour envoyer directement des données à Adobe.

## Processus de collecte de données

Au lieu d’installer et de mettre en œuvre des bibliothèques individuelles distinctes pour chaque produit Adobe, vous pouvez mettre en œuvre l’un des SDK ou extensions de balises ci-dessus pour agréger toutes les données souhaitées en une seule payload. Cette payload est envoyée à un [flux de données](/help/datastreams/overview.md) dans Adobe Experience Platform Edge Network.

![Diagramme de collecte de données](assets/tags-sdks.png)

Adobe Experience Platform Edge Network est un réseau de serveurs distribué dans le monde entier, rapide et fiable, capable de recevoir et de traiter des données à très grande échelle. Lorsqu’un flux de données reçoit des données, il les distribue à chaque solution respective que vous avez configurée. Les données sont transmises dans un format compris par chaque produit.

![diagramme de solutions ](assets/adobe-solutions.png)

Vous pouvez également utiliser le [transfert d’événement](/help/tags/ui/event-forwarding/overview.md) pour transformer, enrichir et envoyer des données à n’importe quelle destination non Adobe avec une faible latence et sans code d’implémentation côté client.

![Diagramme de transfert d’événement](assets/event-forwarding.png)
