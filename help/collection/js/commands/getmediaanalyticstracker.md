---
title: getMediaAnalyticsTracker
description: Découvrez comment créer un objet de suivi Media Analytics et l’utiliser pour effectuer le suivi des événements multimédia.
exl-id: ae968da8-7763-4b2a-a716-3014ba0d270d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# `getMediaAnalyticsTracker`

Cette commande Web SDK récupère un outil de suivi Media Analytics. Vous pouvez utiliser cette commande pour créer une instance d’objet, puis, à l’aide des mêmes API que celles fournies par la [bibliothèque JS Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), effectuer le suivi des événements multimédia.

La commande `getMediaAnalyticsTracker` renvoie l’API Media Analytics héritée.

| Nom de la méthode | Description | Syntaxe |
|---|---|---|
| `getInstance` | Crée une instance de média pour effectuer le suivi de la session de lecture. | `Media.getInstance()` |
| `createMediaObject` | Crée un objet contenant des informations sur le média. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | Crée un objet contenant des informations sur l’arrêt. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | Crée un objet contenant des informations publicitaires. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | Crée un objet contenant des informations sur le chapitre. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | Crée un objet contenant des informations sur l’état. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createStateObject(name)` |
| `createQoEObject` | Crée un objet contenant des informations sur la qualité de service. Renvoie un objet vide si des paramètres non valides sont transmis. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## Méthodes d’instance

| Nom de la méthode | Description | Syntaxe |
|---|---|---|
| `trackSessionStart` | Effectuez le suivi de l’intention de démarrer la lecture. Une session de suivi est ainsi lancée sur l’instance de suivi multimédia. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | Effectuez le suivi de la lecture multimédia ou reprenez après une pause précédente. | `trackerInstance.trackPlay()` |
| `trackPause` | Suivi de la pause du média. | `trackerInstance.trackPause()` |
| `trackComplete` | Suivi du média terminé. Appelez cette méthode uniquement lorsque le média a été entièrement visionné. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | Effectuez le suivi de la fin d’une session de visualisation. Appelez cette méthode même si l’utilisateur ne voit pas le média jusqu’à la fin. | `trackerInstance.trackSessionEnd()` |
| `trackError` | Effectue le suivi d’une erreur qui s’est produite lors de la lecture du média. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | Effectuez le suivi d’un événement personnalisé. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | Mettez à jour la position du curseur de lecture. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | Mettez à jour la qualité de l’expérience. | `trackerInstance.updateQoEObject(qoe)` |

## Constantes

| Nom constant | Description | Valeur |
|---|---|---|
| `MediaType` | Type de média | `Video`, `Audio` |
| `StreamType` | Type de flux | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | Cette section définit les clés de métadonnées standard pour les flux vidéo | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed` `StreamFormat` |
| `AudioMetadataKeys` | Cela définit les clés de métadonnées standard pour les flux audio. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | Cela définit les clés de métadonnées standard pour les publicités. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | Définit le type d’un événement de suivi. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart` `StateEnd` |
| `PlayerState` | Cela définit des valeurs standard pour le suivi de l’état du lecteur. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |

## Obtention du dispositif de suivi Media Analytics à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK équivalente à cette commande est l’action [**[!UICONTROL Get Media Analytics tracker]**](/help/tags/extensions/client/web-sdk/actions/get-media-analytics-tracker.md).
