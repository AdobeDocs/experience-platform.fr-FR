---
title: Mappage manuel des variables dans Analytics
seo-title: Mappage manuel des variables en Analytics avec le SDK Web
description: Comment mapper manuellement des variables en Analytics à l’aide de règles de traitement
seo-description: mapper manuellement des variables en Analytics à l’aide de règles de traitement avec le SDK Web
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 20%

---


# Mappage manuel des variables dans Analytics

L’Adobe Experience Platform (AEP) [!DNL Web SDK] peut mapper automatiquement certaines variables, mais les variables personnalisées doivent être mappées manuellement.

Pour les données XDM qui ne sont pas automatiquement mises en correspondance avec [!DNL Analytics], vous pouvez utiliser des données [](https://docs.adobe.com/content/help/fr-FR/analytics/implementation/vars/page-vars/contextdata.html) contextuelles pour faire correspondre votre [schéma](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/schema/composition.html). Il peut ensuite être mappé en [!DNL Analytics] utilisant des règles [de](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) traitement pour renseigner [!DNL Analytics] des variables.

Vous pouvez également utiliser un ensemble par défaut d’actions et de listes de produits pour envoyer ou récupérer des données avec l’AEP [!DNL Web SDK]. Pour ce faire, voir [Produits](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html).

## Données contextuelles

Pour être utilisée par [!DNL Analytics], les données XDM sont aplaties à l’aide de la notation point et rendues disponibles sous `contextData`forme. La liste suivante de paires valeur présente un exemple de `context data`:

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

All data collected by the edge network can be accessed via [processing rules](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). Dans [!DNL Analytics], vous pouvez utiliser des règles de traitement pour incorporer des données contextuelles dans [!DNL Analytics] des variables.

Par exemple, dans la règle suivante, Analytics est défini pour renseigner les termes de recherche **interne (eVar2)** avec les données associées à **a.x_atag.search.term(Données contextuelles)**.

![](assets/examplerule.png)


## Schéma XDM

[!DNL Experience Platform] utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente entre les systèmes, il devient plus facile de conserver une signification et, par conséquent, de tirer profit des données. [!DNL Analytics] les données contextuelles fonctionnent avec la structure définie par le schéma.

L&#39;exemple suivant montre comment la commande [`event`](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) peut être utilisée avec l&#39; `xdm` option d&#39;envoi et de récupération de données avec l&#39;AEP [!DNL Web SDK]. Dans cet exemple, la `event` commande correspond au Schéma [Détails du commerce](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ExperienceEvent, de sorte que le suivi des éléments et `name` `SKU` valeurs productListItems et productListItems soit effectué :


```
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

Pour plus d’informations sur le suivi des événements avec l’AEP [!DNL Web SDK], voir événements [de](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html)suivi.
