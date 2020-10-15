---
title: Rendu du contenu personnalisé
seo-title: Rendu du contenu personnalisé avec le SDK Web d’Adobe Experience Platform
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web d’Experience Platform
seo-description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web d’Experience Platform
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 23%

---


# Présentation des options de personnalisation

Le Adobe Experience Platform [!DNL Web SDK] prend en charge l’interrogation des solutions de personnalisation à l’Adobe, y compris Adobe Target. Il existe deux modes de personnalisation : récupération du contenu qui peut être rendu automatiquement et du contenu que le développeur doit rendre. Le SDK fournit également des fonctionnalités de [gestion du scintillement](../personalization/manage-flicker.md).

## Rendu automatique du contenu

Le SDK effectue automatiquement le rendu du contenu personnalisé lorsque vous envoyez un événement au serveur et que vous définissez `renderDecisions` sur `true` comme option sur l’événement.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Le rendu du contenu personnalisé est asynchrone. Il ne doit donc pas y avoir d’hypothèse sur le moment où un élément de contenu particulier fait partie de la page.

## Rendu manuel du contenu

Vous pouvez demander la liste des décisions à renvoyer en tant que promesse sur la `sendEvent` commande en spécifiant l&#39; `decisionScopes` option. Une portée est une chaîne qui permet à la solution de personnalisation de savoir quelle décision vous souhaitez prendre.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  })
```

Cela renverra une liste de décisions en tant qu’objet JSON pour chaque décision.

```javascript
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

>[!TIP]
>
> Si vous utilisez [!DNL Target], les étendues deviennent des mBoxes sur le serveur, mais elles sont toutes demandées à la fois et non pas individuellement. La mbox globale est toujours envoyée.

### Récupérer le contenu automatique

Si vous souhaitez que les décisions `result.decisions` de rendu automatique soient incluses et que l’option NOT have Alloy les génère automatiquement, vous pouvez définir `renderDecisions` sur `false`et inclure la portée spéciale `__view__`.
