---
title: createMediaSession
description: Découvrez comment configurer Web SDK pour gérer automatiquement les sessions multimédia
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
TQID: https://experienceleague.adobe.com/7wV5TUFeB8GgK40MenSnKr4QAN-HZJPVihQxuSH2Y0Q
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 390
ht-degree: 12%

---

# `createMediaSession`

La commande `createMediaSession` fait partie du composant `streamingMedia` de Web SDK. Vous pouvez utiliser ce composant pour collecter des données relatives aux sessions multimédia sur votre site web. Voir la `streamingMedia` [documentation](configure/streamingmedia.md) pour savoir comment configurer ce composant.

Les données collectées peuvent inclure des informations sur les lectures de médias, les pauses, les terminaisons et d’autres événements associés. Une fois collectées, vous pouvez envoyer ces données à [Adobe Analytics for Streaming Media](https://experienceleague.adobe.com/fr/docs/media-analytics/using/media-overview), afin d’agréger les mesures. Cette fonctionnalité fournit une solution complète pour suivre et comprendre le comportement de consommation des médias sur votre site web.

Vous pouvez créer des sessions multimédia dans Web SDK de deux manières :

* **Les sessions multimédias suivies automatiquement** permettent au SDK Web de gérer l’envoi d’événements ping multimédia à [Adobe Analytics for Streaming Media](https://experienceleague.adobe.com/fr/docs/media-analytics/using/media-overview). La fréquence de ces pings est déterminée par les paramètres de configuration du composant [streamingMedia](configure/streamingmedia.md).
* **Sessions multimédias suivies manuellement** vous permet de mieux contrôler l’envoi des événements ping de session à [Adobe Analytics for Streaming Media](https://experienceleague.adobe.com/fr/docs/media-analytics/using/media-overview). De plus, vous avez la possibilité de stocker le `sessionID` pour les sessions multimédia.

## Création d’une session multimédia suivie automatiquement {#automatic}

Pour démarrer le suivi automatique d’une session multimédia, appelez la méthode `createMediaSession` avec les options décrites ci-dessous :

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
| `playerId` | Chaîne | Oui | L’identifiant du lecteur, un identifiant unique représentant la session multimédia. |
| `getPlayerDetails` | Fonction | Oui | Une fonction qui renvoie les détails du lecteur. Cette fonction de rappel sera appelée par le SDK Web avant chaque événement multimédia pour le `playerId` fourni. |
| `xdm.eventType` | Objet | Non | Type d’événement multimédia. S’il n’est pas fourni, ce champ est automatiquement défini sur `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objet | Oui | Contient les propriétés des détails de la session. Voir [Schéma Media Collection](/help/xdm/data-types/media-collection-details.md) pour plus d’informations. |

## Création d’une session multimédia suivie manuellement {#manual}

Pour démarrer le suivi manuel d’une session multimédia, appelez la méthode `createMediaSession` avec les options décrites ci-dessous :

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
| `xdm.mediaCollection.sessionDetails` | Objet | Oui | Contient les propriétés des détails de la session. Voir [Schéma Media Collection](/help/xdm/data-types/media-collection-details.md) pour plus d’informations. |
| `xdm.mediaCollection.playhead` | Entier | Oui | Curseur de lecture actuel. |
| `xdm.mediaCollection.qoeDataDetails` | Objet | Non | Détails sur la qualité des données d’expérience. Pour plus d’informations, consultez la documentation [Schéma de collecte de médias](/help/xdm/data-types/media-collection-details.md) . |

## Création d’une session multimédia à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK équivalente à cette commande est le type d’événement [**[!UICONTROL Session start]**](/help/tags/extensions/client/web-sdk/actions/send-media-event.md#session-start) dans l’action « [!UICONTROL Send media event] ».
