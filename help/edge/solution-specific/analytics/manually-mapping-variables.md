---
title: Mappage manuel des variables dans Analytics
seo-title: Mappage manuel des variables dans Analytics avec le SDK Web
description: Mappage manuel de variables dans Analytics à l’aide de règles de traitement
seo-description: mapper manuellement des variables dans Analytics à l’aide de règles de traitement avec le SDK Web
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 47%

---


# Mappage manuel des variables dans Analytics

Adobe Experience Platform (AEP) [!DNL Web SDK] peut mapper automatiquement certaines variables, mais les variables personnalisées doivent être mappées manuellement.

For XDM data that is not automatically mapped to [!DNL Analytics], you can use [context data](https://docs.adobe.com/content/help/fr-FR/analytics/implementation/vars/page-vars/contextdata.html) to match your [schema](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/schema/composition.html). Il peut ensuite être mappé en [!DNL Analytics] utilisant des règles [de](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) traitement pour renseigner [!DNL Analytics] des variables.

Also, you can use a default set of actions and product lists to send or retrieve data with the AEP [!DNL Web SDK]. Pour ce faire, consultez [Produits](https://docs.adobe.com/content/help/fr-FR/experience-platform/edge/implement/commerce.html).

## Données contextuelles

To be used by [!DNL Analytics], XDM data is flattened using dot notation and made available as `contextData`. La liste suivante de paires de valeurs présente un exemple de `context data` :

```javascript
{
          "bh": "900",
          "bw": "1680",
          "c": "24",
          "c.a.d.key.[0]": "value1",
          "c.a.d.key.[1]": "value2",
          "c.a.d.object.key1": "value1",
          "c.a.d.object.key2.[0]": "value2",
          "c.a.x.environment.browserdetails.javascriptenabled": "true",
          "c.a.x.environment.type": "browser",
          "cust_hit_time_gmt": "1579781427",
          "g": "http://example.com/home",
          "gn": "home",
          "j": "1.8.5",
          "k": "Y",
          "s": "1680x1050",
          "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
          "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
          "v": "Y"
        }
```

## Règles de traitement

Toutes les données collectées par le réseau Edge sont accessibles via des [règles de traitement](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In [!DNL Analytics], you can use processing rules to incorporate context data into [!DNL Analytics] variables.

Par exemple, dans la règle suivante, Analytics est défini pour renseigner les **termes pour la recherche interne (eVar2)** avec les données associées à **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## Schéma XDM

[!DNL Experience Platform] utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente entre les systèmes, il devient plus facile de conserver une signification et, par conséquent, de tirer profit des données. [!DNL Analytics] les données contextuelles fonctionnent avec la structure définie par le schéma.

The following example shows how the [`event` command](https://docs.adobe.com/content/help/fr-FR/experience-platform/edge/fundamentals/tracking-events.html) can be used with the `xdm` option to send and retrieve data with the AEP [!DNL Web SDK]. Dans cet exemple, la commande `event` correspond au [Schéma de détails du commerce ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md), ce qui permet de suivre le `name` de productListItems et les valeurs `SKU` :


```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

For more information on tracking events with the AEP [!DNL Web SDK], see [Tracking events](https://docs.adobe.com/content/help/fr-FR/experience-platform/edge/fundamentals/tracking-events.html).
