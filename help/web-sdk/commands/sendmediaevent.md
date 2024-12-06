---
title: sendMediaEvent
description: Découvrez comment utiliser la commande sendMediaEvent pour effectuer le suivi des sessions multimédia dans le SDK Web.
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 877e12f1d53bb4a8d7c2564490d4e8f3e9e34e34
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# `sendMediaEvent`

La commande `sendMediaEvent` fait partie du composant SDK Web `streamingMedia`. Vous pouvez utiliser ce composant pour collecter des données relatives aux sessions multimédia sur votre site web. Consultez la `streamingMedia` [documentation](configure/streamingmedia.md) pour savoir comment configurer ce composant.

Utilisez la commande `sendMediaEvent` pour effectuer le suivi des lectures multimédia, des pauses, des compléments, des mises à jour de l’état du lecteur et d’autres événements connexes.

Le SDK Web peut gérer les événements multimédia en fonction du type de suivi de session multimédia :

* **Gestion des événements pour les sessions suivies automatiquement**. Dans ce mode, vous n’avez pas besoin de transmettre `sessionID` à l’événement multimédia ou la valeur du curseur de lecture. Le SDK Web gère cette opération pour vous, en fonction de l’identifiant du lecteur fourni et de la fonction de rappel `getPlayerDetails` fournie lors du démarrage de la session multimédia.
* **Gestion des événements pour les sessions suivies manuellement**. Dans ce mode, vous devez transmettre `sessionID` à l’événement multimédia, ainsi que la valeur du curseur de lecture (valeur entière). Vous pouvez également transmettre les détails de la qualité des données d’expérience, si nécessaire.

## Gestion des événements de média par type {#handle-by-type}

Sélectionnez les onglets ci-dessous pour afficher des exemples de gestion des types d’événement pour chaque type d’événement et chaque méthode de suivi de session (automatique ou manuelle).


### Play {#play}

Le type d’événement `media.play` est utilisé pour effectuer le suivi au démarrage de la lecture multimédia. Cet événement doit être envoyé lorsque le lecteur passe de l’état &quot;lecture&quot; à un autre état. Parmi les autres états à partir desquels le lecteur passe à &quot;lecture&quot;, citons &quot;mise en mémoire tampon&quot;, la reprise de l’utilisateur après &quot;mise en pause&quot;, la reprise du lecteur suite à une erreur ou la lecture automatique.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Pause {#pause}

Le type d’événement `media.pauseStart` est utilisé pour effectuer le suivi de la mise en pause de la lecture multimédia. Cet événement doit être envoyé lorsque l’utilisateur appuie sur **[!UICONTROL Pause]**. Il n’existe aucun type d’événement resume . Une reprise est déduite lorsque vous envoyez un événement `media.play` après un `media.pauseStart`.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Erreur {#error}

Le type d’événement `media.error` est utilisé pour effectuer le suivi d’une erreur survenant pendant la lecture du média. Cet événement doit être envoyé lorsqu’une erreur se produit.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Début de la coupure publicitaire {#ad-break-start}

Le type d’événement `media.adBreakStart` est utilisé pour effectuer le suivi du début d’une coupure publicitaire. Cet événement doit être envoyé au démarrage d’une coupure publicitaire.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Fin de la coupure publicitaire {#ad-break-complete}

Le type d’événement `media.adBreakComplete` est utilisé pour effectuer le suivi de la fin d’une coupure publicitaire. Cet événement doit être envoyé à la fin d’une coupure publicitaire.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Démarrage de publicité {#ad-start}

Le type d’événement `media.adStart` est utilisé pour effectuer le suivi du démarrage d’une publicité. Cet événement doit être envoyé au démarrage d’une publicité.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]


### Fin de publicité {#ad-complete}

Le type d’événement `media.adComplete` est utilisé pour effectuer le suivi à la fin d’une publicité. Cet événement doit être envoyé lorsqu’une publicité se termine.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Ignorer la publicité {#ad-skip}

Le type d’événement `media.adSkip` est utilisé pour effectuer le suivi lorsqu’une publicité est ignorée. Cet événement doit être envoyé lorsqu’une publicité est ignorée.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Début du chapitre {#chapter-start}

Le type d’événement `media.chapterStart` est utilisé pour effectuer le suivi du début d’un chapitre. Cet événement doit être envoyé au début d’un chapitre.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]


### Fin du chapitre {#chapter-complete}

Le type d’événement `media.chapterComplete` est utilisé pour effectuer le suivi de la fin d’un chapitre. Cet événement doit être envoyé lorsqu’un chapitre se termine.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Saut de chapitre {#chapter-skip}

Le type d’événement `media.chapterSkip` est utilisé pour effectuer le suivi lorsqu’un chapitre est ignoré. Cet événement doit être envoyé lorsqu’un chapitre est ignoré.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Début de la mémoire tampon {#buffer-start}

Le type d’événement `media.bufferStart` est utilisé pour effectuer le suivi au démarrage de la mise en mémoire tampon. Cet événement doit être envoyé au démarrage de la mise en mémoire tampon. Il n’existe pas de type d’événement `bufferResume`. Un `bufferResume` est déduit lorsque vous envoyez un événement de lecture après `bufferStart`.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Changement de débit binaire {#bitrate-change}

Le type d’événement `media.bitrateChange` est utilisé pour effectuer le suivi des changements de débit binaire. Cet événement doit être envoyé lorsque le débit binaire change.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Mises à jour d’état {#state-updates}

Le type d’événement `media.statesUpdate` est utilisé pour effectuer le suivi des modifications de l’état du lecteur. Cet événement doit être envoyé lorsque l’état du lecteur change.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.statesUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]


### Fin de session {#session-end}

Le type d’événement `media.sessionEnd` est utilisé pour informer le serveur principal Media Analytics de fermer immédiatement la session lorsque l’utilisateur a abandonné l’affichage du contenu et qu’il est peu probable qu’il y rende.

Si vous n’envoyez pas d’événement `sessionEnd`, une session abandonnée expirera après qu’aucun événement n’a été reçu pendant 10 minutes, ou lorsqu’aucun mouvement du curseur de lecture ne se produit pendant 30 minutes. La session est automatiquement supprimée.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Fin de la session {#session-complete}

Le type d’événement `media.sessionComplete` est utilisé pour effectuer le suivi à la fin d’une session multimédia. Cet événement doit être envoyé lorsque la fin du contenu principal est atteinte.

>[!BEGINTABS]

>[!TAB Suivi automatique de session]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB Suivi manuel de session]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]
