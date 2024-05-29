---
title: createMediaSession
description: Découvrez comment configurer le SDK Web pour gérer automatiquement les sessions multimédia
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---


# `createMediaSession`

La variable `createMediaSession` fait partie du SDK Web `streamingMedia` composant. Vous pouvez utiliser ce composant pour collecter des données relatives aux sessions multimédia sur votre site web. Voir `streamingMedia` [documentation](configure/streamingmedia.md) pour savoir comment configurer ce composant.

Les données collectées peuvent inclure des informations sur les lectures multimédia, les pauses, les fins et d’autres événements connexes. Une fois collectées, vous pouvez envoyer ces données à [Adobe Analytics pour les médias en streaming](https://experienceleague.adobe.com/fr/docs/media-analytics/using/media-overview), pour agréger des mesures. Cette fonctionnalité offre une solution complète pour effectuer le suivi et comprendre le comportement de consommation des médias sur votre site web.

Vous pouvez créer des sessions multimédia dans le SDK Web de deux manières :

* [Sessions de médias suivies automatiquement](#automatic) permettre au SDK Web de gérer la distribution des événements ping multimédia vers [Adobe Analytics pour les médias en streaming](https://experienceleague.adobe.com/fr/docs/media-analytics/using/media-overview). La fréquence de ces pings est déterminée par les paramètres de configuration de la variable [streamingMedia](configure/streamingmedia.md) composant.
* [Sessions multimédia suivies manuellement](#manual) vous donner plus de contrôle sur l’envoi d’événements ping de session à [Adobe Analytics pour les médias en streaming](https://experienceleague.adobe.com/fr/docs/media-analytics/using/media-overview). De plus, vous pouvez stocker le `sessionID` pour les sessions multimédia.

## Créer une session multimédia automatiquement suivie {#automatic}

Pour lancer automatiquement le suivi d’une session multimédia, appelez la fonction `createMediaSession` avec les options décrites ci-dessous :

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| Propriété | Type | Obligatoire | Description |
|---------|----------|---------|---------|
| `playerId` | Chaîne | Oui | Identifiant du lecteur, un identifiant unique représentant la session multimédia. |
| `getPlayerDetails` | Fonction | Oui | Fonction qui renvoie les détails du lecteur. Cette fonction de rappel sera appelée par le SDK Web avant chaque événement multimédia pour la variable `playerId` fourni. |
| `xdm.eventType ` | Objet | Non | Type d’événement multimédia. Si elle n’est pas fournie, elle est automatiquement définie sur `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objet | Oui | Objet de détails de la session. La variable `sessionDetails` doit contenir les propriétés des détails de la session. Voir [Schéma Media Collection](../../xdm/data-types/media-collection-details.md) pour plus d’informations. |


## Création d’une session multimédia suivie manuellement {#manual}

Pour commencer le suivi manuel d’une session multimédia, appelez la méthode `createMediaSession` avec les options décrites ci-dessous :

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| Propriété | Type | Requis | Description |
|---------|----------|---------|---------|
| `xdm.eventType` | Objet | Non | Type d’événement multimédia. Si elle n’est pas fournie, elle est automatiquement définie sur `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objet | Oui | Objet de détails de la session. La variable `sessionDetails` doit contenir les propriétés des détails de la session. Voir [Schéma Media Collection](../../xdm/data-types/media-collection-details.md) pour plus d’informations. |
| `xdm.mediaCollection.playhead` | Nombre entier | Oui | Curseur de lecture actuel. |
| `xdm.mediaCollection.qoeDataDetails` | Objet | Non | Qualité des détails des données d’expérience. Voir [Schéma Media Collection](../../xdm/data-types/media-collection-details.md) pour plus d’informations. |
