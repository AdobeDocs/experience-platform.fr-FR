---
title: onBeforeLinkClickSend
description: Rappel s’exécutant juste avant l’envoi des données de suivi des liens.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
TQID: https://experienceleague.adobe.com/YwogdzhVCX18A0mzpd1WfsIqyC6zGsUDTEH9O70-FXM
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 173
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Ce rappel est obsolète. Utilisez [`clickCollection.filterClickDetails`](clickcollection.md) à la place.

Le rappel `onBeforeLinkClickSend` vous permet d’enregistrer une fonction JavaScript qui peut modifier les données de suivi des liens que vous envoyez juste avant que ces données ne soient envoyées à Adobe. Il vous permet de manipuler le `xdm` ou `data` objet, notamment d’ajouter, de modifier ou de supprimer des éléments. Vous pouvez également annuler de manière conditionnelle l’envoi de données, par exemple avec le trafic de robots côté client détecté.

Ce rappel s’exécute uniquement si [`clickCollectionEnabled`](clickcollectionenabled.md) est activé et `filterClickDetails` ne contient pas de fonction enregistrée.

Si [`onBeforeEventSend`](onbeforeeventsend.md) et `onBeforeLinkClickSend` contiennent tous deux des fonctions enregistrées, `onBeforeLinkClickSend` est exécuté en premier.

>[!WARNING]
>
>Ce rappel permet d’utiliser du code personnalisé. Si un code que vous incluez dans le rappel renvoie une exception non interceptée, le traitement de l’événement s’arrête. Les données ne sont pas envoyées à Adobe.

## `onBeforeLinkClickSend` et `filterClickDetails`

Le rappel [`clickCollection.filterClickDetails`](clickcollection.md) est conçu pour remplacer `onBeforeLinkClickSend`. Adobe déconseille vivement d’affecter des fonctions de rappel aux deux simultanément. Si vous attribuez une fonction de rappel à la fois à `filterClickDetails` et à `onBeforeLinkClickSend`, la bibliothèque utilise la logique suivante :

* Seul `filterClickDetails` s’exécute ; `onBeforeLinkClickSend` ne s’exécute pas.
* Le regroupement d’événements `clickCollection.eventGroupingEnabled` ne fonctionne pas.
