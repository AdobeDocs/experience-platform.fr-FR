---
title: Mappage manuel des variables dans Adobe Analytics
seo-title: Mappage manuel des variables en Adobe Analytics avec le SDK Web
description: Comment mapper manuellement des variables dans Adobe Analytics à l’aide de règles de traitement
seo-description: Mappage manuel de variables dans Adobe Analytics à l’aide de règles de traitement avec le SDK Web
keywords: adobe analytics ; analytics ; variables ; variables de mappage ; variables de mappage ; variables de mappage ; contextData ; données contextuelles ; règles de traitement ; règles ; xdm ; schéma ;
translation-type: tm+mt
source-git-commit: 206b5addd6baf5a120b469b21313ee86ac1fe53b
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 34%

---


# Mappage manuel des variables dans Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] peut mapper automatiquement certaines variables, mais les variables personnalisées doivent être mappées manuellement.

Pour les données XDM qui ne sont pas automatiquement mises en correspondance avec [!DNL Analytics], vous pouvez utiliser [les données contextuelles](https://docs.adobe.com/content/help/fr-FR/analytics/implementation/vars/page-vars/contextdata.html) pour faire correspondre votre [schéma](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/schema/composition.html). Ensuite, il peut être mappé en [!DNL Analytics] à l&#39;aide de [règles de traitement](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) pour renseigner les variables [!DNL Analytics].

En outre, vous pouvez utiliser un ensemble par défaut d’actions et de listes de produits pour envoyer ou récupérer des données avec Adobe Experience Platform Web SDK. Pour ce faire, consultez [Produits](https://docs.adobe.com/content/help/fr-FR/experience-platform/edge/implement/commerce.html).

## Données contextuelles

À utiliser par [!DNL Analytics], les données XDM sont aplaties à l’aide de la notation point et rendues disponibles sous la forme `contextData`. La liste suivante de paires de valeurs présente un exemple de `context data` :

```json
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

Toutes les données collectées par le réseau Edge sont accessibles via des [règles de traitement](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). Dans [!DNL Analytics], vous pouvez utiliser des règles de traitement pour incorporer des données contextuelles dans des variables [!DNL Analytics].

Par exemple, dans la règle suivante, Adobe Analytics est défini pour renseigner les **termes de recherche interne (eVar2)** avec les données associées à **a.x._atag.search.term(Données contextuelles)**.

![](assets/examplerule.png)


## Schéma XDM

Adobe Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente entre les systèmes, il devient plus facile de conserver une signification et, par conséquent, de tirer profit des données. [!DNL Analytics] les données contextuelles fonctionnent avec la structure définie par le schéma.

L&#39;exemple suivant montre comment la commande [`event`](https://docs.adobe.com/content/help/fr-FR/experience-platform/edge/fundamentals/tracking-events.html) peut être utilisée avec l&#39;option `xdm` pour envoyer et récupérer des données avec le SDK Web de Adobe Experience Platform. Dans cet exemple, la commande `event` correspond au [Schéma de détails du commerce ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md), ce qui permet de suivre le `name` de productListItems et les valeurs `SKU` :


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

Pour plus d&#39;informations sur les événements de suivi avec Adobe Experience Platform [!DNL Web SDK], voir [événements de suivi](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
