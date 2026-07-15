---
title: Présentation de l’extension Adobe Media Analytics for Audio and Video
description: Découvrez lʼextension de balise Adobe Media Analytics for Audio and Video dans Adobe Experience Platform.
exl-id: 426cfd08-aead-4b35-824c-45494bca2fc8
TQID: https://experienceleague.adobe.com/%2D%2D%2DWEKSFg9Xfi-wK7GHjdHcsM9AyGlv9Q7N6URjrlN0
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c069c44e-5426-4c1a-accc-8028662f2fde
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: df312454-73c4-43f6-a90e-18f5043f074c
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 84a6bfe05e26b606b772867be54dc0f63e82fde8
workflow-type: tm+mt
source-wordcount: 970
ht-degree: 87%

---

# Présentation de l’extension Adobe Media Analytics for Audio and Video

Pour plus d’informations sur l’installation, la configuration et la mise en œuvre de l’extension Adobe Media Analytics for Audio and Video (extension Media Analytics), utilisez cette documentation. Les options disponibles lors de l’utilisation de cette extension pour créer une règle, ainsi que des exemples et des liens vers des exemples, sont inclus.

L’extension Media Analytics (MA) ajoute le SDK principal JavaScript Media (SDK Media 2.x). Cette extension permet dʼajouter lʼinstance de suivi `MediaHeartbeat` à un site de balise ou à un projet. L’extension MA requiert deux extensions supplémentaires :

* [Extension Analytics](../analytics/overview.md)
* [L’extension Experience Cloud ID](../id-service/overview.md)

>[!IMPORTANT]
>
>Le suivi audio requiert l’extension Analytics version 1.6 ou ultérieure.

Après avoir inclus les trois extensions mentionnées ci-dessus dans votre projet de balise, vous pouvez procéder de deux façons :

* Utiliser les API `MediaHeartbeat` de votre application web
* Inclure ou créer une extension spécifique au lecteur qui associe des événements de lecteur multimédia spécifiques aux API sur l’instance de suivi `MediaHeartbeat`. Cette instance est exposée via l’extension MA.

## Installation et configuration de l’extension MA

* **Installation -** Pour installer l’extension MA, ouvrez la propriété de votre extension, puis sélectionnez **[!UICONTROL Extensions > Catalogue]** et placez le curseur sur l’extension **[!UICONTROL Adobe Media Analytics for Audio and Video]** et sélectionnez **[!UICONTROL Installer]**.

* **Configurer -** Pour configurer l’extension MA, ouvrez l’onglet [!UICONTROL Extensions], placez le curseur sur l’extension, puis cliquez sur **[!UICONTROL Configurer]** :

![Configuration de l’extension MA](../../../images/ext-va-config.jpg)

### Options de configuration :

| Option | Description |
| :--- | :--- |
| Serveur de suivi | Définit le serveur pour le suivi des pulsations multimédia (il ne s’agit pas du même serveur que votre serveur de suivi Analytics) |
| Application Version | La version de l’application/du SDK du lecteur multimédia |
| Nom du lecteur | Le nom du lecteur multimédia en cours d’utilisation (par exemple, « AVPlayer », « Lecteur HTML5 », « Mon lecteur personnalisé ») |
| Canal | Propriété du nom de canal |
| Online Video Provider | Nom de la plateforme vidéo en ligne sur laquelle le contenu est distribué |
| Debug Logging | Activation ou désactivation de la journalisation |
| Enable SSL | Activation ou désactivation de l’envoi de pings via HTTPS |
| Export APIs to Window Object | Activer ou désactiver l’exportation des API Media Analytics vers la portée globale |
| Variable Name | Une variable utilisée pour exporter les API de Media Analytics sous l’objet `window` |

**Rappel :** l’extension MA requiert les extensions [Analytics](../analytics/overview.md) et [Experience Cloud ID](../id-service/overview.md). Vous devez également ajouter ces extensions à la propriété de votre extension et les configurer.

## Utilisation de l’extension MA

