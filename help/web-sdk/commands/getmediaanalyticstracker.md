---
title: getMediaAnalyticsTracker
description: Découvrez comment créer un objet de suivi Media Analytics et l’utiliser pour effectuer le suivi des événements multimédia.
source-git-commit: 9384c1cc15441199e898d6cc0850e5422253f106
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---


# `getMediaAnalyticsTracker`

Cette commande du SDK Web récupère un outil de suivi Media Analytics. Vous pouvez utiliser cette commande pour créer une instance d’objet, puis, en utilisant les mêmes API que celles fournies par la variable [Bibliothèque JS Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), effectuez le suivi des événements multimédia.

La variable `getMediaAnalyticsTracker` renvoie l’API Media Analytics héritée.


| Nom de la méthode | Description | Syntaxe |
|-----------------|---|----------------|
| `getInstance` | Crée une instance de média pour effectuer le suivi de la session de lecture. | `Media.getInstance()` |
| `createMediaObject` | Crée un objet contenant des informations sur le média. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | Crée un objet contenant des informations sur le saut de page. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | Crée un objet contenant des informations sur les publicités. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | Crée un objet contenant des informations sur le chapitre. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | Crée un objet contenant des informations sur l’état. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createStateObject(name)` |
| `createQoEObject` | Crée un objet contenant des informations sur la qualité de l’expérience. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## Méthodes d’instance

| Nom de la méthode | Description | Syntaxe |
|---|---|----|
| `trackSessionStart` | Suivez l’intention de démarrer la lecture. Cela lance une session de suivi sur l’instance de suivi multimédia. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | Effectuez le suivi de la lecture ou de la reprise du média après une interruption précédente. | `trackerInstance.trackPlay()` |
| `trackPause` | Suivi de la mise en pause du média | `trackerInstance.trackPause()` |
| `trackComplete` | Suivi du média terminé Appelez cette méthode uniquement lorsque le média a été entièrement visionné. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | Suivez la fin d’une session de visionnage. Appelez cette méthode même si l’utilisateur ne voit pas le média jusqu’à la fin. | `trackerInstance.trackSessionEnd()` |
| `trackError` | Suivi d’une erreur qui s’est produite pendant la lecture multimédia. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | Suivi d’un événement personnalisé. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | Mettez à jour le curseur de lecture. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | Mettez à jour la qualité de l’expérience. | `trackerInstance.updateQoEObject(qoe)` |

## Constantes

| Nom de constante | Description | Valeur |
|-----------------|--|-----------------|
| `MediaType` | Type de média | `Video`, `Audio` |
| `StreamType` | Type de flux | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | Cela définit les clés de métadonnées standard pour les flux vidéo. | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed`, `StreamFormat` |
| `AudioMetadataKeys` | Cela définit les clés de métadonnées standard pour les diffusions audio. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | Cela définit les clés de métadonnées standard pour les publicités. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | Cela définit le type d’un événement de suivi. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart`, `StateEnd` |
| `PlayerState` | Cela définit des valeurs standard pour le suivi de l’état du lecteur. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |
