---
title: data
description: Découvrez comment envoyer des données non-XDM à Adobe, par le biais de l’objet de données.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# `data`

L’objet `data` vous permet d’envoyer à Adobe une payload qui ne correspond pas à un schéma XDM. Elle est utile dans les scénarios non XDM, comme l’envoi direct de données à Adobe Analytics, Adobe Target ou Adobe Audience Manager. Lorsque les données arrivent dans le flux de données, vous pouvez utiliser le [mappage de la préparation des données](/help/data-prep/ui/mapping.md) pour affecter des champs XDM à chaque champ de l’objet `data`. Si un produit est déjà configuré par Adobe pour détecter des champs dans l’objet `data`, vous pouvez envoyer ces données en l’état à un flux de données.

>[!IMPORTANT]
>
>Les données de cet objet doivent avoir au moins l’une des actions suivantes :
>
>* Un service dans le flux de données doit être configuré pour récupérer les données d’une propriété donnée dans l’objet `data`.
>* La propriété donnée doit être mappée à un champ XDM à l’aide de la préparation des données.
>
>Si une propriété donnée n’est pas mappée à un champ XDM ou utilisée par un service configuré, ces données sont définitivement perdues.

Définissez l’objet `data` dans le cadre de l’objet JSON dans le paramètre de la commande `sendEvent`. Pour les données que vous prévoyez de mapper dans le flux de données, vous pouvez structurer cet objet comme vous le souhaitez. Pour les données utilisées par certains services, assurez-vous que la hiérarchie d’objets correspond à ce que le service attend. Vous pouvez inclure l’objet `data` et l’objet [`xdm`](xdm.md) dans la même commande `sendEvent`.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Utiliser l’objet `data` avec Adobe Analytics {#analytics}

Vous pouvez utiliser l’objet `data` avec Adobe Analytics pour envoyer des données à une suite de rapports sans schéma XDM. Les variables sont configurées pour utiliser la même syntaxe que les variables AppMeasurement, ce qui simplifie le processus de mise à niveau vers le SDK Web. Voir [&#x200B; Mappage des variables d’objet de données à Adobe Analytics](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/data-var-mapping) dans le guide de mise en œuvre d’Adobe Analytics pour plus d’informations.

## Utiliser l’objet `data` à l’aide de l’extension de balise Web SDK

L’objet `data` est disponible en tant qu’élément de données [Variable](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) lors de l’utilisation de l’extension de balise Web SDK.
