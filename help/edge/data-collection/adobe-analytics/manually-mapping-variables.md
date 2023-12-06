---
title: Mappage manuel des variables Adobe Analytics dans le SDK Web de Adobe Experience Platform
description: Découvrez comment mapper manuellement des variables dans Adobe Analytics à l’aide de règles de traitement dans le SDK Web Experience Platform.
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;analytics;variables;variables de mappage;variables map;contextData;données contextuelles;règles de traitement;règles;xdm;schéma;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 12%

---

# Mappage manuel des variables dans Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] peut mapper certaines variables automatiquement, mais les variables personnalisées doivent être mappées manuellement.

Pour les données XDM qui ne sont pas automatiquement mappées à [!DNL Analytics], vous pouvez utiliser [données contextuelles](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=fr) pour correspondre à votre [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr). Ensuite, il peut être mappé dans [!DNL Analytics] using [règles de traitement](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=fr) pour renseigner [!DNL Analytics] .

Vous pouvez également utiliser un ensemble d’actions et de listes de produits par défaut pour envoyer ou récupérer des données avec le SDK Web de Adobe Experience Platform. Pour ce faire, voir [Collecte d’informations sur le commerce et les produits](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## Données contextuelles

À utiliser par [!DNL Analytics], les données XDM sont aplaties à l’aide de la notation par points et mises à disposition sous la forme `contextData`. La liste suivante de paires de valeurs présente un exemple de ce que la variable `context data` ressemble à ce qui suit lorsqu’il est aplati :

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

Toutes les données collectées par le réseau Edge sont accessibles via des [règles de traitement](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=fr). Dans [!DNL Analytics], vous pouvez utiliser des règles de traitement pour incorporer des données contextuelles dans [!DNL Analytics] .

Par exemple, dans la règle suivante, Adobe Analytics est défini pour renseigner **Termes de recherche interne (eVar2)** avec les données associées à **a.x._atag.search.term(Context Data)**.

![Image de l’interface utilisateur d’Analytics montrant un exemple de règle.](assets/examplerule.png)

## Schéma XDM

Adobe Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il devient plus facile de conserver un sens et, par conséquent, d’en tirer profit. [!DNL Analytics] les données contextuelles fonctionnent avec la structure définie par le schéma.

L’exemple suivant illustre la manière dont la variable [`event` command](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=fr) peut être utilisé avec la variable `xdm` pour envoyer et récupérer des données avec le SDK Web de Adobe Experience Platform. Dans cet exemple, la commande `event` correspond au [Schéma de détails du commerce ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md), ce qui permet de suivre le `name` de productListItems et les valeurs `SKU` :


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

Pour plus d’informations sur le suivi des événements avec Adobe Experience Platform [!DNL Web SDK], voir [Suivi des événements](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=fr).