### Utilisation depuis une page web/application JavaScript

L’extension MA exporte les API MediaHeartbeat dans l’objet fenêtre global en activant le paramètre « Exporter les API vers l’objet fenêtre » de la page [!UICONTROL Configuration]. Il exporte les API sous le nom de variable configuré. Par exemple, si le nom de variable est configuré pour être `ADB`, vous pouvez alors accéder à MediaHeartbeat via `window.ADB.MediaHeartbeat`.

>[!IMPORTANT]
>
>L’extension MA exporte les API uniquement lorsque `window["CONFIGURED_VARIABLE_NAME"]` n’est pas défini et ne remplace pas les variables existantes.

1. **Créer une instance MediaHeartbeat** : `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

   **Paramètres** : un objet délégué valide exposant ces fonctions.

   | Méthode |  Description   |
   | :--- | :--- |
   | `getQoSObject()` | Retourne l’instance `theMediaObject` contenant les informations actuelles sur la qualité de service QoS. Cette méthode est appelée à plusieurs reprises au cours d’une session de lecture. La mise en œuvre du lecteur doit toujours retourner les plus récentes données QoS disponibles. |
   | `getCurrentPlaybackTime()` | Renvoie la position actuelle du curseur de lecture. Pour le suivi VOD, la valeur est indiquée en secondes à partir du début de l’élément média. Pour le suivi LIVE/LIVE, la valeur est indiquée en secondes à partir du début du programme. |

   **Valeur renvoyée** : une promesse qui est résolue avec une instance `MediaHeartbeat` ou rejetée avec un message d’erreur.

1. **Accéder aux constantes MediaHeartbeat :** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat`

   Cette opération expose toutes les constantes et les méthodes statiques de la classe [`MediaHeartbeat`](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

   Vous pouvez obtenir l’exemple de lecteur ici : [MA Sample Player](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/2.x). Le lecteur d’exemple fait office de référence pour expliquer comment utiliser l’extension MA pour prendre en charge directement Media Analytics à partir d’une application web.

1. Créez l’instance de suivi MediaHeartbeat comme suit :

   ```javascript
   var MediaHeartbeat = window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat;
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   };
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   };
   
   var self = this;
   MediaHeartbeat.getInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   ```

### Utilisation à partir d’autres extensions

L’extension MA expose les modules partagés `get-instance` et `media-heartbeat` à d’autres extensions. (Pour plus d’informations sur les modules partagés, voir la [documentation sur les modules partagés](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Les modules partagés ne sont accessibles que depuis d’autres extensions. En d’autres termes, une page web ou une application JavaScript ne peuvent pas accéder aux modules partagés ni utiliser `turbine` (voir l’exemple de code ci-dessous) en dehors d’une extension.

1. **Créer une instance MediaHeartbeat** `get-instance` : module partagé

   **Paramètres** :

   * Un objet délégué valide exposant ces fonctions :

     | Méthode |  Description   |
     | :--- | :--- |
     | `getQoSObject()` | Retourne l’instance `MediaObject` contenant les informations actuelles sur la qualité de service QoS. Cette méthode est appelée à plusieurs reprises au cours d’une session de lecture. La mise en œuvre du lecteur doit toujours retourner les plus récentes données QoS disponibles. |
     | `getCurrentPlaybackTime()` | Renvoie la position actuelle du curseur de lecture. Pour le suivi VOD, la valeur est indiquée en secondes à partir du début de l’élément média. Pour le suivi LIVE/LIVE, la valeur est indiquée en secondes à partir du début du programme. |

   * Un objet de configuration facultatif exposant ces propriétés :

     | Propriété | Description | Obligatoire |
     | :--- | :--- | :--- |
     | Online Video Provider | Nom de la plateforme vidéo en ligne sur laquelle le contenu est distribué. | Non. Le cas échéant, remplace la valeur définie pendant la configuration de l’extension. |
     | Nom du lecteur | Le nom du lecteur multimédia en cours d’utilisation (par exemple, « AVPlayer », « Lecteur HTML5 », « Mon lecteur personnalisé ») | Non. Le cas échéant, remplace la valeur définie pendant la configuration de l’extension. |
     | Canal | Propriété du nom de canal | Non. Le cas échéant, remplace la valeur définie pendant la configuration de l’extension. |

   **Valeur renvoyée** : une promesse qui est résolue avec une instance `MediaHeartbeat` ou rejetée avec un message d’erreur.

1. **Accéder aux constantes MediaHeartbeat** `media-heartbeat` : module partagé

   Ce module expose toutes les constantes et les méthodes statiques de cette classe : [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

1. Créez l’instance de suivi MediaHeartbeat comme suit :

   ```javascript
   var getMediaHeartbeatInstance =
     turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   
   var MediaHeartbeat =
     turbine.getSharedModule('adobe-video-analytics', 'media-heartbeat');
     ...
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   }
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   }
   ...
   
   var self = this;
   getMediaHeartbeatInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       ...
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   
   ...
   ```

1. À l’aide de l’instance Pulsations multimédia, consultez la [documentation JS du SDK multimédia](https://experienceleague.adobe.com/docs/media-analytics/using/legacy-implementations/legacy-media-sdks/setup-javascript/set-up-js-2.html) et la [documentation de l’API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html) pour mettre en œuvre le suivi multimédia.

>[!NOTE]
>
>**Tests :** pour tester votre extension dans cette version, vous devez télécharger votre extension sur [Experience Platform](../../../extension-dev/submit/upload-and-test.md), où vous avez accès à toutes les extensions dépendantes.


<!--
## Leveraging the sample HTML5 player

You can obtain the MA extension sample HTML5 player here: [HTML5 Sample Player](https://github.com/adobe/reactor-adobe-va-sample-player). The sample player acts as a reference to create video player extensions and to showcase using the MA extension to support media tracking.

### Sample player extension action types

This section describes the action types available in the Sample Player extension.

#### Open Video

The _Open Video_ action provides various configurations for creating and customizing an HTML5 player, providing a video to play and enabling/disabling Adobe Video Analytics tracking.

**Action Configuration / Player Settings:** Note the CSS Selector setting which specifics the `<div>` in the web page where the player is added. Note also that the _Enable Adobe Analytics_ checkbox is checked in the Analytics Settings pane.

![Player Extension Action Configuration](../../../images/ext-va-sp-action.png)

![Player Extension Action Configuration](../../../images/ext-va-sp-action1.png)

* [\[...\]/openVideo/openVideo.jsx](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/view/actions/openVideo/openVideo.jsx) -

  UI Code to configure the Action is defined here.

* [\[...\]/actions/openVideo.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/actions/openVideo.js) - This file exports a function that gets executed when the Action is triggered as part of the tag rule.

  This is a code snippet from `openVideo.js` where the `openVideo` Action is executed:

  ```javascript
    function openVideo(settings) {
        let player;
        try {
            Logger.info(LOG_TAG, `Executing action with ${JSON.stringify(settings)}`);

            player = new PlayerFacade(settings);
            PlayerStore.registerPlayer(player);
            player.load(settings.media);
        } catch (ex) {
            Logger.error(LOG_TAG, `Creating player for action openVideo failed with error ${ex.message}`);

            // Cleanup from DOM.
            if (player) {
                player.destroy();
            }
        }
    }
    ...
  ```

* [\[...\]/analytics/adobeAnalyticsProvider.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/helpers/analytics/adobeAnalyticsProvider.js) - This file implements Video Analytics tracking by using Shared Modules exposed by the VA extension.

### Sample player extension basic deployment

Once the Sample Player extension is installed, you'll need to create at least one rule to properly deploy it. The Image below shows a sample rule that opens the specified video when the core extension fires the `DOMLoaded` event.

![Player Extension Sample Rule](../../../images/ext-va-sp-rule.png)

After you have saved this rule, you will need to add it to a Library, and then build and deploy so that you can test the behavior.

-->
