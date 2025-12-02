---
title: onBeforeLinkClickSend
description: Rappel s’exécutant juste avant l’envoi des données de suivi des liens.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
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
