---
title: createMediaSession
description: Découvrez comment configurer le SDK Web pour gérer automatiquement les sessions multimédia
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---

# `createMediaSession`

La commande `createMediaSession` fait partie du composant SDK Web `streamingMedia`. Vous pouvez utiliser ce composant pour collecter des données relatives aux sessions multimédia sur votre site web. Consultez la `streamingMedia` [documentation](configure/streamingmedia.md) pour savoir comment configurer ce composant.

Les données collectées peuvent inclure des informations sur les lectures multimédia, les pauses, les fins et d’autres événements connexes. Une fois ces données collectées, vous pouvez les envoyer à [Adobe Analytics pour les médias en streaming](https://experienceleague.adobe.com/fr/docs/media-analytics/using/media-overview) pour agréger les mesures. Cette fonctionnalité offre une solution complète pour effectuer le suivi et comprendre le comportement de consommation des médias sur votre site web.

Vous pouvez créer des sessions multimédia dans le SDK Web de deux manières :

* [&#x200B; Les sessions multimédia suivies automatiquement](#automatic) permettent au SDK Web de gérer la distribution des événements ping multimédia sur [Adobe Analytics pour les médias en streaming](https://experienceleague.adobe.com/fr/docs/media-analytics/using/media-overview). La fréquence de ces pings est déterminée par les paramètres de configuration du composant [streamingMedia](configure/streamingmedia.md).
* [Les sessions multimédias suivies manuellement](#manual) vous permettent de mieux contrôler la distribution des événements ping de session sur [Adobe Analytics pour les médias en streaming](https://experienceleague.adobe.com/fr/docs/media-analytics/using/media-overview). De plus, vous avez la possibilité de stocker le `sessionID` pour les sessions multimédia.

## Créer une session multimédia automatiquement suivie {#automatic}

Pour lancer automatiquement le suivi d’une session multimédia, appelez la méthode `createMediaSession` avec les options décrites ci-dessous :

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
| `getPlayerDetails` | Fonction | Oui | Fonction qui renvoie les détails du lecteur. Cette fonction de rappel sera appelée par le SDK Web avant chaque événement multimédia pour le `playerId` fourni. |
| `xdm.eventType ` | Objet | Non | Type d’événement multimédia. Si elle n’est pas fournie, elle est automatiquement définie sur `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objet | Oui | Objet de détails de la session. L’objet `sessionDetails` doit contenir les propriétés des détails de session. Pour plus d’informations, consultez la documentation [Schéma Media Collection](../../xdm/data-types/media-collection-details.md) . |


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
| `xdm.mediaCollection.sessionDetails` | Objet | Oui | Objet de détails de la session. L’objet `sessionDetails` doit contenir les propriétés des détails de session. Pour plus d’informations, consultez la documentation [Schéma Media Collection](../../xdm/data-types/media-collection-details.md) . |
| `xdm.mediaCollection.playhead` | Nombre entier | Oui | Curseur de lecture actuel. |
| `xdm.mediaCollection.qoeDataDetails` | Objet | Non | Qualité des détails des données d’expérience. Pour plus d’informations, consultez la documentation [Schéma Media Collection](../../xdm/data-types/media-collection-details.md) . |
