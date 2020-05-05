---
title: Rendu du contenu personnalisé
seo-title: Rendu du contenu personnalisé avec le SDK Web d’Adobe Experience Platform
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web d’Experience Platform
seo-description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web d’Experience Platform
translation-type: tm+mt
source-git-commit: bb3841da8a566105fde1b7ac78dccd79a7ea15d4

---


# (bêta) Présentation des options de personnalisation

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Le SDK Web d’Adobe Experience Platform prend en charge l’interrogation des solutions de personnalisation chez Adobe, y compris Adobe Cible. Il existe deux modes de personnalisation : récupération du contenu qui peut être rendu automatiquement et du contenu que le développeur doit rendre. Le SDK fournit également des fonctionnalités de [gestion du scintillement](managing-flicker.md).

## Rendu automatique du contenu

Le SDK effectue automatiquement le rendu du contenu personnalisé lorsque vous envoyez un événement au serveur et que vous définissez `renderDecisions` sur `true` comme option sur l’événement.

```javascript
alloy("event", {
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

Vous pouvez demander la liste des décisions à renvoyer comme promesse sur la `event` commande en utilisant `scopes`. Une portée est une chaîne qui permet à la solution de personnalisation de savoir quelle décision vous souhaitez prendre.

```javascript
alloy("event",{
    xdm:{...},
    scopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      //do something with the decisions
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

{info}Si vous utilisez des étendues de Cible pour créer des mBoxes sur le serveur, seules les requêtes sont traitées en une seule fois et non individuellement. La mbox globale est toujours envoyée.
{info}

### Récupérer le contenu automatique

Si vous souhaitez inclure les décisions de rendu automatique, vous pouvez définir `result.decisions` `renderDecisions` la valeur false et inclure la plage spéciale `__view__`
