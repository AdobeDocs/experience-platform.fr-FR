---
title: Présentation de lʼextension Adobe Media Analytics (3.x SDK) for Audio and Video
description: Découvrez lʼextension Adobe Media Analytics (SDK 3.x) for Audio and Video dans Adobe Experience Platform.
exl-id: 7289d57d-7e7f-4832-9469-3b5a62183a32
TQID: https://experienceleague.adobe.com/SIfGqM-kdtMyQyfkorCmUzmkaGVSDxZPR9ePnv5IRYI
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 722
ht-degree: 95%

---

# Présentation de lʼextension Adobe Media Analytics (3.x SDK) for Audio and Video

Pour plus d’informations sur l’installation, la configuration et la mise en œuvre de l’extension Adobe Media Analytics (SDK 3.x) for Audio and Video (extension Media Analytics), utilisez cette documentation. Les options disponibles lors de l’utilisation de cette extension pour créer une règle, ainsi que des exemples et des liens vers des exemples, sont inclus.

L’extension Media Analytics (MA) ajoute le SDK principal JavaScript Media (SDK Media 3.x). Cette extension est une fonctionnalité qui permet d’ajouter l’instance `Media` de suivi à un site ou à un projet acceptant les balises. L’extension MA requiert deux extensions supplémentaires :

* [Extension Analytics](../analytics/overview.md)
* [L’extension Experience Cloud ID](../id-service/overview.md)

>[!IMPORTANT]
>
>Cette extension est déployée avec le SDK Media 3.x, qui n’a pas de compatibilité descendante avec le SDK Media 2.x. Puisque la version 2.x a été abandonnée, veuillez mettre à jour vers la version 3.x.

Après avoir inclus les trois extensions mentionnées ci-dessus dans votre projet acceptant les balises, vous pouvez procéder de deux façons :

* Utiliser les API `Media` de votre application web
* Inclure ou créer une extension spécifique au lecteur qui associe des événements de lecteur multimédia spécifiques aux API sur l’instance de suivi `Media`. Cette instance est exposée via l’extension MA.

## Installation et configuration de l’extension MA

* **Installer :** Pour installer l’extension MA, ouvrez la propriété d’extension, cliquez sur **[!UICONTROL Extensions > Catalog]**, survolez l’extension **[!UICONTROL Adobe Media Analytics (3.x SDK) for Audio and Video]** avec votre souris et cliquez sur **[!UICONTROL Install]**.

* **Configurer :** Pour configurer l’extension MA, ouvrez l’onglet [!UICONTROL Extensions], survolez l’extension avec votre souris, puis cliquez sur **[!UICONTROL Configure]** :

![Configuration de l’extension MA](../../../images/ext-ma-config.png)

### Options de configuration :

| Option | Description |
| :--- | :--- |
| Collection API Server | Définit le serveur d’API Media Collection (contactez votre représentant Adobe pour obtenir ce serveur) |
| Application Version | La version de l’application/du SDK du lecteur multimédia |
| Nom du lecteur | Le nom du lecteur multimédia en cours d’utilisation (par exemple, « AVPlayer », « Lecteur HTML5 », « Mon lecteur personnalisé ») |
| Canal | Propriété du nom de canal |
| Debug Logging | Activation ou désactivation de la journalisation |
| Enable SSL | Activation ou désactivation de l’envoi de pings via HTTPS |
| Export APIs to Window Object | Activer ou désactiver l’exportation des API Media Analytics vers la portée globale |
| Variable Name | Une variable utilisée pour exporter les API de Media Analytics sous l’objet `window` |

**Rappel :** l’extension MA requiert les extensions [Analytics](../analytics/overview.md) et [Experience Cloud ID](../id-service/overview.md). Vous devez également ajouter ces extensions à la propriété de votre extension et les configurer.

## Utilisation de l’extension MA

### Utilisation depuis une page web/application JavaScript

L’extension MA exporte les API Media dans l’objet global window en activant le paramètre « Export APIs to Window Object » dans la page [!UICONTROL Configuration]. Il exporte les API sous le nom de variable configuré. Par exemple, si le nom de variable est configuré pour être `ADB`, vous pouvez alors accéder aux API Media via `window.ADB.Media`.

>[!IMPORTANT]
>
>L’extension MA exporte les API uniquement lorsque `window["CONFIGURED_VARIABLE_NAME"]` n’est pas défini et ne remplace pas les variables existantes.

1. **API Media :** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Expose toutes les API et constantes du SDK Media : [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **Créer une instance de suivi Media :** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **Valeur renvoyée :** Une instance de suivi `Media` pour le suivi d’une session de médias.

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. A l’aide de l’instance de suivi Media, suivez la [documentation de l’API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) pour mettre en œuvre le suivi des médias.

Vous pouvez obtenir l’exemple de lecteur ici : [MA Sample Player](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x). Le lecteur d’exemple fait office de référence pour expliquer comment utiliser l’extension MA pour prendre en charge directement Media Analytics à partir d’une application web.


### Utilisation à partir d’autres extensions

L’extension MA expose `media` en tant que module partagé aux autres extensions. (Pour plus d’informations sur les modules partagés, voir la [documentation sur les modules partagés](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Les modules partagés ne sont accessibles que depuis d’autres extensions. En d’autres termes, une page web ou une application JavaScript ne peuvent pas accéder aux modules partagés ni utiliser `turbine` (voir l’exemple de code ci-dessous) en dehors d’une extension.

1. **API Media :** `media` Module partagé

   Expose toutes les API et constantes du SDK Media : [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. Créez l’instance de suivi Media comme suit :

   **Valeur renvoyée :** Une instance de suivi `Media` pour le suivi d’une session de médias.

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. A l’aide de l’instance de suivi Media, suivez la [documentation de l’API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) pour mettre en œuvre le suivi des médias.

>[!NOTE]
>
>**Tests :** pour tester votre extension dans cette version, vous devez télécharger votre extension sur [Experience Platform](../../../extension-dev/submit/upload-and-test.md), où vous avez accès à toutes les extensions dépendantes.
