---
title: Envoi de données à Adobe Analytics à l’aide du SDK Web
description: Découvrez comment envoyer des données à Adobe Analytics avec le SDK Web de Adobe Experience Platform.
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Envoi de données à Adobe Analytics à l’aide du SDK Web

Le SDK Web Experience Platform peut envoyer des données à Adobe Analytics par l’intermédiaire de l’Edge Network Experience Platform. Adobe propose plusieurs options pour envoyer des données à Adobe Analytics à l’aide du SDK Web :

* Ajoutez le [**[!UICONTROL groupe de champs Adobe Analytics ExperienceEvent]**](../../xdm/field-groups/event/analytics-full-extension.md) à votre schéma, puis utilisez l’objet [`XDM`](../commands/sendevent/xdm.md).
* Utilisez l’ [`data` objet](../commands/sendevent/data.md) pour envoyer des données à Adobe Analytics sans schéma XDM.
* Utilisez les [variables de données contextuelles](https://experienceleague.adobe.com/fr/docs/analytics/implementation/vars/page-vars/contextdata) et les [règles de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) générées automatiquement.

## Utilisation de l’objet `XDM` {#use-xdm-object}

Si vous souhaitez utiliser un schéma prédéfini spécifique à Adobe Analytics, vous pouvez ajouter le [groupe de champs de schéma Adobe Analytics ExperienceEvent](../../xdm/field-groups/event/analytics-full-extension.md) à votre schéma. Une fois ajouté, vous pouvez renseigner ce schéma à l’aide de l’objet `xdm` dans le SDK Web pour envoyer des données à une suite de rapports. Lorsque des données arrivent à l’Edge Network, elles convertissent l’objet XDM dans un format qu’Adobe Analytics comprend.

Vous pouvez envoyer des données à Adobe Analytics par le biais du SDK Web de deux façons :

* [Envoi de données à Adobe Analytics à l’aide de l’extension de balise SDK Web](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [Envoi de données à Adobe Analytics à l’aide de la bibliothèque JavaScript SDK Web](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

Voir [Mappage des variables d’objet XDM vers Adobe Analytics](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/xdm-var-mapping) dans le guide de mise en oeuvre d’Adobe Analytics pour obtenir une référence complète des champs XDM et la manière dont ils sont associés aux variables Analytics.

## Utilisation de l’objet `data` {#use-data-object}

Au lieu d’utiliser l’objet XDM, vous pouvez utiliser l’objet de données à la place. L’objet de données est axé sur les implémentations qui utilisent actuellement AppMeasurement, ce qui facilite la mise à niveau vers le SDK Web.

Selon que vous utilisez AppMeasurement ou l’extension de balise Analytics, consultez les guides suivants pour plus d’informations sur la migration vers le SDK Web :

* [Migration de l’extension de balise Adobe Analytics vers l’extension de balise SDK Web](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [Migration de l’AppMeasurement vers le SDK Web](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

Pour obtenir une référence complète des champs d’objet de données et leur mappage aux variables Analytics, reportez-vous à la documentation sur le [mappage de variable d’objet de données à Adobe Analytics](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/data-var-mapping) dans le guide de mise en oeuvre d’Adobe Analytics.

## Utilisation de variables de données contextuelles {#use-context-data-variables}

Toutes les variables qui ne sont pas automatiquement mappées sont disponibles en tant que [variables de données contextuelles](https://experienceleague.adobe.com/fr/docs/analytics/implementation/vars/page-vars/contextdata). Vous pouvez ensuite utiliser des [règles de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) pour mapper des variables de données contextuelles à des variables Analytics. Par exemple, si vous aviez un schéma XDM personnalisé qui ressemblait à ce qui suit :

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

Ces champs seront alors les clés de données contextuelles disponibles dans l’interface Règles de traitement :

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## FAQ

+++Comment différencier les appels de pages vues des appels de suivi de liens dans le SDK Web ?

AppMeasurement dans Adobe Analytics utilise des appels de méthode distincts pour les pages vues ([`t()` method](https://experienceleague.adobe.com/fr/docs/analytics/implementation/vars/functions/t-method)) et les appels de suivi des liens ([`tl()` method](https://experienceleague.adobe.com/fr/docs/analytics/implementation/vars/functions/tl-method)). Le SDK Web fournit uniquement la commande [`sendEvent`](../commands/sendevent/overview.md) pour envoyer les pages vues et le suivi des liens. Les données que vous incluez dans un événement déterminent s’il s’agit d’une [page vue](https://experienceleague.adobe.com/fr/docs/analytics/components/metrics/page-views) ou d’un [événement de page](https://experienceleague.adobe.com/fr/docs/analytics/components/metrics/page-events) dans Adobe Analytics.

Par défaut, tous les événements sont considérés comme des pages vues dans Adobe Analytics. Si vous souhaitez définir un événement SDK Web sur un appel de suivi des liens Adobe Analytics, définissez les champs suivants :

* **Objet XDM** : `xdm.web.webInteraction.name`, `web.webInteraction.type` et `web.webInteraction.URL`
* **Objet de données** : `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType` et `data.__adobe.analytics.linkURL`
* **Données contextuelles** : non prises en charge

Pour plus d’informations, voir la méthode [`tl()`](https://experienceleague.adobe.com/fr/docs/analytics/implementation/vars/functions/tl-method) dans le guide de mise en oeuvre d’Adobe Analytics.

Si vous activez [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) dans la commande `configure`, ces champs sont renseignés pour vous.

+++

+++Comment un flux de données différencie-t-il les données d’autres services des données destinées à Adobe Analytics ?

Tous les événements envoyés à un flux de données sont transmis à tous les services configurés. Par exemple, si vous effectuez des appels distincts pour la personnalisation et Analytics, les deux événements sont envoyés à Analytics et Target. Ces événements sont enregistrés dans les rapports Analytics et peuvent affecter des mesures telles que le taux de rebond.

Si vous utilisez le SDK Web, ces appels sont généralement combinés dans la commande [`sendEvent`](../commands/sendevent/overview.md).

+++
